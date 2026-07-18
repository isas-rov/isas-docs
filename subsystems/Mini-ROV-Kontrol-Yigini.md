# Mini ROV Kontrol Yigini

Bkz: [[Guc-ve-Haberlesme-Altyapisi]], [[Kamera-ve-Sensorler]], [[Baglanti-Haritasi]]

## Yapi

Mini ROV tarafinda kontrol iki ayri karta bolunmustur:

1. Raspberry Pi Zero 2 W
2. Raspberry Pi Pico

## Neden Iki Kart Var

Belgelerde aciklandigi gibi, video aktarimi ile gercek zamanli motor kontrolu ayni islemciye yuklenirse gecikme ve kararsizlik riski olusur.

Bu yuzden:

- `Pi Zero 2 W`: kamera ve video aktarimi
- `Pi Pico`: PWM, guvenlik ve hizli kontrol

## Pi Zero 2 W'nin Gorevi

- Camera Module 3 Wide ile kamera calistirma
- Goruntuyu ana araca / su ustune aktarma
- Video aktarim katmani olarak calisma

## Pi Pico'nun Gorevi

- UART komutu alma
- 4 adet ESC'ye PWM gonderme
- Sizinti algilama
- Ultrasonik veri okuma
- Haberlesme timeout kontrolu
- Failsafe durumunda motorlari notrleme

## Guc Yapisi

- Mini PDB, Mini ROV ana dagitim merkezidir.
- Step-down regulator ile 5V uretilir.
- Pi Zero 2 W ve Pi Pico bu 5V hattan beslenir.

## Failsafe Mantigi

- Paket gecersizse motorlar notr
- Haberlesme zaman asiminda motorlar notr
- Sizinti varsa alarm/failsafe
- Kritik sensor ihlalinde motor komutlari kesilir

## Acik Karar Noktalari

- Mini ROV'un varsayilan beslemesi `kendi bataryasi` mi olacak, `ana aractan besleme opsiyonu` ana plana dahil mi olacak?
- Ultrasonik sensor sayisi ve veri toplama yontemi net degil.
