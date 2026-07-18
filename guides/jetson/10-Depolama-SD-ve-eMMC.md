---
tags: [jetson, sd, emmc, ext4, boot]
---

# Depolama: SD Kart, eMMC ve Kök Dosya Sistemi

## Mevcut Yapı

```text
/dev/mmcblk0      14.7G  → dahili 16 GB eMMC
/dev/mmcblk1      58.6G  → 64 GB SD kart
/dev/mmcblk1p1            → mevcut kök dosya sistemi /
```

Doğrulama:

```bash
findmnt -n -o SOURCE /
```

Beklenen:

```text
/dev/mmcblk1p1
```

Kapasite:

```bash
df -h /
```

Doğrulanmış sonuç:

```text
/dev/mmcblk1p1   58G   15G   41G  27% /
```

## Neden SD Karta Taşındı?

16 GB eMMC, tam JetPack/CUDA ve proje dosyaları için dardı. SD kart:

- Yaklaşık 58 GB kullanılabilir alan sağladı.
- CUDA, cuDNN, TensorRT ve geliştirme paketlerinin kurulmasına alan açtı.
- Veri seti, model ve loglar için daha geniş alan verdi.

## Windows Neden SD Kartı Görmüyor?

SD kart başta exFAT iken Windows `E:` sürücüsü olarak gördü. Jetson için `ext4` olarak biçimlendirildikten sonra Windows Dosya Gezgini ext4 dosya sistemini doğrudan okuyamaz. Bu, kartın bozuk olduğu anlamına gelmez.

`L4T-README` yaklaşık 16 MB'lık ayrı USB gadget bölümüdür; ana Jetson depolaması değildir.

## Yaptığımız Taşıma İşleminin Kaydı

> [!danger] Bu bölümü tekrar çalıştırma
> Aşağıdaki `mkfs.ext4` komutu seçilen bölümdeki tüm veriyi siler. Mevcut sistem zaten SD'den çalışıyor. Bu bölüm yalnızca ne yaptığımızın kaydı ve gelecekte kontrollü kurtarma rehberidir.

### 1. Diskleri ayırt ettik

```bash
lsblk -o NAME,SIZE,FSTYPE,MOUNTPOINT,LABEL
```

SD kart `/dev/mmcblk1p1` olarak belirlendi.

### 2. ext4 olarak biçimlendirdik

Kartın doğru olduğu kesinleştirildikten sonra:

```bash
sudo mkfs.ext4 /dev/mmcblk1p1
```

Bu işlem inode tablolarını, journal'ı ve ext4 süper bloklarını oluşturdu.

### 3. Bağlama noktası oluşturduk

```bash
sudo mkdir -p /mnt/sdroot
sudo mount /dev/mmcblk1p1 /mnt/sdroot
```

Kontrol:

```bash
df -h /mnt/sdroot
```

### 4. Kök dosya sistemini kopyaladık

```bash
sudo cp -a --one-file-system /. /mnt/sdroot/
```

- `cp`: Kopyalar.
- `-a`: Sahiplik, izin, sembolik link ve zaman bilgilerini koruyan arşiv modu.
- `--one-file-system`: `/dev`, `/proc`, `/sys` gibi başka bağlı sanal dosya sistemlerine geçmez.
- `/.`: Kök dizinin içeriği.
- `/mnt/sdroot/`: SD kart hedefi.

Kopyalama sırasında terminal uzun süre sessiz kalabilir. Komut istemi geri geldiğinde tamamlanmıştır.

Kontrol:

```bash
df -h /mnt/sdroot
```

Kopya yaklaşık 4,7 GB yer kapladı.

### 5. Boot root parametresini SD'ye yönlendirdik

`extlinux.conf` içinde:

```text
root=/dev/mmcblk1p1
```

kullanıldı.

Kontrol:

```bash
grep -n "APPEND" /boot/extlinux/extlinux.conf
```

Hem eMMC boot tarafı hem SD kopyası, SD kök bölümüne yönlendirildi.

### 6. Yeniden başlattık ve kesin doğrulama yaptık

```bash
sudo reboot
```

Sonra:

```bash
findmnt -n -o SOURCE /
df -h /
```

Sonuç `/dev/mmcblk1p1` oldu.

## Boot Parametresinde İki `root=` Görülmesi

Kernel komut satırında hem eMMC'den gelen eski `root=/dev/mmcblk0p1` hem de extlinux'tan eklenen `root=/dev/mmcblk1p1` görülebilir. Hangi kökün gerçekten kullanıldığını tartışmak yerine şu komut kesin cevabı verir:

```bash
findmnt -n -o SOURCE /
```

## SD Kartı Çıkarırsak Ne Olur?

Mevcut boot yapılandırması `/dev/mmcblk1p1` bekliyor. SD kart takılı değilse sistem kök dosya sistemini bulamayabilir ve açılmayabilir. SD kartı sökmeden önce eMMC'ye dönüş boot ayarı hazırlanmalıdır.

## eMMC'ye Kontrollü Dönüş

> [!warning]
> Bu işlem yalnızca eMMC'deki sistemin sağlam olduğu doğrulandıktan sonra yapılır. Yanlış extlinux ayarı sistemi açılmaz hale getirebilir.

eMMC'yi bağla:

```bash
sudo mkdir -p /mnt/emmc
sudo mount /dev/mmcblk0p1 /mnt/emmc
```

Dosyaları kontrol et:

```bash
ls -l /mnt/emmc/boot/extlinux/
grep -n "APPEND" /mnt/emmc/boot/extlinux/extlinux.conf
```

Yedek varsa içeriğini önce oku:

```bash
grep -n "APPEND" /mnt/emmc/boot/extlinux/extlinux.conf.emmc-backup
```

Ancak yedeğin gerçekten `root=/dev/mmcblk0p1` içerdiği doğrulanırsa geri kopyalanır.

## Disk Sağlığı ve Alan

```bash
df -h /
df -i /
```

Büyük klasörleri bul:

```bash
sudo du -xh --max-depth=1 / 2>/dev/null | sort -h
```

APT önbelleğini temizlemek için:

```bash
sudo apt clean
```

Silmeden önce neyin yer kapladığını kontrol et; rastgele `/usr/local/cuda`, NVIDIA paketleri veya `/boot` dosyalarını silme.

## Yedek Stratejisi

- Kodları Git ile ayrı depoda tut.
- Yapılandırma dosyalarını Obsidian notlarında kaydet.
- Önemli model/veri setlerini haricî diske kopyala.
- Boot değişikliğinden önce `extlinux.conf` dosyasını tarihli yedekle:

```bash
sudo cp /boot/extlinux/extlinux.conf /boot/extlinux/extlinux.conf.$(date +%Y%m%d-%H%M%S).bak
```
