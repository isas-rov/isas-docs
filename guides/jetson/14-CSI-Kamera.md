---
tags: [jetson, kamera, csi, imx219]
---

# CSI Kamera — IMX219

## Kamera Bilgisi

Kamera: IMX219-77IR, 8 MP, 3280×2464, CSI. Sensör ailesi Jetson Nano tarafında desteklenen IMX219 sürücüsüyle uyumludur. Bununla birlikte ürün adı tek başına fiziksel kablo/yön/elektrik uyumluluğunu garanti etmez.

## Mevcut Hata

```bash
ls /dev/video*
```

Sonuç:

```text
ls: cannot access '/dev/video*': No such file or directory
```

Kernel logu:

```text
imx219 7-0010: error during i2c read probe (-121)
imx219 8-0010: error during i2c read probe (-121)
board setup failed
```

`-121`, sürücünün I²C adresi `0x10` üzerinden sensörden onay/cevap alamadığını gösterir. VNC veya masaüstü sorunu değildir; kamera donanım bağlantısı/sensör algılama aşamasında kalmıştır.

## En Önemli Güvenlik Kuralı

> [!danger] CSI kabloyu enerjiliyken takıp çıkarma
> `sudo poweroff` ile kapat, sistem tamamen durunca güç kablosunu çıkar. CSI hatlarında hot-plug yapmak sensöre veya Jetson CSI arayüzüne zarar verebilir.

## Fiziksel Kontrol Sırası

1. Jetson'da:

```bash
sudo poweroff
```

2. Sistem durduktan sonra gücü fiziksel olarak kes.
3. CSI soket kilidini nazikç aç.
4. Kablonun temas uçlarında kir, oksit, katlanma veya yırtık kontrol et.
5. Kabloyu sokete tam, düz ve paralel yerleştir.
6. Temas yönünü kart baskısı ve Waveshare dokümanından doğrula; varsayım yapma.
7. Kilidi iki taraftan eşit kapat.
8. Kamera kartı tarafındaki CSI soketini de aynı şekilde kontrol et.
9. Güç ver ve boot tamamlanınca test et.

## Yazılım Testi

```bash
sudo dmesg | grep -A4 -B2 imx219
```

```bash
ls -l /dev/video*
```

Algılanırsa genellikle `/dev/video0` oluşur.

V4L2 bilgi paketi gerekiyorsa:

```bash
sudo apt install v4l-utils
v4l2-ctl --list-devices
v4l2-ctl --all -d /dev/video0
```

Argus/GStreamer testi:

```bash
nvgstcapture-1.0
```

Ekransız/VNC ortamında basit pipeline:

```bash
gst-launch-1.0 nvarguscamerasrc num-buffers=120 ! 'video/x-raw(memory:NVMM),width=1280,height=720,framerate=30/1' ! nvvidconv ! fakesink
```

Bu komut 120 kareyi okuyup görüntülemeden işler; kamera akışını test eder.

## İki CSI Portunu Denemek

Kartta iki CSI portu var ve logda I²C bus 7 ile 8 için sürücü denemesi görüldü. Port değiştirirken her seferinde:

1. Yazılımsal kapat.
2. Gücü kes.
3. Kabloyu taşı.
4. Kilit/yön kontrolü yap.
5. Yeniden boot et.
6. `dmesg` ve `/dev/video*` kontrolü yap.

## Multimetre/Kablo Yoksa Ne Yapılabilir?

Bir şerit kablonun elektriksel sürekliliğini kesin ölçmenin doğru yolu multimetre veya bilinen-sağlam yedek kablodur. Gözle kontrol yalnızca açık kırık/kat izi bulabilir; iç iletken kopuğunu dışlayamaz.

Yedek yoksa sıralama:

1. Kabloyu iki uçta yeniden oturt.
2. Doğru yönü belgeyle karşılaştır.
3. İkinci CSI portunu dene.
4. Kamera kartındaki görünür hasarı incele.
5. Bilinen-sağlam aynı pin aralığında CSI kablo edin.
6. Mümkünse bilinen-sağlam IMX219 ile çapraz test yap.

## Hata Yorumlama

| Belirti | Yorum |
|---|---|
| `no acknowledge ... 0x10` | Sensör I²C cevabı yok; kablo/yön/güç/sensör |
| `/dev/video0` yok | Probe tamamlanmadı |
| `/dev/video0` var, Argus hata | Mod/daemon/pipeline sorunu olabilir |
| Bir port çalışıyor, diğeri çalışmıyor | Port, pinmux veya soket sorunu |
| Görüntü mor/pembe | IR filtre/aydınlatma/renk kalibrasyonu |

## Kamera Çalıştıktan Sonra Kodlama

Jetson CSI kamera için OpenCV'de `cv2.VideoCapture(0)` her zaman en iyi yol değildir. NVIDIA `nvarguscamerasrc` GStreamer pipeline'ı, donanım hızlandırmalı CSI akışı için tercih edilir. Önce GStreamer ile kararlı akışı doğrula, sonra OpenCV pipeline ekle.
