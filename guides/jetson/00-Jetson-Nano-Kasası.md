---
tags: [jetson, moc, ana-sayfa]
cssclasses: [jetson-kasasi]
---

# Jetson Nano Kasası

Bu klasör, Jetson Nano'yu ilk açılıştan proje geliştirmeye kadar kullanmak için gereken teknik hafızadır. Ana giriş: [[Jetson Kullanımı]].

## Senaryonu Seç

| Senaryo | İlk okunacak not | Kullanılacak adres |
|---|---|---|
| PdaNet + Windows + USB | [[08-PdaNet-Proxy]] | `192.168.137.2` |
| Normal modem/router + Ethernet | [[07-Normal-İnternet]] | Router'ın verdiği IP |
| Sadece Windows–Jetson USB | [[05-IP-SSH-ve-Başka-Bilgisayardan-Bağlanma]] | Genellikle `192.168.55.1` |
| HDMI yok, cihaz açılmıyor gibi | [[04-Seri-Konsol-PuTTY]] | `COM5`, `115200` |
| Grafik masaüstü gerekli | [[06-VNC-Grafik-Arayüz]] | `<Jetson-IP>:1` |
| Yeni SD/eMMC kurulumu | [[03-Sıfırdan-Kurulum]] | Kurulumdan sonra belirlenir |

## Günlük Çalışma Zinciri

```text
Güç ver
   ↓
Seri konsol veya USB ağıyla kontrol et
   ↓
IP adresini doğrula
   ↓
SSH veya VNC ile bağlan
   ↓
Gerekliyse internet/proxy'yi aç
   ↓
Pixhawk, kamera, GPIO ve proje kodunu çalıştır
```

## Mevcut Sistemde Doğrulanmış Noktalar

- `cat /etc/nv_tegra_release` sonucu L4T `R32.7.5`.
- `nvidia-jetpack`, `nvidia-cuda`, `nvidia-cudnn8`, `nvidia-tensorrt` sürümü `4.6.5-b29`.
- CUDA `10.2`; `deviceQuery` sonucu `PASS`.
- Kök dosya sistemi `/dev/mmcblk1p1`, yaklaşık 58 GB.
- Pixhawk `/dev/ttyACM0` ve `/dev/serial/by-id/usb-3D_Robotics_PX4_FMU_v2.x_0-if00` olarak görüldü.
- CSI IMX219 henüz algılanmadı; I²C `-121` hatası ayrı notta izleniyor.
- PdaNet üzerinden Ubuntu ve NVIDIA depolarına `apt update` başarılı.

## Hızlı Bağlantılar

- [[02-Hızlı-Giriş]]
- [[15-Arıza-Çözme]]
- [[16-Komut-Sözlüğü]]
- [[Proje-Ozeti]]
- [[Sistem-Mimarisi]]
- [[Pixhawk]]
- [[Kamera-ve-Sensorler]]
