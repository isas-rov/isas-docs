---
title: "ARDUSUB-SITL-MAVLINK"
created: 2026-11-09
updated: 2026-11-09
status: taslak
category: yazilim
tags: [isas, umman, rov]
---

# ArduSub / SITL / MAVLink çalışma notu

## Gerçek parçalar
- Pixhawk üzerinde **ArduSub**, aracı dengeler ve uygun motor karıştırmasını yürütür.
- QGroundControl bağlantı/parametre/kalibrasyon içindir.
- Jetson/PyMAVLink üst seviye komut ve telemetri sağlar.
- WSL2 üzerindeki SITL, **fiziksel motor/hidrodinamik davranış kanıtı değildir**.

## 8 itici: hazır konfigürasyon
ArduSub `FRAME_CONFIG=2` Vectored_6DOF, `FRAME_CONFIG=3` Vectored_6DOF-90 gibi **8 motorlu** frame örnekleri içerir. Seçim motor geometrisiyle birebir eşleşmelidir. Motor yönü ve servo kanal eşlemesi tabloda ölçülür. Kaynak: https://ardupilot.org/sub/docs/sub-frames.html

## Kontrol modları
`ALT_HOLD`: derinlik sensörüyle hedef derinlik tutulabilir. `GUIDED`/`AUTO` gibi konum tabanlı modlar güvenilir yatay konum kestirimi gerektirir. ODOMETRY harici konum/hız sağlama yolu olabilir; kart/firmware/koordinat dönüşü ve test doğrulanmalı.

Kaynak: https://ardupilot.org/sub/docs/modes.html • https://ardupilot.org/dev/docs/mavlink-nongps-position-estimation.html

## İlk doğrulama
1. Pixhawk tam model/firmware/port doğrula.
2. Motorlar sökülüyken doğru ESC uç ve nötr sinyallerini test et.
3. ESC'lerin arm/reverse davranışını üretici test yöntemiyle doğrula.
4. SITL'de telemetri, mod, arming, kesilen link davranışı logla.
5. Enerji verildiğinde gerçek ESC kanalları ve motor yönleri güvenli standda doğrulanır.
6. Havuzda düşük komutla 6-DOF eksen testleri.
