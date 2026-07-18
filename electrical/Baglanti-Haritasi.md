# Baglanti Haritasi

Bkz: [[Elektrik-Sistemi]], [[Jetson-Nano]], [[Pixhawk]], [[Mini-ROV-Kontrol-Yigini]]

> [!info] Bu notun amaci
> Bu sayfa, `ne nereye baglanacak` sorusunun calisma taslagidir.
> Nihai sema ve kablolama karari icin referans sayfadir.

## Ana Arac - Guc

| Kaynak                   | Hedef                    | Hat tipi   | Tahmini seviye   | Amac                        | Durum      |
| ------------------------ | ------------------------ | ---------- | ---------------- | --------------------------- | ---------- |
| Ana 4S LiPo              | 100A sigorta             | Guc        | 14.8V nominal    | Asiri akim korumasi         | Net        |
| 100A sigorta             | Acil stop / guc kesme    | Guc        | 14.8V            | Manuel enerji kesme         | Net        |
| Acil stop                | Hi-Base PDB              | Guc        | 14.8V            | Ana dagitim                 | Net        |
| Hi-Base PDB              | 6x ESC                   | Guc        | Batarya seviyesi | Thruster besleme            | Net        |
| Hi-Base PDB              | 5V/12V regulator         | Guc        | Batarya seviyesi | Kontrol elektronigi besleme | Net        |
| 5V regulator             | Jetson Nano              | Regule guc | 5V               | Gorev bilgisayari besleme   | Net        |
| Power module / regulator | Pixhawk                  | Regule guc | 5V civari        | Otopilot besleme            | Net        |
| Regulator                | Kameralar                | Regule guc | 5V/uygun seviye  | Goruntu birimleri           | Kismen net |
| Regulator                | Sensorler                | Regule guc | 3.3V/5V          | Sensor besleme              | Kismen net |
| PDB / regulator          | Elektromiknatis surucusu | Guc        | 12V/uygun seviye | Mini ROV birakma sistemi    | Kismen net |

## Ana Arac - Kontrol ve Sinyal

| Kaynak | Hedef | Hat tipi | Amac | Durum |
|---|---|---|---|---|
| On kamera | Jetson Nano | Video | Nesne/hedef algilama | Net |
| Alt kamera | Jetson Nano | Video | Hat takibi | Net |
| Jetson Nano | Pixhawk | Veri/komut | Gorev kararini hareket komutuna cevirme | Belirsiz: USB veya UART |
| Pixhawk | 6x ESC | PWM | Thruster kontrolu | Net |
| D300 derinlik sensoru | Pixhawk veya ara denetleyici | I2C | Derinlik ve sicaklik | Kismen net |
| A02YYUW x6 | Pixhawk veya ara denetleyici | UART | Yakin engel algilama | Belirsiz |
| Water leak sistemi | Kontrol katmani | Dijital alarm | Sizinti bildirimi | Kismen net |
| Pixhawk | Yer istasyonu / Jetson | Telemetri | Durum verisi | Kismen net |

## Mini ROV - Guc

| Kaynak | Hedef | Hat tipi | Tahmini seviye | Amac | Durum |
|---|---|---|---|---|---|
| 3S LiPo | Mini sigorta/devre kesici | Guc | 11.1V nominal | Koruma | Net |
| Mini sigorta | Mini PDB | Guc | 11.1V | Dagitim | Net |
| Mini PDB | 4x ESC | Guc | Batarya seviyesi | Motor besleme | Net |
| Mini PDB | MP1584EN step-down | Guc | Batarya seviyesi | 5V uretilmesi | Net |
| Step-down 5V | Pi Zero 2 W | Regule guc | 5V | Video bilgisayari | Net |
| Step-down 5V | Pi Pico | Regule guc | 5V | Motor kontrol karti | Net |
| Step-down 5V | Sensorler | Regule guc | 5V/3.3V | Sizinti/engel algilama | Net |

## Mini ROV - Kontrol ve Video

| Kaynak | Hedef | Hat tipi | Amac | Durum |
|---|---|---|---|---|
| Camera Module 3 Wide | Pi Zero 2 W | CSI kamera | Boru ici goruntu | Net |
| Operator komutu | Ana arac | Veri | Ust seviye komut iletimi | Net |
| Ana arac arayuzu | Pi Pico | UART/veri | Mini ROV kontrol komutu | Net |
| Pi Pico | 4x ESC | PWM | Motor kontrolu | Net |
| Water leak sistemi | Pi Pico | Dijital alarm | Sizinti algilama | Net |
| Ultrasonik sensorler | Pi Pico | UART/dijital | Yakin engel algilama | Kismen net |
| Pi Zero 2 W | Ana arac / ethernet arayuzu | Video/veri | Goruntu aktarimi | Net |

## Kara ve Tether Baglantisi

| Kaynak | Hedef | Hat tipi | Amac | Durum |
|---|---|---|---|---|
| Yer istasyonu | Ana arac | Ethernet/tether | Komut + telemetri + goruntu | Net |
| Ana arac switch | Jetson Nano | Ethernet | Veri/goruntu omurgasi | Net |
| Ana arac switch | Mini ROV hatti | Ethernet | Mini ROV goruntusunu tasima | Net |

## Sema Notlari

- `Net label` kullan: `VBAT_MAIN`, `5V_JETSON`, `PWM_ESC_1`, `UART_MINI_TX`, `LEAK_ALARM`.
- Her konnektoru adlandir: `J_PWR_MAIN`, `J_ESC_1`, `J_TETHER`, `J_MINI_LINK`.
- Belirsiz baglantilari `TODO` notu ile isaretle.

## Dikkat Gerektiren Bosluklar

- `Jetson Nano <-> Pixhawk` baglantisi kesin port secimi bekliyor.
- `A02YYUW x6` icin okuma topolojisi net degil.
- Mini ROV veri ve guc hatlarinin ayni konnektorden mi, ayri konnektorlerden mi gececegi net degil.
