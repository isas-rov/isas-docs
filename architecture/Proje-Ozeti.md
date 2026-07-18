# Proje Ozeti

Bkz: [[Sistem-Mimarisi]], [[Elektrik-Sistemi]], [[Malzeme-Envanteri]]

> [!info] Tek cumlelik tanim
> Bu proje, ana arac ile Mini ROV'un gorev paylastigi hibrit bir su alti gorev sistemidir.

## Projenin Ana Fikri

CELEBI-UMMAN sistemi, TEKNOFEST 2026 Insansiz Su Alti Sistemleri Yarismasi icin tasarlanmis hibrit bir su alti gorev sistemidir.

Sistem 3 ana parcadan olusur:

1. Ana Arac
2. Mini ROV
3. Su Ustu Kontrol Istasyonu

## Gorev Mantigi

- Ana arac, otonom hat takibi ve gorev bolgesine intikal icin kullanilir.
- Mini ROV, kapali alan veya boru ici inceleme gorevinde ayrilip manuel olarak kullanilir.
- Su ustu kontrol istasyonu, operatore goruntu, telemetri, alarm ve manuel kontrol arayuzu saglar.

## Ana Aracin Gorevi

- Otonom hat takibi
- Nesne ve hedef bolge algilama
- Intikal ve manevra
- Mini ROV'u tasima ve birakma
- Kara ile veri/goruntu/telemetri aktarimi

## Mini ROV'un Gorevi

- Kapali alan incelemesi
- Operatore canli goruntu aktarma
- Dar alanda 4 motorlu manuel hareket
- Sizinti ve haberlesme kaybinda failsafe uygulama

## Hesaplama ve Kontrol Dagilimi

- `Jetson Nano`: goruntu isleme, gorev mantigi, ust seviye karar
- `Pixhawk`: dusuk seviye hareket kontrolu, stabilizasyon, PWM cikisi
- `Raspberry Pi Zero 2 W`: Mini ROV kamera ve video aktarimi
- `Raspberry Pi Pico`: Mini ROV motor PWM ve guvenlik denetimi

## Elektrik Tasariminin Cekirdek Mantigi

- Yuksek akim tasiyan motor/ESC hatlari ayri dusunulur.
- Dusuk gerilimli islemci, sensor, kamera ve haberlesme hatlari ayri dusunulur.
- Ortak toprak referansi korunur.
- Sigorta, acil stop ve sizinti algilama temel guvenlik katmanlaridir.

## Bu Ozetin Satin Alma Acisindan Anlami

- En kritik satinalma grubu `guc dagitimi + kontrol kartlari + su gecirmez baglanti` tarafidir.
- Liste tamamlansa bile `yardimci sarflar`, `adaptasyon kablolari` ve `konnektor eslesmeleri` ayrica kontrol edilmelidir.
- Bunun icin [[Eksik-Parca-Analizi]] notunu esas al.

## Bu Notun Semadaki Karsiligi

- Sistem seviyesi cizim icin: [[Sistem-Mimarisi]]
- Elektrik semasi mantigi icin: [[Elektrik-Sistemi]]
- Net baglanti listesi icin: [[Baglanti-Haritasi]]
