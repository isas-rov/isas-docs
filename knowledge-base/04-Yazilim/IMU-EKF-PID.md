---
title: "IMU-EKF-PID"
created: 2026-11-09
updated: 2026-11-09
status: taslak
category: yazilim
tags: [isas, umman, rov]
---

# IMU / EKF / PID kavramları

## Üç farklı katman
- **IMU** sensördür: ivmeölçer ve jiroskop verileri (Pixhawk yönelim kestirimi sensör birleştirme içerebilir).
- **EKF** durum tahmincisidir: hareket modeli ile ölçümleri güvenilirliğine göre birleştirir; **olmayan bir mutlak konumu yaratmaz**.
- **PID** kontrolcüdür: `e = hedef - ölçüm` üzerinden komut üretir; hatalı ölçümü düzeltemez.

## Örnek
Baş yönü 30° hedef, ölçülen 25°; anlık hata 5°. Kontrol bu hata için yaw komutu üretir. Pusula yanlış 75° ölçüyorsa aynı PID aracı yanlış yöne çevirebilir.

## İş bölümü
Pixhawk ArduSub derinlik/yönelim alt seviye kontrol; Jetson rota/görsel servo gibi üst seviye kontrol. İki PID, aynı motor/ekseni birbirinden habersiz doğrudan sürmeyecek.

## Pusula kaybında
Jiroskop kısa süreli yön değişimini takip edebilir, drift artar. Görsel VO yerel hareket için yardımcı olur; kuzey/yatay pozisyon güvenini otomatik geri getirmez.

## Veride minimum doğrulama
`timestamp`, gyro/accel kalibrasyonu, bar30 derinlik ve deniz suyu yoğunluğu, koordinat çerçevesi, offset, covariance, failsafe threshold ve ham loglar.
