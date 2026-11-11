---
title: "BAGLANTI-TABLOSU"
created: 2026-11-09
updated: 2026-11-09
status: taslak
category: elektronik
tags: [isas, umman, rov]
---

# Bağlantı, kablo ve pin doğrulama tablosu

**Pin numaraları kasıtlı olarak boş bırakıldı.** Tam kart modeli, konektör revizyonu ve kablo üretici dokümanı olmadan pin uydurmak kısa devre ve ekipman hasarına yol açar.

| Kaynak | Hedef | Veri/enerji | İşlev | Durum | Belirlenecek |
|---|---|---|---|---|---|
| 4S ana batarya | sigorta / ana güç kesici | VBAT/GND yüksek akım | ana güç | BELGEDE | konektör, polarite, kesit, sigorta |
| ana güç kesici | ana PDB | VBAT/GND | dağıtım | BELGEDE | panel/su sızdırmazlık ve ölçüm |
| Ana PDB | 8 ana ESC | VBAT/GND yüksek akım | itki | 8 adet ONERI | her ESC sürekli/tepe akım |
| Pixhawk | 8 ana ESC | PWM/GND | motor kontrolü | 8 adet ONERI | gerçek çıkış portu, nötr, protokol |
| Ana PDB | Jetson buck | batarya | 5V regüle | BELGEDE | giriş/çıkış akımı, filtre, voltaj |
| Buck | Jetson Nano | 5V/GND | bilgisayar | BELGEDE | taşıyıcı kart giriş yöntemi |
| Uygun power module | Pixhawk | güç/sensör | otopilot | TASARIM | kesin model ve pinout |
| Bar30 | Pixhawk I2C | SDA/SCL, güç, GND | derinlik | BELGEDE | JST GH vs DF13, 3.3V lojik |
| IMX219 | Jetson CSI | şerit kablo | ön görüş | BELGEDE | CSI port ve soket yönü |
| OV2710 | Jetson USB | USB video | alt görüş | BELGEDE | fiziksel USB sığma + EMI |
| Jetson | Pixhawk | MAVLink USB/UART | yüksek/alt kontrol | BELGEDE | link seçimi, baud, level shifting |
| Jetson | Sublink/Hi-com | Ethernet/USB | tether ağ | BELGEDE | gerçek modül uyumu |
| Mini ROV | Ana ROV | korumalı veri kablosu | Mini video + komut | BELGEDE | iletim standardı ve su altı konnektör |
| Ana PDB | LED sürücü | uygun DC | aydınlatma | BELGEDE | sürücü/termal |
| Mini 3S | Mini PDB | 3S güç | mini dağıtım | BELGEDE | XT60, sigorta, BMS yok LiPo |
| Mini PDB | 4 Mini ESC | 3S | mini itki | BELGEDE | ESC gerçek pinout |
| Pi Zero 2 W | Pi Pico | UART | Mini PWM komutları | BELGEDE | TTL lojik ve CRC tasarımı |

## Netlist değişiklik yönetimi
- `REV-A`: 2026 6-ESC ana araç tasarım, KiCad dosyası görülmedi.
- `REV-B`: 2027 adayı 8 ESC; yalnız blok şema mevcut.
- Çizimi tamamlayınca `.kicad_sch`, BOM, pin-table CSV, ERC raporu ve kart/konnektör fotoğrafları bu kasaya bağlanmalı.
