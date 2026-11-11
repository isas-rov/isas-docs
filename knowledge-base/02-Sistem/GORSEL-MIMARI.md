---
title: ÇELEBİ–UMMAN sistem akışları
updated: 2026-11-11
status: taslak
tags: [mimari, sema, isas]
---
# Sistem akışları (kavramsal)

> [!WARNING] Üretim ve pin şeması değil
> Aşağıdaki çizimler **işlevsel blok şemalarıdır**. Bağlantı pini, kablo kesiti, sigorta değeri ve ESC beslemesi doğrulandıktan sonra nihai KiCad şemasına dönüştürülür. [Güncel KiCad kaynakları](https://github.com/isas-rov/isas-hardware/tree/main/electrical/kicad/main-rov) ayrı depodadır.

## Ana araç veri ve güç akışı

```mermaid
flowchart TB
    SURFACE[Su üstü yer istasyonu] <-->|Tether haberleşmesi| LINK[Bağlantı birimi / Switch]
    CAM1[Ön kamera] --> JETSON[Jetson Nano: görev, algılama]
    CAM2[Alt kamera] --> JETSON
    LINK <--> JETSON
    JETSON <-->|MAVLink| PIX[Pixhawk: ArduSub kontrol]
    IMU[IMU, manyetometre] --> PIX
    DEPTH[Basınç / derinlik sensörü] --> PIX
    PIX --> ESC[ESC sürücüleri]
    ESC --> MOTORS[6 motor: 2026 KTR / 8 motor: öneri]
    BAT[Batarya] --> PROTECT[Koruma, kesici, güç dağıtımı]
    PROTECT --> ESC
    PROTECT --> REG[5V, 12V regülatörler]
    REG --> JETSON
    REG --> PIX
```

## Kör uçuşta bilgi zinciri

```mermaid
flowchart LR
    CAM[Alt kamera] --> FLOW[Optical Flow / VO]
    IMU[IMU ve yönelim] --> EST[Durum tahmini]
    DEP[Bar30: basınç derinliği] --> EST
    FLOW --> EST
    EST --> TRACK[Rota kontrolü]
    TARGET[Ön kamera: hedef algılama] --> TRACK
    TRACK --> MAV[MAVLink komutu]
    MAV --> SUB[ArduSub dengeleme ve motor karıştırma]
    SUB --> THR[Thruster]
    EST --> TRUST[Belirsizlik izleme ve güvenlik]
    TRUST --> TRACK
```

**Ana sınırlama:** Bar30, kamera–taban irtifasını vermez; optik akışın metrik ölçeği bundan dolayı her zaman hesaplanamaz. Alt kamera başarısızsa yatay konum kestirimi hızla belirsizleşir. [Ayrıntı](../04-Yazilim/OPTICAL-FLOW-VE-VO.md).

## Mini ROV ilişkisi

```mermaid
flowchart LR
    OP[Operatör] <-->|Video ve kontrol| MAIN[Ana ROV köprüsü]
    MAIN <-->|İletişim hattı| PI[Pi Zero 2 W: kamera/video]
    MAIN <-->|Kontrol hattı| PICO[Pico: PWM ve güvenlik]
    PICO --> ESC4[4 ESC] --> M4[4 motor]
    MINI_BAT[Mini ROV bataryası] --> ESC4
```

**Kontrol:** Mini ROV güç, toprak, haberleşme ve güvenlik kablo/topoloji kararları henüz fiziksel olarak doğrulanmalı. [Mini ROV](MINI-ROV.md).

## İlgili kaynaklar
- [Kavramsal bağlantı listesi](../03-Elektronik/BAGLANTI-TABLOSU.md)
- [Güncel KiCad taslağı](https://github.com/isas-rov/isas-hardware/tree/main/electrical/kicad/main-rov)
- [Görsel kaynak atlası](../98-Gorseller/GORSEL-ATLAS.md)
