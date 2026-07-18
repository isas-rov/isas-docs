# ISAS - Obsidian Ana Sayfa

Bu bilgi agaci, asagidaki kaynaklar temel alinarak hazirlandi:

- `Umman-Malzeme-Listesi-Guncel.xlsx`
- `KTR-CELEBI-UMMAN.pdf`
- `2026_INSANSIZ_SU_ALTI_SISTEMLERI_...pdf`

> [!summary] Bu kasa ne ise yariyor
> Bu vault, proje mimarisini, elektrik baglantilarini, malzeme envanterini ve eksik parca analizini tek yerde toplar.
> Amac, ekip icinde ortak bir teknik hafiza olusturmaktir.

## Hizli Erisim

- [[Proje-Ozeti]]
- [[Sistem-Mimarisi]]
- [[Jetson Kullanımı]]
- [[00-Jetson-Nano-Kasası]]
- [[Elektrik-Sistemi]]
- [[Baglanti-Haritasi]]
- [[Malzeme-Envanteri]]
- [[Eksik-Parca-Analizi]]
- [[Yarisma-Isterleri]]

## Moduller

- [[Jetson-Nano]]
- [[02-Hızlı-Giriş]]
- [[Pixhawk]]
- [[Mini-ROV-Kontrol-Yigini]]
- [[Guc-ve-Haberlesme-Altyapisi]]
- [[Kamera-ve-Sensorler]]

## Kullanim Sirasi

- Sistem mimarisini anlamak icin once [[Proje-Ozeti]] ve [[Sistem-Mimarisi]] notlarini oku.
- Elektrik semasina baslamadan once [[Elektrik-Sistemi]] ve [[Baglanti-Haritasi]] notlarini kullan.
- Hangi modulu cizecegini belirlemek icin `03-Moduller` klasorundeki notlara bak.
- Parca bazli kontrol icin [[Malzeme-Envanteri]] notunu kullan.
- Satin alma ve teknik acik analizi icin [[Eksik-Parca-Analizi]] notunu kullan.

## Hizli Durum Ozeti

- Sistem, `Ana Arac + Mini ROV + Su Ustu Kontrol Istasyonu` olarak kurgulanmis hibrit bir yapidir.
- Ana arac uzerinde `Jetson Nano + Pixhawk + 6 thruster + 6 ESC + sensorler + kameralar + guc dagitimi` bulunur.
- Mini ROV uzerinde `Pi Zero 2 W + Pi Pico + 4 motor + 4 ESC + kamera + sizinti/engel algilama` bulunur.
- Kara baglantisi kablolu `tether/ethernet` mantigindadir.
- Elektrik tasariminin ana mantigi `yuksek akim itki hatti` ile `dusuk gerilim kontrol/sensor/video hattini` ayirmaktir.

## Ana Karar Notlari

> [!warning] Netlesmesi gereken kritik basliklar
> - `Jetson Nano <-> Pixhawk` haberlesmesinin `USB mi, UART mi` olacagi
> - `A02YYUW x6` sensorlerinin nasil okunacagi
> - Mini ROV'un varsayilan besleme senaryosu
> - XT90, XT60 ve PDB/power module arasindaki guc baglanti zincirinin son hali

## Cozulmesi Gereken Belirsizlikler

- `Jetson Nano <-> Pixhawk` fiziksel baglantisinin `USB mi, UART mi` olacagi kesinlestirilmeli.
- `A02YYUW` ultrasonik sensorlerin 6 adedinin nasil okunacagi netlestirilmeli.
- Mini ROV'un gucunun varsayilan olarak `kendi bataryasindan mi` yoksa `ana aractan mi` beslenecegi semada ana senaryo olarak secilmeli.
