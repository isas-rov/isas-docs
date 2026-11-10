# Malzeme Envanteri

Bkz: [[Jetson-Nano]], [[Pixhawk]], [[Mini-ROV-Kontrol-Yigini]], [[Guc-ve-Haberlesme-Altyapisi]], [[Kamera-ve-Sensorler]]

Bu notta malzeme listesindeki tum kalemler, alt sistem ve kullanim amacina gore gruplanmistir.

> [!summary] Bu not nasil okunmali
> - Bu sayfa `elde olan veya listelenen` parcayi gosterir.
> - `Eksik veya netlesmemis` parcayi gormek icin [[Eksik-Parca-Analizi]] notuna gec.

## Kontrol

| Malzeme | Adet | Nerede kullaniliyor | Amac | Link |
|---|---:|---|---|---|
| NVIDIA Jetson Nano 4GB | 1 | Ana arac | Goruntu isleme, gorev akisi, kamera yonetimi | https://www.robocombo.com/waveshare-jetson-nano-gelistirme-kiti-kit-a?srsltid=AfmBOorZ_lIJu6BNg9qIiUo3ZZHCPQo0bh8rI6c2RM_fsyoynDH0Te7Crwk |
| Holybro Pixhawk 2.8 | 1 | Ana arac | Otopilot, denge, yonelim, PWM cikisi | https://www.direnc.net/pixhawk-px4-pix-248-32-bit-ucus-kontrol-cihazi-standart-paket |
| Raspberry Pi Zero 2 W | 1 | Mini ROV | Kamera ve video aktarimi | https://www.robotistan.com/raspberry-pi-zero-2-w |
| Raspberry Pi Pico | 1 | Mini ROV | Motor kontrolu, PWM, sizinti ve guvenlik | https://www.robotistan.com/raspberry-pi-pico |

## Itki

| Malzeme                             |  Adet | Nerede kullaniliyor   | Amac                       | Link                                                                  |
| ----------------------------------- | ----: | --------------------- | -------------------------- | --------------------------------------------------------------------- |
| Mucif / Degz Mitras Su Alti Iticisi |     6 | Ana arac              | 6 eksen hareket ve manevra | https://www.mucif.com/urunler/mitras-su-alti-iticisi/                 |
| Mucif / Degz Blu 30A ESC            |     6 | Ana arac              | Mitras thruster surme      | https://www.mucif.com/urunler/degz-blu-30a-esc-fircasiz-motor-surucu/ |
| Degz Blu 30A ESC                    |     4 | Mini ROV              | Mini ROV motor surme       | https://www.mucif.com/urunler/degz-blu-30a-esc-fircasiz-motor-surucu/ |
| M1 Su Gecirmez Su Alti Motoru       |     4 | Mini ROV              | Mini ROV itki              | https://www.mucif.com/urunler/degz-m1-su-gecirmez-su-alti-motoru/     |
| Mitras Yuksek Guclu Pervane         | 2 set | Mini ROV / itki grubu | Pervane/nozul seti         | https://www.mucif.com/urunler/mitras-su-alti-itici-pervane/           |

## Guc

