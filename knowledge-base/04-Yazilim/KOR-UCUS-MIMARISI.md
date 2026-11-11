---
title: "KOR-UCUS-MIMARISI"
created: 2026-11-09
updated: 2026-11-09
status: taslak
category: yazilim
tags: [isas, umman, rov]
---

# Kör uçuş: DVL ve sonar olmadan çözüm tasarımı

## Gerçek problemin tanımı
Şartname koordinat verir; **su altında GNSS doğrudan yoktur**. Araç mevcut baş yönünü ve derinliğini korurken akıntıyla kayabilir. Motor komutunu veya sadece IMU ivmesini entegre etmek güvenilir yatay konum değildir.

## Aşamalı yaklaşım
1. **Minimum çalışan prototip:** Bar30 ile depth hold, Pixhawk IMU ile yönelim, düşük hızda kalibre hareket modeli. `IMU+komut → kabaca hareket` durumu `LOW_CONFIDENCE`.
2. **Görsel hareket katmanı:** OV2710 ile zemin özelliği tespiti, Optical Flow ve dönüş telafisi. Görülen zeminin mesafesi bilinmiyorsa metrik hız güvenilmez; `SCALE_UNKNOWN`.
3. **VO/SLAM araştırması:** AQUALOC veri setinde U-VIP-SLAM / UR-MVO; sonra Jetson maliyeti, kamera kalibrasyonu, test sonuçları.
4. **Sensör füzyonu:** Görsel hareketi + IMU yönelimini + Bar30 derinliğini birleştir; durum kovaryansı/kalite skoru yayımla.
5. **Görev:** şamandıra göründüğünde `visual_servo`, dönüş tamamlanınca bitiş alanı görsel teyidi.
6. **Fail-safe:** kamera görüş kaybı, pusula sapması, su kaçağı, batarya, link kaybında tasarım riskine göre güvenli davranış; 2026 yalnız bitişte yüzeye çıkış kısıtını unutma.

## Hangi sensör neyi veriyor?
- **IMU:** dönme, eğim ve anlık özgül kuvvet; akıntıyı doğrudan ölçemez.
- **Bar30:** su yüzeyine göre derinlik; alt kamera–zemin mesafesi değil.
- **Optical Flow:** görüntü düzleminde özellik kayması; kamera dönüşü/ölçek problemi var.
- **Monoküler VO:** göreli kamera yörüngesi; mutlak ölçek ya da mutlak enlem-boylam tek başına yok.
- **Görüntüden hedef:** şamandıra merkez/siluet açısı; görüşteyken yönlendirme düzeltmesi.

## Araştırma kaynakları
[ACIK-KAYNAK-PROJELER](../08-Referanslar/ACIK-KAYNAK-PROJELER.md); özellikle U-VIP-SLAM, UR-MVO, AQUALOC, Visual Servoing ve Teach & Repeat.

## Çalışabilirlik kriterleri (öneri; test sonucu değil)
Birincil test: havuzda bağımsız ölçülen 5–10m düz rotada konum tahmini hatası; görüş zayıflamasında geçerli/invalid bayrağı; pusula motor etkisi; şamandıra görüldüğünde hedef merkezleme başarısı; Jetson CPU/GPU/sıcaklık ve uçtan uca gecikme.
