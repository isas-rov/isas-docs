# Elektrik Sistemi

Bkz: [[Baglanti-Haritasi]], [[Guc-ve-Haberlesme-Altyapisi]], [[Jetson-Nano]], [[Pixhawk]], [[Mini-ROV-Kontrol-Yigini]]

> [!summary] Elektrik mimarisinin ozeti
> Ana mantik, motor guc dagitimini ve hassas kontrol/sensor/video hatlarini birbirinden ayirmaktir.

## Tasarimin Ana Prensibi

Elektrik mimarisi iki ana hatta ayrilir:

1. Yuksek akim itki/guc hatti
2. Dusuk gerilim kontrol/sensor/video hatti

Bu ayrimin amaci:

- Elektriksel gurultuyu azaltmak
- Gerilim dusumunu azaltmak
- Kablo karmasasini azaltmak
- Bakimi kolaylastirmak
- Hata izolasyonunu iyilestirmek

## Ana Arac Elektrik Mantigi

Temel guc zinciri:

`Ana batarya -> ana sigorta -> acil stop/guc kesme -> PDB -> ESC grubu + regulatorler + kontrol birimleri`

Alt dagilim:

- `VBAT` seviyesi: ESC, elektromiknatis surucusu, bazi yukler
- `5V/12V regule hatlar`: Jetson, Pixhawk, kameralar, sensorler, aydinlatma

## Mini ROV Elektrik Mantigi

Temel guc zinciri:

`Mini ROV bataryasi -> mini sigorta/devre kesici -> Mini PDB -> ESC + step-down + kontrol birimleri`

Alt dagilim:

- `11.1V/3S`: motor guc hatti
- `5V`: Pi Zero 2 W, Pi Pico, sensorler

## Kontrol Birimleri

- [[Jetson-Nano]]: gorev bilgisayari
- [[Pixhawk]]: hareket kontrol ve PWM
- [[Mini-ROV-Kontrol-Yigini]]: Pi Zero 2 W + Pi Pico

## Sensor ve Kamera Mantigi

- On kamera, nesne/hedef algilama icin ana aracta kullanilir.
- Alt kamera, hat takibi icin ana aracta kullanilir.
- D300 derinlik sensoru ana aracta derinlik bilgisi saglar.
- A02YYUW sensorleri yakin engel algilama icin planlanmistir.
- Mini ROV kamera modulu boru ici canli goruntu icin kullanilir.
- Water Level sizinti algilama mantigi icin kullanilir.

## Haberlesme ve Video

- Kara baglantisi kabloludur.
- Ana arac uzerinde ethernet/switch mantigi vardir.
- Mini ROV sinyali ana arac uzerinden karaya tasinir.

## Guvenlik Katmani

Elektrik guvenligi icin temel bilesenler:

- Ana sigorta
- Mini ROV sigortasi
- Acil stop
- Ortak GND referansi
- Sizinti algilama
- Dusuk voltaj takibi
- Elektromiknatis surucusu icin diyot korumasi
- PWM failsafe

## Cizim Acisindan Sayfa Bolme Onerisi

Bu projeyi asagidaki sayfalara bolmek mantikli olur:

1. Sistem blok diyagrami
2. Ana arac guc dagitimi
3. Ana arac kontrol ve sinyal hatlari
4. Mini ROV guc dagitimi
5. Mini ROV kontrol ve video hatlari
6. Tether/ethernet ve yer istasyonu baglantilari
7. Pinout ve konnektor tablolari

## Satin Alma ve Uygulama Riski

> [!warning] Sadece ana kartlari almak yetmez
> Bu sistemde baglanti donanimi, branch sigortalama, adaptasyon kablolari ve su gecirmez gecis elemanlari da kritik onemdedir.
> Detayli kontrol icin [[Eksik-Parca-Analizi]] notuna bak.
