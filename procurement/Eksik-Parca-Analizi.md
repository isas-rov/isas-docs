# Eksik Parca Analizi

Bkz: [[Malzeme-Envanteri]], [[Baglanti-Haritasi]], [[Elektrik-Sistemi]]

> [!summary] Bu notun mantigi
> Buradaki maddeler ikiye ayrilir:
> - Gercekten listede olmayan veya eksik gorunen parcalar
> - Listede olsa bile proje akisini kapatmak icin henuz netlesmemis parcalar

## Hizli Sonuc

> [!warning] Kisa yorum
> Liste guclu ama `tam kapanmis bir satin alma listesi` degil.
> Ana eksik, kartlardan cok `ara baglanti`, `adaptasyon`, `su gecirmez gecis`, `yardimci sarf` ve `olcum/arayuz` tarafinda.

## 1. Kritik Eksikler

### 1.1 XT90 var ama zincir kapanmiyor

Durum:

- `XT90-S Anti Spark` listede var.
- Ama `XT90 sarj kablosu` satiri bos.
- Ana guc hattinda `XT90`, `XT60`, `power module`, `PDB` arasindaki son baglanti zinciri tam kapanmiyor.

Risk:

- Batarya var ama sahada dogru adaptasyon olmadan guc hatti karmasiklasir.
- Sarj ve test duzeni karisir.

Oneri:

- `XT90 erkek/disi yedek set`
- `XT90 -> XT60 adaptasyon kablosu` veya net bir custom harness
- `XT90 sarj kablosu`

### 1.2 Ana arac icin branch sigorta dagitimi eksik

Durum:

- Ana sigorta var.
- Ama Jetson, aydinlatma, elektromiknatis, regulator cikislari gibi alt kollarda ayri koruma elemani listede yok.

Risk:

- Tek noktali arizada tum sistem kapanabilir.
- Yardimci yuklerden biri hata verirse ana hat gereksiz etkilenebilir.

Oneri:

- Hat bazli `inline fuse` veya `blade fuse` dagitimi
- Regulator cikislari icin ayri sigortalama

### 1.3 Ana aracta 6 adet UART sensor icin ara arayuz eksik

Durum:

- `A02YYUW x6` planli.
- Mevcut listede bunlari toplayacak acik bir `yardimci MCU`, `UART cogaltici` veya `USB-UART hub` yok.

Risk:

- Sensorler fiziksel olarak var olsa bile okuma mimarisi kapanmaz.

Oneri:

- Yardimci mikrodenetleyici
- USB-UART donusturucu/hub
- Alternatif sensor topolojisi karari

### 1.4 Mini ROV batarya olcumu icin acik donanim eksigi var

Durum:

- Arayuzde Mini ROV batarya durumu gosterilmek isteniyor.
- Ama Mini ROV tarafinda bunun icin net bir `voltage divider`, `telemetry/current sensor`, `ADC olcum devresi` listede acik degil.

Risk:

- Arayuzde batarya gostergesi yazilimsel varsayim olarak kalir.

Oneri:

- Mini ROV batarya gerilim olcumu icin voltaj bolucu veya telemetry modulu

### 1.5 Su gecirmez ethernet/hat sonlandirma tarafi eksik veya kapali degil

Durum:

- Ethernet switch, Hicom kablolari ve USB ethernet adaptoru var.
- Ama `waterproof RJ45 bulkhead`, `ethernet sonlandirma setleri`, `patch kablolari`, `crimp/sonlandirma plani` listede net degil.

Risk:

- Haberlesme omurgasi kagit ustunde var gorunur ama pratik montaj kapanmaz.

Oneri:

- Su gecirmez ethernet gecis cozumu
- Ic patch kablolar
- RJ45 sonlandirma/konnektor setleri

## 2. Yuksek Riskli Belirsizlikler

### 2.1 Jetson - Pixhawk haberlesme sekli net degil

Durum:

- USB ile de yapilabilir, UART/TELEM ile de.
- Malzeme listesi bunu kesin kapatmiyor.

Gereken karar:

- `USB` mi?
- `TELEM UART` mi?

### 2.2 Mini ROV ana gucu hangi senaryoya gore kurulacak

Durum:

- Belgede kendi bataryasindan veya ana aractan besleme opsiyonu geciyor.
- Listede kendi bataryasi var, yani esas senaryo o gibi duruyor.

Risk:

- Kablo ve konnektor secimi bu karara gore degisir.

### 2.3 Mini ROV ana baglanti konnektoru pin sayisi riskli

Durum:

- 6 pin su gecirmez konnektor listede var.
- Ama Mini ROV tarafinda `guc + ortak GND + komut + video/veri + belki ek sinyal` ihtiyaci olabilir.

Risk:

- Tek konnektor pin sayisi yetmeyebilir veya cok zorlayici olur.

Oneri:

- Mini ROV baglantisini `guc` ve `veri` olarak iki konnektore ayirma secenegi degerlendirilmeli.

### 2.4 Elektromiknatis surucu adedi asiri veya dagitimi belirsiz

Durum:

- Elektromiknatis 1 adet.
- MOSFET surucu 4 adet listelenmis.

Yorum:

- Fazla stok olabilir ama gorev mantigina gore gereksiz maliyet de olabilir.

## 3. Yardimci Montaj ve Sarf Eksikleri

Bu grup listede dogrudan gorunmuyor ama pratikte cok lazim olur:

- Isi ile daralan makaron
- Kablo orgusu veya spiral kablo toparlama
- Kelepce / zip tie
- Lehim
- Flux
- Lehim pastasi veya lehimleme sarfi
- Krimp pabuclari / ring terminal / fork terminal
- Ferrul uclari
- Kablo etiketleme
- Cift tarafli endustriyel bant veya kart standoff setleri
- Vidali PCB ayaklari / plastik spacer
- Vibrasyon yalitim pedi

## 4. Yuzey Istasyonu Tarafinda Muhtemel Eksikler

Sistem mimarisinde var ama malzeme listesinde acik olmayanlar:

- Joystick veya gamepad
- Yedek USB kablolari
- Pixhawk programlama/veri kablosu
- Jetson ilk kurulum icin monitor/klavye/mouse erisimi

Not:

- Bunlar takimda mevcut olabilir; yine de `proje BOM` mantiginda acik yazilmamis.

## 5. Satin Alma Onceligi

### A. Once netlestir

- Jetson <-> Pixhawk baglantisi
- A02YYUW okuma mimarisi
- Mini ROV ana besleme senaryosu
- Mini ROV tek/iki konnektor karari

### B. Hemen eklenmesi gerekenler

- XT90 sarj ve adaptasyon kablolari
- Hat bazli ek sigortalar
- Ethernet sonlandirma / su gecirmez gecis parcalari
- Mini ROV batarya olcum cozumleri
- Montaj sarflari

### C. Adet revizyonu gerekenler

- MOSFET modulu
- Su gecirmez konnektor adedi ve pin plani
- Ic patch kablo sayisi

## Son Yorum

> [!tip] En onemli gozlem
> Projenin buyuk parcalari listede var.
> Eksik kalan kisim, sistemi gercekten calisir hale getiren `ara parcalar ve saha montaj detaylari`.
