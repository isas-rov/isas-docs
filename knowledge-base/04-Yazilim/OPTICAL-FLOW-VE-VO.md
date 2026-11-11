---
title: "OPTICAL-FLOW-VE-VO"
created: 2026-11-09
updated: 2026-11-09
status: taslak
category: yazilim
tags: [isas, umman, rov]
---

# Optical Flow / Visual Odometry teknik ders notu

## Optical Flow nedir?
Ardışık görüntülerde aynı dokulu noktanın görüntü koordinatının (`u,v`) değişimini ölçer. İleri/yanal hareketi ayırt etmek için kamera dönüşü, lens bozulması ve geometri dikkate alınır.

### Basit ölçek denklemi (ideal düz zemin, aşağı bakan kalibre kamera)
`ΔX ≈ h * Δu / f_px`, `v_x ≈ ΔX/Δt`. `h` kamera–zemin yüksekliği, `f_px` kalibre odak uzunluğu, `Δu` piksel kaymasıdır. **Bar30 su yüzeyinden derinliği verir; h değildir.**

## Ön prototip algoritması
1. Kamera zaman damgası ve `intrinsics` (`fx,fy,cx,cy, distortion`) kalibrasyonunu kaydet.
2. Renk→gri, CLAHE, `goodFeaturesToTrack` ile köşe seç.
3. `calcOpticalFlowPyrLK` ile takip et; ters akış ve RANSAC ile aykırı noktaları at.
4. IMU gyro/tüm yönelimden dönüş hareketini ayır; optik akış belirsizliği hesapla.
5. Aydınlatma, doku, bulanıklık, bulanık su, yansıma ile özellik sayısını test et.
6. Metrik ölçek yalnız doğrulanmış taban mesafesi / stereo / başka referans varsa kullan.

## VO ile fark
Optical Flow piksel kaymasını ölçer; VO çoklu görüntüden kameranın görece hareketini/pozunu çözer. Monoküler VO genellikle mutlak ölçeği gözlemleyemez. Loop closure olan SLAM daha önce görülen bölgelerle hata düzeltebilir; su altında her ortamda garanti değildir.

## Kalibrasyon
Kamera su altı optik penceresinin gerisindeyse kırılma etkisi ve düz/kubbe cam geometriyi değiştirir. Havada yapılan kalibrasyonun su altında aynı kalacağını varsaymayın.

## Performans raporu
`video_id, fps, resolution, tracked_features, inlier_ratio, estimated_dx, ground_truth_dx, scale_source, ATE/RPE, latency_ms, jetson_load`.
