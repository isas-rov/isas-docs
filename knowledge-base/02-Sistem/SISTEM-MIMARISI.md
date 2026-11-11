---
title: "SISTEM-MIMARISI"
created: 2026-11-09
updated: 2026-11-09
status: taslak
category: sistem
tags: [isas, umman, rov]
---

# Ana sistem mimarisi

**Belgesel temel:** 2026 KTR, TYF ve güncel BOM; **öneri:** sekiz iticili gövde ve VO tabanlı kör uçuş.

```mermaid
flowchart LR
  subgraph SUR[Karadaki yer istasyonu]
    OP[Operatör ve USB kumanda] --> PC[Kontrol bilgisayarı / QGroundControl]
  end
  PC <-->|Tether / uygun görev aşamasında kablolu veri| HI[Sublink / Hi-com iletişim]
  subgraph ANA[Ana ROV]
    HI <--> J[Jetson Nano 4GB]
    J <-->|MAVLink: UART/USB| PX[Pixhawk 4 / model teyidi]
    PX -->|PWM: 6 mevcut / 8 öneri| ESC[ESC katı]
    ESC --> THR[İticiler]
    BR[Bar30 derinlik] -->|I2C| PX
    CAM1[IMX219 ön kamera] --> J
    CAM2[OV2710 alt USB kamera] --> J
    BAT[4S LiPo] --> PDB[Ana PDB + sigortalar + regülatörler]
    PDB --> ESC
    PDB --> PX
    PDB --> J
  end
  J <-->|ana araç üzerinden komut ve video| MINI[Mini ROV Pi Zero 2 W + Pico]
```

**Elektriksel şema değil:** konektör pinleri, gerilim ve akım değerleri üretici parça numaraları ile doğrulanmadan bağlanmaz. [ELEKTRIK-ANA-SEMA](../03-Elektronik/ELEKTRIK-ANA-SEMA.md).

## Veri yolları
1. **Ana görev:** Jetson; ön/alt kamera, görsel işleme, görev durumu ve navigasyon.
2. **Alt kontrol:** Pixhawk/ArduSub; IMU, derinlik, motor karıştırma ve motor sinyalleri.
3. **Mini ROV:** Pi Zero 2 W CSI video; Pico gerçek zamanlı ESC/sızıntı kontrolü. Haberleşmenin fiziksel ara birimleri ve dönüş kablosu teyit edilmelidir.
4. **Güç:** ana 4S batarya → ana sigorta/kesici → PDB → ayrı ESC ve regülatör kolları; Mini 3S batarya → Mini PDB → 4 ESC ve 5V regülatör.

## Görev bağımlılıkları
Kamera zemini görmüyorsa görsel odometri zayıflar; pusula motor akımından etkilenebilir; bu durumda hedef koordinatlı kör uçuşun doğruluğu garanti edilemez. [KOR-UCUS-MIMARISI](../04-Yazilim/KOR-UCUS-MIMARISI.md).
