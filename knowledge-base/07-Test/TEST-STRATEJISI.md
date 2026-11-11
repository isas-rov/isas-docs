---
title: "TEST-STRATEJISI"
created: 2026-11-09
updated: 2026-11-09
status: taslak
category: test
tags: [isas, umman, rov]
---

# Test stratejisi — kanıt odaklı

**Kaynak:** `KTR_Test_Tecrube_Zaman_Butce_Risk.docx` 6. TEST bölümü. Bu belge başında **bütünleşik testler başlamadı** diyor; devamında geçmiş test yaşanmış gibi anekdotlar barındırıyor. Dolayısıyla taslaktaki <8cm şerit, <50cm konum, %90 mAP vb. rakamlar **hedef**, doğrulanmış ölçüm değil.

## Aşama kapıları
1. Masa üstü enerjisiz görsel/kablo/polarite kontrolü.
2. Regülatörlerin elektronik yük ile çıkış gerilimi ve ripple doğrulaması.
3. Tek ESC–motor kuru/uygun su yükünde kontrollü deney; kanal/sinyal/nötr.
4. Enerjisiz boş haznede sızdırmazlık.
5. Kuru entegrasyon: MAVLink, kamera, sızıntı, güç telemetrisi.
6. Güvenli havuz: nötr yüzerlik, depth hold, yaw; kademeli otonomi.
7. Görsel odometri harici referanslı doğruluk karşılaştırması.
8. Mini ROV bağlantı/bırakma ve bütün görev denemeleri.
9. Açık su testleri — güvenlik izinleri ve yarışma mevzuatına göre.

## Deney tasarımı
Her testte `minimum 3 tekrar` ilk öneridir; kritik güvenlik testleri daha çok tekrar gerektirebilir. Test sonuçlarına hedef ± tolerans ile bakılır. Yalnız video değil CSV log, gerilim/akım, kamera videosu ve tasarım revizyonu bağlanır.

## Riskli otomatik çıkış
2026 şartnamesi bitiş alanı dışında yüzeye çıkmayı sınırlıyor. Eski KTR taslağındaki `failsafe olunca 5 saniyede otomatik yüzeye çık` fikri her görevde uygun değildir. Kurtarma prosedürü görev durumuna ve emniyet riskine göre yeniden yazılmalı.

Şablon: [TEST-KAYDI-SABLONU](TEST-KAYDI-SABLONU.md).
