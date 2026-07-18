---
tags: [jetson, pixhawk, mavlink, serial]
---

# Pixhawk Bağlantısı

Bkz: [[Pixhawk]], [[Baglanti-Haritasi]].

## Mevcut Doğrulanmış Bağlantı

Pixhawk USB ile takıldığında:

```text
/dev/ttyACM0
/dev/serial/by-id/usb-3D_Robotics_PX4_FMU_v2.x_0-if00
```

Kalıcı `by-id` yolu, yeniden başlatmada `ttyACM0` numarası değişse bile aynı cihazı bulmak için tercih edilir.

## 1. Fiziksel Güvenlik

> [!danger]
> - Masa üstü testte pervane/thruster güçlerini ayır.
> - USB, Pixhawk'a kısmi güç verebilir; motor/servo hattını USB'den beslemeye çalışma.
> - Pixhawk Power portu, USB ve haricî 5 V kaynaklarının topraklama/besleme planını dokümansız birleştirme.
> - TELEM/UART kullanılacaksa 3,3 V lojik seviyesini ve TX/RX çapraz bağlantısını doğrula.

## 2. USB Cihazını Bul

```bash
ls -l /dev/serial/by-id/
```

```bash
ls -l /dev/ttyACM*
```

```bash
dmesg | tail -n 50
```

Mevcut izin:

```text
crw-rw---- 1 root dialout ... /dev/ttyACM0
```

Bu, yalnızca `root` ve `dialout` grubunun porta yazabileceği anlamına gelir.

## 3. `dialout` Grubu

Mevcut grup listesinde `dialout` yoksa:

```bash
sudo usermod -aG dialout jetson
```

- `usermod`: Kullanıcı hesabını değiştirir.
- `-aG`: Var olan grupları silmeden ek gruba ekler.
- `dialout`: Seri port erişim grubu.
- `jetson`: Kullanıcı adı.

Değişiklik için oturumu tamamen kapatıp aç veya yeniden başlat:

```bash
sudo reboot
```

Sonra:

```bash
groups
```

Listede `dialout` olmalı.

## 4. Neden `cat /dev/ttyACM0` ile IMU Göremeyebiliriz?

Pixhawk, terminal metni değil ikili MAVLink paketleri gönderir. `cat` bu ikili veriyi anlamlandıramaz; bazen hiç okunabilir çıktı görünmez. Doğru test MAVLink kütüphanesi veya QGroundControl kullanmaktır.

## 5. pip ve pymavlink

```bash
sudo apt install python3-pip
```

Bir sanal ortam oluştur:

```bash
mkdir -p ~/projects/isas/pixhawk
cd ~/projects/isas/pixhawk
python3 -m venv .venv
source .venv/bin/activate
```

Kurulum:

```bash
python -m pip install pymavlink
```

> [!warning] Python 3.6
> Yeni pymavlink/pip sürümleri Python 3.6 desteğini bırakmış olabilir. Kurulum hata verirse hata mesajındaki Python gereksinimini oku ve Python 3.6'yı destekleyen son pymavlink sürümünü sabitle. Sistem Python'unu kaldırma/yükseltme.

## 6. Heartbeat ve IMU Test Programı

```bash
nano ~/projects/isas/pixhawk/pixhawk_test.py
```

İçerik:

```python
#!/usr/bin/env python3
from pymavlink import mavutil

PORT = "/dev/serial/by-id/usb-3D_Robotics_PX4_FMU_v2.x_0-if00"

print("Pixhawk baglantisi aciliyor:", PORT)
master = mavutil.mavlink_connection(PORT, baud=115200)

heartbeat = master.wait_heartbeat(timeout=15)
print(
    "Heartbeat alindi. system=", master.target_system,
    "component=", master.target_component,
)

master.mav.request_data_stream_send(
    master.target_system,
    master.target_component,
    mavutil.mavlink.MAV_DATA_STREAM_ALL,
    4,
    1,
)

for _ in range(20):
    message = master.recv_match(
        type=["ATTITUDE", "RAW_IMU", "HIGHRES_IMU"],
        blocking=True,
        timeout=5,
    )
    if message is None:
        print("5 saniye icinde IMU/attitude mesaji gelmedi")
    else:
        print(message)
```

Çalıştır:

```bash
cd ~/projects/isas/pixhawk
source .venv/bin/activate
python pixhawk_test.py
```

## 7. Hata Durumları

### `/dev/ttyACM0` yok

```bash
lsusb
dmesg | tail -n 100
```

- USB kablo yalnızca şarj kablosu olabilir.
- Pixhawk USB portu/kablosu sorunlu olabilir.
- Pixhawk bootloader/firmware aşamasında olabilir.

### `Permission denied`

```bash
ls -l /dev/ttyACM0
groups
```

`dialout` grubunu ekle ve yeni login yap.

### Port meşgul

```bash
sudo lsof /dev/ttyACM0
```

QGroundControl, ModemManager veya başka bir Python programı portu açmış olabilir. ModemManager gerçekten sorun yaratıyorsa servis durumu incelenir; sebep kanıtlanmadan sistem servislerini kalıcı kapatma.

### Heartbeat yok

- Doğru portu kullan.
- Pixhawk firmware'inin çalıştığını kontrol et.
- USB için baud genellikle kritik olmasa da `115200` kullanılabilir.
- PX4/ArduPilot MAVLink port ve stream ayarlarını kontrol et.
- Aynı porta tek program bağlansın.

## 8. USB mi UART mı?

| Yöntem | Artı | Eksi |
|---|---|---|
| USB `/dev/ttyACM0` | Hızlı kurulum, tak-çalıştır | Kablo/konnektör kilidi zayıf, cihaz adı değişebilir |
| UART/TELEM | Araç içi kalıcı kablolamaya uygun | Pinout, lojik seviye, baud ve toprak dikkat ister |

Masa üstü geliştirmede USB ile başla. Araç içi nihai tasarımda kilitli konnektörlü TELEM/UART değerlendir.
