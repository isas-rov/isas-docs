---
title: "SEKIZ-MOTORLU-SASE"
created: 2026-11-09
updated: 2026-11-09
status: taslak
category: mekanik
tags: [isas, umman, rov]
---

# Sekiz motorlu küp şase — öneri

## Önceki tasarım
2026 malzeme listesi ana araç için **6 Mitras + 6 ESC**, H-100/H-60 hazneler, PETG şase, yüzerlik köpüğü ve gövdeye bağlanan Mini ROV içeriyor. Yeni konuşmalarda 8 motor/iki hazne/mini ROV yuvası önerildi.

## Motor dizilimi seçimi
Dört yatay + dört dikey, uygun `Vectored_6DOF` yerleşimi değerlendirilebilir. Ama motorların tam konum ve dönme açıları mekanik çizim ve thrust-allocation matrisiyle doğrulanmadan hazır ArduSub frame seçilmez.

## CAD paketleme şartı
Tüm kartların gerçek 3D modeli/USB/CSI/UART konnektörleri, kablo bükülme yarıçapı, penetratör delikleri, bakım için erişim alanı ve sıcaklık boşlukları dahil edilir. Önceki deneyimde Jetson USB soketi hazne içinde yer problemi çıkardı.

## Kaldırma/denge
- Kütle merkezi CG, kaldırma merkezi CB, kaldırma hacmi ve net yüzdürücülük hesaplanır.
- Mini ROV doklu ve bırakılmış iki ayrı kütle/CB hesabı yapılır.
- Motor reaksiyon torkları, kablo/tether sürüklemesi, kamera görüşü ve alt kamera zemin mesafesi eşzamanlı değerlendirilir.
- PETG üretim toleransı, deniz suyu korozyon, keskin kenarlar, pervane korumaları ve test koşulları belirtilir.

## Çıktılar
Assembly CAD, tüm parçaların ölçülü STEP dosyaları, kablo/hazne layout, itici koordinat tablosu (X,Y,Z, doğrultu birim vektörü), kütle tablosu, CG/CB ve hidrodinamik varsayımlar.
