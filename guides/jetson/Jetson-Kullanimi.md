---
tags:
  - jetson
  - rehber
  - yazilim
aliases:
  - Jetson Kullanımı
  - Jetson Nano Rehberi
---

# Jetson Nano Kullanım Kasası

Bu not, ayrıntılı Jetson Nano bilgi kasasının giriş sayfasıdır.

> [!summary] Mevcut kurulumun kısa özeti
> - Kart: Waveshare `JETSON-NANO-DEV-KIT` / IO-BASE-A tabanlı Jetson Nano 4 GB
> - Sistem: Ubuntu 18.04.6, L4T `R32.7.5`, JetPack `4.6.5-b29`
> - Ana kök dosya sistemi: 64 GB SD karttaki `/dev/mmcblk1p1`
> - Windows–Jetson USB ağı: Windows `192.168.137.1`, Jetson `192.168.137.2`
> - Kurtarma/seri konsol: PuTTY, `COM5`, `115200`
> - SSH: `ssh jetson@192.168.137.2`
> - VNC: `192.168.137.2:1`
> - PdaNet interneti: Windows'taki `jetproxy` üzerinden HTTP/HTTPS proxy

## Nereden Başlamalıyım?

- Her gün cihazı açıp bağlanmak için: [[02-Hızlı-Giriş]]
- Ağ mantığını anlamak için: [[01-Sistem-Özeti-ve-Kavramlar]]
- Yeni bir cihazı ilk kez kurmak için: [[03-Sıfırdan-Kurulum]]
- HDMI olmadan kurtarma için: [[04-Seri-Konsol-PuTTY]]
- SSH ve başka bilgisayardan bağlanmak için: [[05-IP-SSH-ve-Başka-Bilgisayardan-Bağlanma]]
- Grafik arayüz için: [[06-VNC-Grafik-Arayüz]]
- Modem/router/normal internet için: [[07-Normal-İnternet]]
- PdaNet interneti için: [[08-PdaNet-Proxy]]
- Kısaltmalar ve terminal mantığı için: [[09-Aliaslar-ve-Terminal]]
- SD kart/eMMC/boot için: [[10-Depolama-SD-ve-eMMC]]
- CUDA, Python ve kodlama için: [[11-CUDA-Python-ve-Kodlama]]
- Fan, GPIO ve LED için: [[12-Fan-GPIO-ve-LED]]
- Pixhawk için: [[13-Pixhawk-Bağlantısı]]
- CSI kamera için: [[14-CSI-Kamera]]
- Hata durumları için: [[15-Arıza-Çözme]]
- Komutların anlamı için: [[16-Komut-Sözlüğü]]
- Güvenlik ve yedek için: [[17-Güvenlik-ve-Yedekleme]]

## En Önemli Kural

> [!danger] Komut istemini kopyalama
> Belgelerde `jetson@jetson-desktop:~$` veya `PS C:\...>` komutun parçası değildir. Yalnızca bu işaretlerden sonra gelen komutu yaz.

## Resmî Kaynaklar

- [Waveshare JETSON-NANO-DEV-KIT ürün sayfası](https://www.waveshare.com/jetson-nano-dev-kit-a.htm)
- [Waveshare Jetson Nano Wiki](https://www.waveshare.com/wiki/JETSON-NANO-DEV-KIT)
- [NVIDIA Jetson Nano başlangıç rehberi](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-2gb-devkit)
- [NVIDIA Jetson Linux R32.7.5 sürüm notları](https://docs.nvidia.com/jetson/archives/l4t-archived/l4t-3275/pdf/Jetson_Linux_Release_Notes_R32.7.5_GA.pdf)
