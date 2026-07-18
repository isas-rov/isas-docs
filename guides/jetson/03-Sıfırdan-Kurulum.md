---
tags: [jetson, kurulum, sifirdan, jetpack]
---

# Sıfırdan Kurulum

> [!danger] Kart modelini belirlemeden imaj yazma
> Waveshare `JETSON-NANO-DEV-KIT`, 16 GB eMMC'li Jetson Nano modül kullanabilir. Sıradan NVIDIA SD kart imajını körlemesine yazmak, eMMC/boot yapısı nedeniyle beklenen sonucu vermeyebilir. Önce kart ve modül varyantını kesinleştir.

## 1. Gerekli Donanım

- Waveshare Jetson Nano geliştirme kiti ve soğutucu
- Uygun fan
- Kararlı 5 V / 4 A güç kaynağı (kitin önerdiği kaynak)
- Veri iletebilen Micro-USB kablo
- Windows bilgisayar
- 64 GB veya daha büyük, kaliteli/high-endurance SD kart
- İlk kurtarma için PuTTY
- Normal ağ için Ethernet kablosu veya uyumlu Wi-Fi adaptörü

Waveshare IO-BASE-A kartı; 4x USB 3.0, Gigabit Ethernet, HDMI, DisplayPort, 2x MIPI CSI, fan başlıkları, DC giriş ve Micro-USB veri/güç işlevleri sunar. Kesin konektör davranışı için kart revizyonunun [Waveshare sayfasını](https://www.waveshare.com/jetson-nano-dev-kit-a.htm) kullan.

## 2. Elektriksel Güvenlik

- Kartı iletken metal yüzey üzerine koyma.
- CSI şerit kabloyu cihaz enerjiliyken takıp çıkarma.
- GPIO sinyalleri 3,3 V seviyesindedir; GPIO'ya 5 V uygulama.
- Fan konnektörü yönünü kartın baskısından doğrula.
- Birden fazla güç girişini aynı anda kullanma; kart revizyonu için üretici talimatına uy.
- Gücü kesmeden önce `sudo poweroff` kullan.

## 3. Hangi Kurulum Yolunu Seçeceksin?

### Yol A — Satıcıdan yüklü sistem

Mevcut cihaz bu yolla geldi. Cihazda Ubuntu açılıyor fakat HDMI yoksa [[04-Seri-Konsol-PuTTY]] ile ilk girişi yap.

Doğrulama:

```bash
cat /etc/nv_tegra_release
```

```bash
lsblk -o NAME,SIZE,FSTYPE,MOUNTPOINT,LABEL
```

```bash
df -h /
```

### Yol B — Waveshare imajı/rehberi

Kartın tam modeline uygun imaj ve boot talimatı için [Waveshare JETSON-NANO-DEV-KIT Wiki](https://www.waveshare.com/wiki/JETSON-NANO-DEV-KIT) kullanılır.

Yükleme öncesi:

1. Kart revizyonunu ve modülün eMMC/SD varyantını kaydet.
2. Mevcut eMMC ve SD verilerini yedekle.
3. İmajın hedefinin eMMC mi SD mi olduğunu oku.
4. Windows Disk Yönetimi'nde kapasiteye bakarak hedef diski doğrula.
5. Yanlış diski seçmenin bilgisayar verilerini silebileceğini unutma.

### Yol C — NVIDIA SDK Manager

SDK Manager, desteklenen bir Ubuntu x86_64 ana bilgisayarda çalışır; kart Force Recovery modunda USB ile bağlanır. Windows üzerinde doğrudan SDK Manager kullanılmaz. Kartın Waveshare taşıyıcısı ve Nano eMMC modülü için doğru board configuration seçilmelidir.

> [!warning]
> SDK Manager'daki yanlış kart/taşıyıcı seçimi; USB, Ethernet, CSI veya pinmux'un çalışmamasına neden olabilir.

## 4. Headless İlk Açılış

HDMI olmadan:

1. Micro-USB veri kablosunu Windows'a tak.
2. Jetson'a kararlı güç ver.
3. Windows Aygıt Yöneticisi'nde `USB Serial Device (COMx)` ara.
4. PuTTY'yi `Serial`, `COMx`, `115200` ile aç.
5. İlk kurulum ekranı varsa kullanıcı, parola, saat dilimi ve makine adını tamamla.
6. Mevcut sistemde kullanıcı `jetson`, makine adı `jetson-desktop`.

NVIDIA da ekransız ilk kurulum için Micro-USB ve seri uygulama kullanımını belgeler: [Jetson Nano headless setup](https://developer.nvidia.com/embedded/learn/jetson-nano-2gb-devkit-user-guide#setup).

## 5. Temel Sistem Doğrulaması

```bash
uname -a
```

```bash
cat /etc/os-release
```

```bash
cat /etc/nv_tegra_release
```

```bash
dpkg-query -W nvidia-jetpack nvidia-cuda nvidia-cudnn8 nvidia-tensorrt
```

Mevcut sistemin beklenen özeti:

```text
Ubuntu 18.04.6 LTS
L4T R32.7.5
JetPack 4.6.5-b29
CUDA 10.2
```

## 6. Depolama Kontrolü

```bash
lsblk -o NAME,SIZE,FSTYPE,MOUNTPOINT,LABEL
```

Mevcut cihaz:

```text
mmcblk0       14.7G   eMMC
mmcblk1       58.6G   SD kart
mmcblk1p1              /
```

Gerçek kök diski kesin olarak kontrol et:

```bash
findmnt -n -o SOURCE /
```

Beklenen:

```text
/dev/mmcblk1p1
```

SD'ye taşıma ayrı ve riskli bir işlemdir; [[10-Depolama-SD-ve-eMMC]] notuna bak.

## 7. Ağ ve Saat

Normal modem/router varsa [[07-Normal-İnternet]], PdaNet varsa [[08-PdaNet-Proxy]] uygulanır.

Saat kontrolü:

```bash
date
timedatectl
```

Yanlış saat HTTPS sertifikalarını ve paket kurulumunu bozabilir.

## 8. Paket Depoları

İnternet doğrulandıktan sonra:

```bash
sudo apt update
```

> [!warning] Jetson paketlerini rastgele topluca yükseltme
> `sudo apt dist-upgrade` veya sürüm karıştıran NVIDIA paketleri boot/GPU uyumluluğunu bozabilir. Önce yedek al, L4T/JetPack sürümüne uygun paketleri kullan ve ihtiyaç duyulan paketleri tek tek kur.

## 9. Kurulum Sonu Kontrol Listesi

- [ ] Seri konsol açılıyor.
- [ ] Kullanıcı/parola biliniyor.
- [ ] `findmnt` doğru kök diski gösteriyor.
- [ ] `hostname -I` beklenen IP'yi gösteriyor.
- [ ] SSH açılıyor.
- [ ] VNC gerekiyorsa kurulmuş.
- [ ] `apt update` başarılı.
- [ ] `nvcc --version` ve `deviceQuery` başarılı.
- [ ] Fan çalışıyor.
- [ ] Pixhawk ve kamera ayrı ayrı test edilmiş.