| Malzeme | Adet | Nerede kullaniliyor | Amac | Link |
|---|---:|---|---|---|
| Leopard Power 16000mAh 14.8V 4S LiPo | 1 | Ana arac | Ana guc kaynagi | https://www.oyuncakhobi.com/leopard-power-16000mah-148v-4s-25c-uav-miltirator-batarya?srsltid=AfmBOooxzBLmJo9sYUnT7nXZ2xbYOoW_r7cRHIN4_29N4WNdCNvScR8p |
| Reiss Audio 100A Sigorta Yuvasi | 1 | Ana arac | Ana sigorta | https://www.hepsiburada.com/reiss-audio-100a-sigorta-yuvasi-rs-anl100a-guclu-ses-ve-profesyonel-kullanim-icin-pm-HBC00000UPRQH |
| Degz Hi-Base Hall Effect PDB | 2 | Ana arac | Guc dagitimi ve uzaktan kapatma | https://www.mucif.com/urunler/degz-guc-dagitim-karti-hi-base-hall-effect-sensor/ |
| XT90-S Anti Spark konnektor | 3 | Ana arac | Ana guc baglantisi | https://www.motorobit.com/xt90-s-anti-spark-erkek-disi-konnektor-takimi |
| 12 AWG silikon kablo | 3 m | Ana arac | Yuksek akim guc kablosu | https://www.robotistan.com/12-awg-1-metre-siyah-ve-kirmizi-silikon-kablo |
| 18 AWG silikon kablo | 6 m | Genel | Dusuk/orta akim hatlari | https://www.mucif.com/urunler/18-awg-cok-telli-silikon-esnek-kablo/ |
| Servo uzatma kablosu | 8 | Kontrol hatti | PWM/sinyal uzatma | https://www.motorobit.com/servo-uzatma-kablosu-15-cm-disi-erkek |
| DF-13 APM/Pixhawk kablosu | 2 | Ana arac | Pixhawk baglanti kablosu | https://www.f1depo.com/urun/df-13-apm-pixhawk-px4-kablosu-6-pin-konnektor-6p-df13 |
| DC Barrel Jack Male | 2 | Yardimci guc | Guc/deneme baglantisi | https://www.robotistan.com/erkek-kablo-tipi-power-soketi-dc-barrel-jack-male |
| Pololu 5V 15A regulator | 1 | Ana arac | Jetson gibi 5V yukler icin | https://www.robotistan.com/pololu-5v-15a-step-down-voltage-regulator-d24v150f5 |
| 5V 12V Gerilim Regulatoru | 2 | Ana arac | Yardimci besleme | https://www.mucif.com/urunler/5v-12v-gerilim-regulatoru/ |
| Lipo seviye olcer ve alarm | 1 | Genel | Dusuk voltaj uyarisi | https://www.motorobit.com/lipo-seviye-olcer-ve-alarm-modulu?srsltid=AfmBOooXgVSzjRdAHbuT9Kgic2_hoRjW6V2NYmPDjKZOZFQVQS1gRTU4 |
| 30V 90A power module | 1 | Ana arac / Pixhawk | Guc olcumu ve duzenli besleme | https://www.robotistan.com/30-v-90-a-power-module-53v-dc-bec-xt60-socket1 |
| Acil stop butonu | 1 | Su ustu/ana guc | Manuel enerji kesme | https://www.kartalotomasyon.com.tr/urun/b200e-e-40mm-emergency-etiketli-mantar-acil-stop-butonu-nc |
| XT60 soket takim | 10 | Genel | Batarya/guc baglantilari | https://www.voltaj.net/xt60-li-po-pil-erkek-disi-soket-takim-konnektor-pmu1286 |
| XT30 soket seti | 10 | Genel | Yardimci guc baglantilari | https://www.robotistan.com/xt30-erkek-disi-soket-seti?language=tr&h=c75d49be |
| 4 kanal lojik seviye donusturucu | 1 | Kontrol/sensor | 3.3V-5V seviye uyumu | https://www.hepsiburada.com/4-kanal-2-yonlu-lojik-seviye-donusturucu-5v-3-3v-sinyal-uygunlastirici-p-HBCV00007EU6I1?magaza=Devremarkt |
| PROFUSE 11.1V 3S 5000mAh LiPo | 1 | Mini ROV | Mini ROV ana bataryasi | https://www.motorobit.com/111v-3s-5000mah-65c-lipo-batarya?srsltid=AfmBOorW3dsb_ItS5XYO7OWe1rTfb2REZ9Z6_yApwlWcDHoX8MJJTSQK |
| Matek PDB-XT60 w/ BEC | 1 | Mini ROV | Mini ROV guc dagitimi | https://www.motorobit.com/matek-pdb-xt60-w-bec-5v-12v-esc-power-distribution?srsltid=AfmBOoootdGEzeqTXsgpsN6Dxi6dQM84caGUuLUdiP_ShRpEGvKdlJ3s |
| MP1584EN step-down regulator | 1 | Mini ROV | Pi Zero/Pico 5V besleme | https://www.motorobit.com/3a-mini-adjustable-voltage-step-down-regulator-board?srsltid=AfmBOorXD-unRJDb7mCC-eqWSNXyjj5LB89DkMx3QBEVV-KuAXikYVXG |
| 5V 12V Gerilim Regulatoru | 1 | Mini ROV | Yardimci besleme | https://www.mucif.com/urunler/5v-12v-gerilim-regulatoru/ |
| Mini ROV 50A sigorta/devre kesici | 1 | Mini ROV | Ana koruma | https://www.motorobit.com/50a-oto-anfi-sigorta-kutusu-devre-kesici |
| Mini ayarlanabilir 3A regulator | 1 | Yardimci hat | Ek step-down | https://www.robotistan.com/3a-mini-ayarlanabilir-voltaj-dusurucu-regulator-karti-step-down |

