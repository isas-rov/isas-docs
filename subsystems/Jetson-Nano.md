# Jetson Nano

Bkz: [[Jetson Kullanımı]], [[00-Jetson-Nano-Kasası]], [[Pixhawk]], [[Kamera-ve-Sensorler]], [[Baglanti-Haritasi]]

> [!info] Kurulum ve kullanım rehberi
> Günlük bağlantı, PdaNet, SSH, VNC, CUDA, Pixhawk ve kamera adımları için [[Jetson Kullanımı]] notunu kullan.

## Sistemdeki Rolu

Jetson Nano, ana aracin gorev bilgisayaridir.

## Kullanim Amaci

- On kameradan gelen goruntuyu isleme
- Alt kameradan gelen goruntuyu isleme
- Hat takibi algoritmasi calistirma
- Nesne/hedef algilama
- Gorev durumu yonetimi
- Pixhawk'a ust seviye komut uretme
- Gerekirse Mini ROV video akisinin yonetimine katki verme

## Belgelerde Gecen Teknik Ozellikler

- 128-core Maxwell GPU
- Quad-core ARM Cortex-A57 @ 1.43 GHz
- 4 GB LPDDR4 RAM
- MicroSD depolama
- 5V / 4A besleme

## Muhtemel Baglantilari

- On kamera -> Jetson Nano
- Alt kamera -> Jetson Nano
- Jetson Nano -> Pixhawk
- Jetson Nano -> Ethernet switch
- Jetson Nano -> Yer istasyonu veri zinciri

## En Kritik Teknik Belirsizlik

> [!warning] Port secimi net degil
> Jetson ile Pixhawk arasindaki ana haberlesme yolunun `USB mi` yoksa `UART/TELEM mi` olacagi netlestirilmelidir.
