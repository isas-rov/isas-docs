---
title: "YAZILIM-MIMARISI"
created: 2026-11-09
updated: 2026-11-09
status: taslak
category: yazilim
tags: [isas, umman, rov]
---

# Yazılım mimarisi — Jetson + Pixhawk

```mermaid
flowchart TD
  Front[Ön kamera] --> DET[Şamandıra / hedef algılayıcı]
  Bottom[Alt kamera] --> VO[Optical Flow / Visual Odometry]
  IMU[Pixhawk IMU] --> EST[Durum kestirimi]
  BAR[Bar30] --> EST
  VO --> EST
  DET --> MISSION[Görev durum makinesi]
  EST --> MISSION
  MISSION --> CTRL[Rota / görsel servo kontrolcü]
  CTRL --> MAV[MAVLink köprüsü]
  MAV --> PX[ArduSub PID + motor mixing]
  PX --> ESC[ESC + motorlar]
  PX -->|telemetri| EST
  MAV --> LOG[Log + test kayıtları]
  DET --> LOG
  VO --> LOG
```

## Sorumluluk bölüşümü (kişilere değil **modüllere**)
- `camera/`: görüntü alma, kalibrasyon, zaman damgası.
- `vision/`: şamandıra/çizgi tespiti ve görsel güven skoru.
- `odometry/`: Optical Flow, VO ve ölçek belirsizliği.
- `estimation/`: IMU+derinlik+görsel ölçümlerin füzyonu.
- `navigation/`: rota, hedef ve sapma hesabı.
- `control/`: üst seviye konum/görsel servo kontrol; Pixhawk alt seviye PID'siyle kavga etmeme.
- `bridge/`: PyMAVLink/ArduSub telemetrisi, servis sağlık durumu, bağlantı kaybı.
- `logging/`: CSV/rosbag2/video senkron kayıt.

## Koordinat çerçeveleri
`map` (yerel parkur başlangıcı), `odom` (göreli ve drift içeren), `base_link` (araç), `camera_front` ve `camera_bottom`. MAVLink NED/FRD ile bilgisayar tarafında kullanılabilecek ENU/FLU arasında dönüşümler **belgelenmeden** dış odometri yayımlamayın.

## Neden ROS zorunlu değil?
Jetson Nano 4GB ilk prototipte Python+OpenCV+PyMAVLink çalıştırabilir. U-VIP-SLAM vb. ROS bağımlı araştırmalar önce masaüstünde oynatılır. Nano gerçek zaman / CPU/GPU RAM kısıtları test edilmeden modül seçilmez.