## Sensor

| Malzeme | Adet | Nerede kullaniliyor | Amac | Link |
|---|---:|---|---|---|
| A02YYUW Ultrasonik Sensor | 6 | Ana arac | Yakin engel algilama | https://www.direnc.net/a02yyuw-su-gecirmez-ultrasonik-sensor |
| D300 Derinlik ve Su Sicakligi Sensoru | 1 | Ana arac | Derinlik ve su sicakligi | https://www.mucif.com/urunler/d300-derinlik-ve-su-sicakligi-sensoru/ |

## Guvenlik

| Malzeme | Adet | Nerede kullaniliyor | Amac | Link |
|---|---:|---|---|---|
| Water Level | 2 | Ana arac + Mini ROV | Sizinti algilama | https://www.robotistan.com/su-seviyesi-yagmur-sensoru-water-level-rain-sensor |
| 1N5408 1000V 3A diyot | 10 | Birakma sistemi | Flyback / koruma diyodu | https://www.motorobit.com/1n5408-1000v-3a-diyot?srsltid=AfmBOoqJ2S_7NaYl1vhZ2dAShrPKmrtK7r_RTExlh1pjfdqQQR6ZSQbO |

## Baglanti

| Malzeme | Adet | Nerede kullaniliyor | Amac | Link |
|---|---:|---|---|---|
| 6 pin duz su gecirmez konnektor | 1 | Mini ROV | Sizdirmaz baglanti noktasi | https://www.direnc.net/6pin-duz-su-gecirmez-konnektor-takim |
| Pin duz su gecirmez konnektor takim | 4 | Genel | Dis ortam baglantisi | https://www.direnc.net/4pin-duz-su-gecirmez-konnektor-takim |
| Neo kablo rakoru / penetrator | 24 | Hazneler | Sizdirmaz kablo gecisi | https://www.mucif.com/urunler/degz-neo-kablo-rakoru-penetrator/ |

## Goruntu ve Haberlesme

