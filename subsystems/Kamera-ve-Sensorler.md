# Kamera ve Sensorler

Bkz: [[Jetson-Nano]], [[Pixhawk]], [[Mini-ROV-Kontrol-Yigini]]

## Ana Arac Kameralari

### On Kamera

Muhtemel parca:

- `IMX219-77 Kamera`

Amaci:

- Samandira, hedef bolge ve gorev nesnesi algilama

Baglantisi:

- On kamera -> Jetson Nano

### Alt Kamera

Muhtemel parca:

- `IMX335 USB Kamera`

Amaci:

- Zemin cizgisi ve yonlendirme tahtasi takibi

Baglantisi:

- Alt kamera -> Jetson Nano

## Mini ROV Kamerasi

Parca:

- `Raspberry Pi Camera Module 3 Wide`

Amaci:

- Boru ici canli goruntu
- Operatorun yazisal/gorsel ipucunu okumasini saglamak

Baglantisi:

- Kamera -> Pi Zero 2 W

## Derinlik Sensoru

Parca:

- `D300 Derinlik ve Su Sicakligi Sensoru`

Amaci:

- Derinlik olcumu
- Depth hold mantigi

Muhtemel baglanti:

- D300 -> Pixhawk veya ilgili kontrol veri hatti

## Yakin Engel Sensorleri

Parca:

- `A02YYUW Ultrasonik Sensor` x6

Amaci:

- Ana arac cevresinde yakin engel algilama

Belirsizlik:

- 6 adet UART sensorun tam baglanti topolojisi belgelerde pin bazinda net degil

## Sizinti Sensorleri

Parca:

- `Water Level` tipi sizinti algilama probu

Amaci:

- Hazneye su girisini algilamak

Muhtemel baglanti:

- Ana arac sizinti algilama -> kontrol sistemi
- Mini ROV sizinti algilama -> Pi Pico

## Dikkat Gerektiren Nokta

> [!warning] Ana arac ultrasonik topolojisi acik degil
> 6 adet UART tabanli A02YYUW sensorun tek basina mevcut kontrol yapisina nasil baglanacagi kesinlestirilmelidir.
