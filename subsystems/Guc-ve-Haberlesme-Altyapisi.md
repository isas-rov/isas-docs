# Guc ve Haberlesme Altyapisi

Bkz: [[Elektrik-Sistemi]], [[Baglanti-Haritasi]], [[Malzeme-Envanteri]]

## Ana Arac Guc Altyapisi

Ana parcaciklar:

- 4S LiPo ana batarya
- 100A sigorta
- Acil stop
- Hi-Base PDB
- 5V/12V regulatorler
- Power module

Temel akis:

`Batarya -> Sigorta -> Acil stop -> PDB -> ESC + regulator + kontrol yukleri`

## Mini ROV Guc Altyapisi

Ana parcaciklar:

- 3S LiPo
- Mini sigorta/devre kesici
- Mini PDB
- MP1584EN step-down

Temel akis:

`Mini batarya -> Sigorta -> Mini PDB -> ESC + 5V step-down -> Pi Zero 2 W / Pi Pico / sensorler`

## Tether ve Haberlesme

Belgelerde kara ile haberlesmenin kablolu olmasi gerektigi belirtilmis.

Kullanilan omurga:

- Ana arac <-> kara: ethernet/tether
- Ana arac icinde: mini ethernet switch
- Mini ROV video aktarimi: ana arac uzerinden karaya

## Ortak Toprak

Elektrik tasariminda `ortak GND referansi` kritik.

Neden:

- ESC PWM sinyali referans ister
- Sensor okumalarinin kararliligi icin gerekir
- Farkli regulator cikislari arasinda referans kaybi olmamali

## Guvenlik Bilesenleri

- Sigorta
- Devre kesici
- Acil stop
- Diod korumasi
- Sizinti sensoru
- Dusuk voltaj alarmi

## Sema Cizerken Not

- Guc dagitimini ayri sayfada ciz.
- Ethernet/video tarafini ayri sayfada ciz.
- PDB'yi net merkez olarak konumlandir.
- Her regulator cikisini ayri isimlendir.
