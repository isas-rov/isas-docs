# Sistem Mimarisi

Bkz: [[Proje-Ozeti]], [[Elektrik-Sistemi]], [[Baglanti-Haritasi]]

## Ust Duzey Yapi

Sistem asagidaki 3 bolumden olusur:

1. Su ustu kontrol istasyonu
2. Ana arac
3. Mini ROV

## Su Ustu Kontrol Istasyonu

Amac:

- Operatore tek merkezden kontrol vermek
- Kamera akislarini gostermek
- Telemetriyi izlemek
- Alarm ve failsafe durumlarini gostermek

Icerdigi islevler:

- Operator bilgisayari
- Kontrol arayuzu
- Telemetri izleme
- Acil durdurma erisimi

## Ana Arac

Ana alt sistemler:

- [[Jetson-Nano]]
- [[Pixhawk]]
- [[Guc-ve-Haberlesme-Altyapisi]]
- [[Kamera-ve-Sensorler]]
- 6 adet thruster + 6 adet ESC
- Mini ROV birakma/baglama arayuzu

Ana gorev zinciri:

1. Kamera verisi toplanir.
2. Goruntu `Jetson Nano` tarafinda islenir.
3. Gorev karari uretilir.
4. Komut `Pixhawk` tarafina aktarilir.
5. `Pixhawk`, ESC'lere PWM vererek thrusterlari surer.

## Mini ROV

Ana alt sistemler:

- [[Mini-ROV-Kontrol-Yigini]]
- Mini PDB
- 4 adet motor + 4 adet ESC
- Kamera modulu
- Su gecirmez konnektorler

Calisma mantigi:

1. Ana aractan ayrilir.
2. Goruntu `Pi Zero 2 W` ile toplanir ve aktarilir.
3. Komutlar `Pi Pico` tarafinda islenir.
4. PWM cikislari ile 4 itici surulur.
5. Sizinti veya paket kaybinda failsafe uygulanir.

## Veri Akisi

Ana arac:

- On kamera -> Jetson Nano
- Alt kamera -> Jetson Nano
- Jetson Nano -> Pixhawk
- Pixhawk -> ESC -> Thruster

Mini ROV:

- Camera Module 3 Wide -> Pi Zero 2 W
- Operator komutu -> Ana arac -> Mini ROV
- Mini ROV komutu -> Pi Pico -> ESC -> Motor

## Haberlesme Akisi

- Kara <-> Ana Arac: tether/ethernet tabanli
- Ana Arac <-> Mini ROV: komut + video + ortak toprak referansi
- Mini ROV video akisi ana arac uzerinden karaya tasinir

## Elektrik Mimarisiyle Iliskisi

- Ust seviye islev akisi icin bu not kullanilir.
- Gercek sema ve kablolama icin [[Elektrik-Sistemi]] ve [[Baglanti-Haritasi]] kullanilir.
