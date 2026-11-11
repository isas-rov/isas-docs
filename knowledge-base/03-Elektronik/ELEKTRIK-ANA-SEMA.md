---
title: "ELEKTRIK-ANA-SEMA"
created: 2026-11-09
updated: 2026-11-09
status: taslak
category: elektronik
tags: [isas, umman, rov]
---

# Ana araç elektrik mimarisi — kavramsal şema

> **ÖNEMLİ:** Bu dosya **fabrikasyona hazır KiCad elektrik şeması değildir**. Motorların, regulatorların, konnektörlerin gerçek pin numaraları mevcut kaynaklardan kesinleştirilemez. Şema, hata/eksik kontrolü için işlevsel topolojidir; enerjileme öncesi KiCad/ERC/DRC, kablo kesiti, sigorta ve üretici pinout doğrulaması şart.

```mermaid
flowchart TD
  BAT[4S 14.8V nominal LiPo] --> FUSE[Ana sigorta - boyutu hesaplanacak]
  FUSE --> KILL[Ana güç kesici / E-Stop mimarisi]
  KILL --> PDB[8 ESC'ye uyarlanacak Ana PDB]
  PDB --> E1[ESC1 + motor1]
  PDB --> E2[ESC2 + motor2]
  PDB --> EN[ESC3..ESC8 + motor3..8 / tasarım]
  PDB --> BJ[Jetson için bağımsız 5V buck]
  PDB --> BP[Pixhawk için uygun power module / korumalı besleme]
  PDB --> BA[5V sensör/yardımcı buck]
  BJ --> JET[Jetson Nano]
  BP --> PX[Pixhawk]
  BA --> AUX[LED/sensör kontrol katları]
  PX -.->|8 kontrol kanalı PWM/supported protocol| E1
  PX -.-> E2
  PX -.-> EN
  JET <-->|USB/UART MAVLink| PX
  BAR[Bar30 I2C] --> PX
  CAM1[IMX219 CSI] --> JET
  CAM2[OV2710 USB] --> JET
  LEAK[Leak probe] -->|güvenlik kontrolcüsü / tanımlanacak| PX
```

## Net sınıfları
- `VBAT_MAIN` — batarya artı hattı; ana sigorta ve anahtar sonrası dağıtım.
- `GND_MAIN` — güç dönüş hattı; sinyal referansları kontrollü bağlanacak; yıldız topraklama her durumda tek çözüm sayılmaz.
- `5V_JETSON` — Jetson Nano'nun modül/taşıyıcı girişine uygun gerilim ve akım; 3A LM2596 üzerine kör bağlamayın.
- `5V_AUTOPILOT` — Pixhawk'a üretici tasarımına göre power-module/porttan besleme.
- `5V_AUX` — sensör/yardımcı; özellikle motor hatlarının anahtarlama gürültüsünden ayırma/filtreleme.
- `PWM_MOT_1...8` — Pixhawk'ın **teyit edilen** çıkışlarından ESC'lere; arayüz pinout üreticiden kontrol edilecek.
- `I2C_BAR30` — kısa 3.3V lojik düzeyi, kablo ve konnektör sürümü dikkat.
- `UART_MAVLINK` — TX-RX çapraz bağlantı, ortak referans ve 3.3V/5V seviyeleri doğrulanmalı.

## Kablosuz bağlantı yok varsayımı
2026 tam otonom görevinde yüzeyden canlı görev komutuna dayanılmamalı; tether'ın mekanik emniyet görevi ve kablolu operatör evreleri görev bazında ayrılır.

## Çok önemli eksikler
1. Toplam / tepe akım, sigorta seçimi, PDB iz kalınlığı ve kablo AWG hesapları.
2. ESC'lerin su altında ısı atımı, epoksi uyumluluğu ve sızdırmazlık.
3. Batarya terminali, güç kesicinin açma kapama davranışı ve Mini ROV'a etkisi.
4. Pixhawk 4 ve Pixhawk 2.8 arasında konnektör/port farkları.
5. Harici pusula beslemesi, veri hattı ve manyetik çevre.
6. E-stop donanımının gerçek fail-safe davranışı.

Bak: [BAGLANTI-TABLOSU](BAGLANTI-TABLOSU.md) • [GUC-BATARYA-PDB](GUC-BATARYA-PDB.md) • [EMI-PUSULA](EMI-PUSULA.md)
