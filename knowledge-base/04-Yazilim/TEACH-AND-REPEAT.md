---
title: "TEACH-AND-REPEAT"
created: 2026-11-09
updated: 2026-11-09
status: taslak
category: yazilim
tags: [isas, umman, rov]
---

# Manuel sürüşten rota öğretme (Teach & Repeat)

## Geçmiş fikir
Aracı kumandayla parkurdan geçirip PWM / joystick / IMU logları kaydetmek, sonra aynı hareketi otomatik oynatmak önerildi. **Aynı PWM dizisini tekrar etmek konum kontrollü sürüş değildir**: akıntı, pil, başlangıç açısı, yük ve Mini ROV ayrılması sonucu değiştirir.

## Uygulanabilir sürüm
1. Manuel sürüşte `joystick`, MAVLink mesajları, `motor output`, `gyro`, `depth`, `camera frames`, `voltage/current`, zaman damgaları birlikte kaydedilir.
2. Mümkünse dış havuz referansı kullanılarak gerçek rota ölçülür; bu yalnız test kalibrasyonu içindir.
3. Motor modeli (`komut→ölçülmüş hareket`) ve görüntü odometri parametreleri çıkarılır.
4. Görev esnasında referans **rota** takip edilir; yeni sensör verisi ile sapma sürekli düzeltilir.
5. Görsel hareket/konum güveni kaybolduğunda açık çevrim tekrar moduna sınırsız devam edilmez.

## Hazır kaynak
https://github.com/open-navigation/opennav_teach_and_repeat — ROS2/Nav2 rota kaydı ve tekrarı; **lokalizasyonu çözmez**. Bizim sistem için konsept/mesaj tasarımı örneğidir.

## Kayıt şeması
`timestamp_ns, mode, js_forward, js_lateral, js_yaw, depth_m, roll, pitch, yaw, gyro_xyz, accelerometer_xyz, motor_1..8, battery_v, battery_a, camera_seq, vo_valid, estimated_xyz, covariance`.
