# Pixhawk

Bkz: [[Jetson-Nano]], [[Elektrik-Sistemi]], [[Baglanti-Haritasi]]

## Sistemdeki Rolu

Pixhawk, ana aracin dusuk seviye hareket kontrol ve PWM cikis katmanidir.

## Kullanim Amaci

- Denge ve yonelim
- Derinlik kontrolu
- Kapali cevrim hareket kontrolu
- ESC'lere PWM sinyali gonderme
- Telemetri ve kontrol verisi yonetimi

## Belgelerde Gecen Teknik Ozellikler

- STM32F765 @ 216 MHz
- Dahili IMU
- UART, I2C, SPI, CAN
- ArduSub / PX4 uyumlu
- 8+ kanal PWM cikisi

## Muhtemel Baglantilari

- Jetson Nano -> Pixhawk
- Pixhawk -> 6x ESC
- D300 derinlik sensoru -> Pixhawk veya ilgili veri hatti
- A02YYUW sensor grubu -> Pixhawk veya ara kontrol birimi
- Power module / regulator -> Pixhawk power portu

## Dikkat Gerektiren Noktalar

- ESC PWM hatlari tek tek planlanmali.
- Besleme hatti `power module` mantigi ile netlestirilmeli.
- Tum sensorlerin dogrudan Pixhawk'a girip girmeyecegi kesin degil.
