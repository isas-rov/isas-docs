---
tags: [jetson, fan, gpio, led, elektronik]
---

# Fan, GPIO ve LED

## Fan Kontrol Dosyası

Mevcut sistemde fan PWM hedefi:

```text
/sys/devices/pwm-fan/target_pwm
```

Değer aralığı:

```text
0   → kapalı
128 → yaklaşık orta
255 → tam
```

Mevcut değer:

```bash
cat /sys/devices/pwm-fan/target_pwm
```

## Fan Komutları

Kapat:

```bash
sudo sh -c 'echo 0 > /sys/devices/pwm-fan/target_pwm'
```

Orta:

```bash
sudo sh -c 'echo 128 > /sys/devices/pwm-fan/target_pwm'
```

Tam:

```bash
sudo sh -c 'echo 255 > /sys/devices/pwm-fan/target_pwm'
```

Kısaltmalar:

```bash
fanstop
fanmid
fanfull
```

> [!warning]
> Bazı fanlar düşük PWM'de ilk hareketi başlatamaz. Önce `255` ile başlatıp sonra `128` dene. Fan hiç dönmüyorsa konektör yönü, voltaj uyumu, kablo ve fiziksel sıkışmayı kontrol et.

## Sıcaklık ve Yük

```bash
tegrastats
```

Sıcaklık bölgeleri:

```bash
for z in /sys/class/thermal/thermal_zone*; do echo -n "$(cat "$z/type"): "; cat "$z/temp"; done
```

Değerler genellikle miliselsiyus cinsindedir; `50000` yaklaşık 50 °C'dir.

## GPIO Elektrik Kuralları

> [!danger]
> - Jetson GPIO sinyalleri 3,3 V'tur.
> - GPIO pinine 5 V verme.
> - LED'i dirençsiz bağlama.
> - Bağlantıyı güç kesikken yap.
> - Fiziksel pin numarasıyla BCM/SoC numarasını karıştırma.

## Breadboard LED Bağlantısı

Örnek `GPIO.BOARD` düzeni:

```text
Jetson fiziksel pin 12 → 220–330 Ω direnç → LED uzun bacak (anot)
LED kısa bacak (katot) → Jetson GND, örneğin fiziksel pin 6
```

Direnç LED akımını sınırlar ve GPIO/LED'i korur.

## Jetson.GPIO Kontrolü

```bash
python3 -c "import Jetson.GPIO as GPIO; print(GPIO.VERSION)"
```

Kullanıcı grupları:

```bash
groups
```

Mevcut kullanıcının `gpio` grubunda olduğu doğrulandı.

## LED Yak/Söndür Programı

```bash
mkdir -p ~/projects/isas/gpio
nano ~/projects/isas/gpio/led_blink.py
```

İçerik:

```python
#!/usr/bin/env python3
import time
import Jetson.GPIO as GPIO

LED_PIN = 12  # Fiziksel BOARD pin numarasi

GPIO.setmode(GPIO.BOARD)
GPIO.setup(LED_PIN, GPIO.OUT, initial=GPIO.LOW)

try:
    while True:
        GPIO.output(LED_PIN, GPIO.HIGH)
        print("LED acik")
        time.sleep(1)

        GPIO.output(LED_PIN, GPIO.LOW)
        print("LED kapali")
        time.sleep(1)
except KeyboardInterrupt:
    print("Program durduruldu")
finally:
    GPIO.output(LED_PIN, GPIO.LOW)
    GPIO.cleanup()
```

Çalıştır:

```bash
python3 ~/projects/isas/gpio/led_blink.py
```

Durdur:

```text
Ctrl+C
```

`finally` bölümü, program hata verse veya `Ctrl+C` ile dursa bile LED'i kapatır ve GPIO kaynağını temizler.

## Bir Kez Yakmak

```python
#!/usr/bin/env python3
import Jetson.GPIO as GPIO

LED_PIN = 12
GPIO.setmode(GPIO.BOARD)
GPIO.setup(LED_PIN, GPIO.OUT)
GPIO.output(LED_PIN, GPIO.HIGH)
input("LED acik. Kapatmak icin Enter...")
GPIO.output(LED_PIN, GPIO.LOW)
GPIO.cleanup()
```

## GPIO Hatası Kontrolü

```bash
ls -l /dev/gpiochip*
groups
```

`Permission denied` gelirse kullanıcının `gpio` grubunu ve Jetson.GPIO udev kurallarını kontrol et. Sorunu anlamadan her programı `sudo` ile çalıştırmak yerine izinleri düzelt.
