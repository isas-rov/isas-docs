---
tags: [jetson, terminal, komutlar, sozluk]
---

# Komut Sözlüğü

## Yol Sembolleri

| Sembol | Anlamı |
|---|---|
| `/` | Linux kök dizini |
| `~` | Mevcut kullanıcının ana dizini; Jetson'da `/home/jetson` |
| `.` | Mevcut dizin |
| `..` | Bir üst dizin |
| `.bashrc` | Noktayla başladığı için gizli ayar dosyası |

`/etc/...` ile `etc/...` aynı değildir. Baştaki `/`, yolun kökten başladığını söyler.

## Dosya ve Klasör Komutları

### `pwd`

Bulunduğun klasörü gösterir.

```bash
pwd
```

### `ls`

Dosyaları listeler.

```bash
ls
ls -la
```

`-l` ayrıntı, `-a` gizli dosyalar.

### `cd`

Klasör değiştirir.

```bash
cd ~/projects/isas
cd ..
cd ~
```

### `mkdir`

Klasör oluşturur.

```bash
mkdir -p ~/projects/isas
```

### `cp`

Kopyalar.

```bash
cp kaynak hedef
cp -a klasor hedef
```

### `mv`

Taşır veya yeniden adlandırır.

```bash
mv eski yeni
```

### `rm`

Siler. Geri dönüşüm kutusu yoktur.

```bash
rm dosya
```

> [!danger]
> `sudo rm -rf` komutunu neyi sildiğini kesin bilmeden kullanma.

## Dosya Okuma

### `cat`

Bir veya daha fazla dosyanın içeriğini terminale basar.

```bash
cat /etc/nv_tegra_release
```

`cat` burada değişiklik yapmaz; yalnızca okur.

### `head`

Dosyanın başını gösterir.

```bash
head -n 20 dosya
```

### `tail`

Dosyanın sonunu gösterir.

```bash
tail -n 20 dosya
tail -f uygulama.log
```

`-f`, yeni satırları canlı izler; `Ctrl+C` ile durur.

### `grep`

Metin içinde desen arar.

```bash
grep -n "APPEND" /boot/extlinux/extlinux.conf
```

`-n`, satır numarasını gösterir.

## Yetki ve Kabuk

### `sudo`

Bir komutu yönetici/root yetkisiyle çalıştırır.

```bash
sudo apt update
```

Her komut `sudo` gerektirmez. Sadece sistem dosyası, paket, servis veya donanım kontrolü için gerektiğinde kullan.

### `sh -c`

Metin olarak verilen tüm komutu yeni kabukta çalıştırır.

```bash
sudo sh -c 'echo 128 > /sys/devices/pwm-fan/target_pwm'
```

Burada `>` dahil tüm işlem root yetkisinde olur.

### `source`

Bir kabuk dosyasını mevcut terminale yükler.

```bash
source ~/.bashrc
```

Kısa eşdeğeri:

```bash
. ~/.bashrc
```

## Yönlendirme ve Boru

### `>`

Komut çıktısıyla dosyayı yeniden yazar.

```bash
echo test > dosya.txt
```

### `>>`

Dosyanın sonuna ekler.

```bash
echo test >> dosya.txt
```

### `|`

Soldaki komutun çıktısını sağdaki komutun girdisine verir.

```bash
env | grep -i proxy
```

### `2>/dev/null`

Hata çıktısını görünmez sanal cihaza yollar.

```bash
grep alias ~/.bashrc ~/.bash_aliases 2>/dev/null
```

Tanılama sırasında hatayı gizlemek istemiyorsan kullanma.

### `&`

Komutu arka planda çalıştırır.

```bash
vncconfig -nowin &
```

## Ağ Komutları

### `hostname -I`

Cihazın IP adreslerini listeler.

### `ip address`

Ağ arayüzü adreslerini gösterir/değiştirir.

```bash
ip -br address
sudo ip address replace 192.168.137.2/24 dev l4tbr0
```

### `ip route`

Yönlendirme tablosunu gösterir/değiştirir.

```bash
ip route
ip route get 1.1.1.1
```

### `ping`

ICMP erişim testi yapar.

```bash
ping -c 3 192.168.137.1
```

`-c 3`, üç paket sonra durur. Proxy bağlantısında ping başarısız olsa bile HTTP çalışabilir.

### `nmcli`

NetworkManager komut satırı aracıdır.

```bash
nmcli device status
nmcli connection show --active
```

## Disk Komutları

### `lsblk`

Disk ve bölümleri listeler.

```bash
lsblk -o NAME,SIZE,FSTYPE,MOUNTPOINT,LABEL
```

### `df`

Dosya sistemi kullanımı.

```bash
df -h /
```

`-h`, insan okunabilir GB/MB gösterir.

### `findmnt`

Neyin nereye bağlı olduğunu gösterir.

```bash
findmnt -n -o SOURCE /
```

### `mount`

Dosya sistemini bir klasöre bağlar.

```bash
sudo mount /dev/mmcblk0p1 /mnt/emmc
```

### `mkfs.ext4`

Bir bölümü ext4 olarak biçimlendirir ve mevcut verileri siler.

## Paket Komutları

### `apt update`

Depo paket listelerini yeniler; paketleri yükseltmez.

```bash
sudo apt update
```

### `apt install`

Paket kurar.

```bash
sudo apt install python3-pip
```

### `apt-get -s`

Kurulumu simüle eder.

```bash
apt-get -s install PAKET
```

### `dpkg-query -W`

Kurulu Debian paket sürümünü gösterir.

## Servis Komutları

### `systemctl status`

Servis durumunu gösterir.

```bash
sudo systemctl status ssh
```

### `systemctl enable --now`

Servisi hemen başlatır ve boot'ta otomatikleştirir.

```bash
sudo systemctl enable --now ssh
```

## Süreç Komutları

### `ps`

Çalışan süreçleri gösterir.

### `pkill`

Ada/desene göre süreç sonlandırır.

```bash
pkill -f chromium
```

### `lsof`

Bir dosya/portu hangi sürecin açtığını gösterir.

```bash
sudo lsof /dev/ttyACM0
```

## Editör

### `nano`

Terminal metin editörü.

```bash
nano ~/.bash_aliases
```

- Kaydet: `Ctrl+O`, `Enter`
- Çık: `Ctrl+X`
- Arama: `Ctrl+W`
- Satır kes: `Ctrl+K`
- Yapıştır: `Ctrl+U`

## Yeniden Başlatma/Kapatma

```bash
sudo reboot
sudo poweroff
```

`reboot` yeniden başlatır; `poweroff` güvenli kapatır.