| Malzeme | Adet | Nerede kullaniliyor | Amac | Link |
|---|---:|---|---|---|
| Raspberry Pi Camera Module 3 Wide | 1 | Mini ROV | Boru ici canli goruntu | https://www.robotistan.com/raspberry-pi-3-wide-camera |
| IMX219-77 Kamera | 1 | Ana arac | On gorus / hedef algilama | https://www.robotistan.com/imx219-77-camera-for-jetson-nano |
| IMX335 USB Kamera | 1 | Ana arac | Alt gorus / hat takibi | https://www.robotistan.com/imx335-tak-calistir-usb-kamera-a |
| Sublink Hi-com modulu | 1 | Haberlesme | Yuksek hizli iletisim | https://www.mucif.com/urunler/sublink-hi-com-yuksek-hizli-iletisim-modulu/ |
| Sublink Hi-com USB modulu | 1 | Haberlesme | USB tabanli yuksek hizli iletisim | https://www.mucif.com/urunler/sublink-hi-com-usb-yuksek-hizli-iletisim-modulu/ |
| Mini ethernet switch | 1 | Ana arac | Kara + Jetson + Mini ROV ag toplama | https://www.hepsiburada.com/tp-link-tl-sf1005d-5-port-10-100mbps-ehternet-switch-p-BD999568 |
| Hicom 2 ethernet kablosu | 50 m | Kara <-> Ana arac | Tether / veri omurgasi | https://www.mucif.com/urunler/hicom-2-ethernet-iletisim-kablosu-twisted-pair-poliuretan-yuzer-kablo/ |
| Hicom 8 ethernet kablosu | 10 m | Mini ROV <-> Ana arac | Mini ROV veri hatti | https://www.mucif.com/urunler/hicom-8-ethernet-iletisim-kablosu-twisted-pair-poliuretan-yuzer-kablo-cat-5/ |
| USB OTG + USB ethernet adaptor | 1 | Mini ROV / Pi Zero | USB tabanli ethernet | - |
| Raspberry Pi camera cable mini 200mm | 1 | Mini ROV | Kamera kablosu | https://www.robotistan.com/raspberry-pi-camera-cable-standard-mini-200mm-en |
| Raspberry Pi FFC camera cable 0.3m | 1 | Kamera | FFC uzatma | https://www.robotistan.com/30-cm-raspberry-pi-kamera-kablosu-ffc-15-pin-4b-3b-3b-3a-uyumlu |
| Raspberry Pi FFC camera cable 0.15m | 1 | Kamera | FFC uzatma | https://www.robotistan.com/raspberry-4b/3b/3b/3a-camera-ffc-15pin-cable-no-support-zero/zero-w-0 |
| Pi Zero uyumlu PoE Ethernet/USB Hub HAT | 1 | Mini ROV | Ethernet/USB genisleme | https://www.robocombo.com/waveshare-pi-zero-uyumlu-poe-ethernetusb-hub-hat-4672?srsltid=AfmBOoq1RUNFcp0vaS5Et3xMypILe0aQHe00B7kvnilqn6gWMKojSOmr |
| Pi Zero GPIO Header | 2 | Mini ROV | GPIO lehimleme / baglanti | https://www.robotistan.com/odseven-raspberry-pi-2x20-double-row-pin-male-colour-coded-gpio-header-for-pi-zero |
| Micro SD kart | 1 | Pi Zero / Jetson | Depolama | https://www.trendyol.com/sandisk/ultra-64-gb-100-mb-s-uhs-i-class-10-sdsqunr-064g-gn3mn-micro-sd-kart-p-52184396 |

## Birakma Sistemi

| Malzeme | Adet | Nerede kullaniliyor | Amac | Link |
|---|---:|---|---|---|
| P40/20 12V DC Electromagnet | 1 | Ana arac alti | Mini ROV tut-birak | https://www.robotistan.com/p40-20-12v-dc-electromagnet-30kg-attraction-force |
| D4184 Mosfet control module | 4 | Birakma sistemi | Elektromiknatis surucusu | https://www.robotistan.com/d4184-mosfet-kontrol-modulu |

## Aydinlatma

| Malzeme | Adet | Nerede kullaniliyor | Amac | Link |
|---|---:|---|---|---|
| Labarka su alti lambasi 39 LED | 2 | Ana arac | Kamera gorusunu destekleme | https://www.hepsiburada.com/labarka-su-alti-lambasi-39-led-li-12-24v-beyaz-pm-HBC00006BZ9HL |
| Panter IPX8 su alti feneri | - | Opsiyonel | Yardimci aydinlatma | https://www.trendyol.com/panther/pt-4980-ipx8-led-su-alti-feneri-siyah-p-857382305 |

## Test, Sarj ve Operasyon Destegi

| Malzeme | Adet | Nerede kullaniliyor | Amac | Link |
|---|---:|---|---|---|
| iMAX B6AC sarj cihazi | 1 | Operasyon | LiPo sarj/balans | https://www.robotistan.com/imax-b6ac-adaptorlu-profesyonel-li-po-ni-mh-sarj-aleti-balancer-50w-51 |
| 4mm Banana - XT60 kablo | 2 | Sarj | Sarj adaptoru | https://www.robotronik.com.tr/4mm-banana---erkek-xt60-donusturucu-30cm-kablo-a0979 |
| Lipo safe bag | 1 | Guvenlik | Batarya saklama | https://www.robotistan.com/lipo-saklama-cantasi-22x18x4cm |
| 4mm Banana - XT90 sarj kablosu | - | Sarj | XT90 sarj baglantisi | - |

## Mekanik, Sizdirmazlik ve Uretim

| Malzeme | Adet | Nerede kullaniliyor | Amac | Link |
|---|---:|---|---|---|
| PETG Filament | 13 | Govde/sase | 3B baski uretim | https://3dcim.com/petg-filament-cesitleri?srsltid=AfmBOorMEfb6KtmaClSd1KvoGYYo-wR90HbHGaCL_cYoa-jYo4TPCnZa |
| H-100 Su Alti Haznesi | 1 | Ana arac | Elektronik hazne | https://www.mucif.com/urunler/h-100-su-alti-haznesi/ |
| H-60 Su Alti Haznesi | 1 | Mini ROV | Kompakt elektronik hazne | https://www.mucif.com/urunler/h-60-sualti-haznesi/ |
| Sertlestirilmis polikarbonat optik kubbe | 1 | Ana arac | Kamera gorus kubbesi | https://www.letnamarine.com/sualti-kamera-kubbesi |
| Epoksi siringa yapistirici | 2 | Genel | Yapisal yapistirma/sizdirmazlik | https://www.ruzgarlihobi.com/urun/nano-epoksi-siringa-yapistirici-7900-psi-bor-karbur-25-ml?srsltid=AfmBOorEfH6Uay8-yxHvSTneUwH7wSFqtdo7W3K2NsqXB2udqLUsnhf9 |
| Plastik kaynak zimba teli | 1 | Govde onarim | Plastik guclendirme | https://bemoold.com.tr/100-adet-0-8mm-dalgali-tip-plastik-kaynak-zimba-teli?srsltid=AfmBOoorhFviwJDCfnPy7wWCRivFfKo8THXqxJvpAgpkgByubslVMbat |
| Isiya dayanikli sizdirmaz conta | 1 | Genel | O-ring / sizdirmazlik | https://www.robotistan.com/dayanikli-siyah-oring?language=tr&h=98644dae |
| Epoxy son kat boya | 1 | Govde koruma | Kimyasal ve su alti dayanim | https://www.denizmarketi.com/urun/teknomarin-aquapox-epoxy-son-kat-boya-1kg |
| Epoksi vernik | 1 | Govde koruma | Son kat koruma | https://www.denizmarketi.com/urun/tekno-teknopox-epoksi-vernik |
| Arakat boya | 1 | Govde koruma | Katman gecisi | https://www.denizmarketi.com/urun/tekno-teknopox-universal-epoxy-primer-arakat-boya |
| Boya astari | 1 | Govde koruma | Yuzey hazirlik | https://www.denizmarketi.com/urun/tekno-teknopox-primer-boya-astari |
| Yuzdurucu kopuk | 1 | Ana arac + Mini ROV | Trim ve kaldirma kuvveti | https://www.mucif.com/urunler/yuzdurucu-kopuk/ |
| M5 vida somun pul seti | 1 | Montaj | Mekanik baglanti | https://www.robolinkmarket.com/m5-ysb-vida-somun-ve-pul-seti-300-parca?srsltid=AfmBOord0_eIzQRlUdF-S17fDza9Jt99igI6d-yInwyTfZVdBgdHQ2Jj |
| M10 celik civata seti | 1 | Montaj | Ana yapisal baglanti | https://www.robolinkmarket.com/m5-ysb-vida-somun-ve-pul-seti-300-parca?srsltid=AfmBOord0_eIzQRlUdF-S17fDza9Jt99igI6d-yInwyTfZVdBgdHQ2Jj |

## Notlar

- Ayni isimde tekrar eden bazi regulator kalemleri farkli alt sistemlerde kullanilmak uzere listelenmis olabilir.
- Bazi fiyatlar ve bazi destek kalemlerinin adet alanlari listede eksik geciyor.
- En kritik envanter grubu `Kontrol + Itki + Guc + Sensor + Goruntu + Baglanti + Guvenlik` kalemleridir.
