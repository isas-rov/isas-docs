---
title: "EMI-PUSULA"
created: 2026-11-09
updated: 2026-11-09
status: taslak
category: elektronik
tags: [isas, umman, rov]
---

# Pusula ve elektromanyetik girişim (EMI) — araştırma / test

## Sorun
Geçmiş havuz konuşmalarında yüzeyde pusulanın havuz çevresindeki manyetik alandan etkilendiği bildirildi. Ayrıca 8 motor + ESC + yüksek akım kabloları manyetometreyi etkileyebilir. **Suyun altına inmek dış manyetik bozulmayı otomatik çözmez.**

## Mekanizma
ESC ve motor çevresindeki akım dağılımı manyetik alan yaratır. Ana güç kablolarının döngü alanı da etkiler. Harici pusulanın sensör kablosuna yakın güçlü hatlar sadece manyetik değil elektriksel gürültü üretebilir.

## Önerilen kontrol
1. Motorlar dururken farklı konumlarda referans yön/alan vektörü kaydı.
2. Her motoru ayrı ayrı ve birlikte düşük–orta–yüksek komutlarda, yük altında kaydet.
3. Manyetik alan büyüklüğü (µT), heading farkı (°), toplam akım ve test yeri/zamanını eşleştir.
4. Pusulanın motorlara/PDB'ye uzaklığı değiştirilerek tekrar et; en iyi konumu CAD'e işaretle.
5. ArduSub sürümünde mevcutsa COMPASS_MOT yöntemlerini **dokümana göre** değerlendir; fiziksel yerleşim önceliklidir.
6. Ani tutarsızlıkta pusula ağırlığını düşür; jiroskop driftini ve görev güvenliğini hesaba kat. Mutlak konum kaybolursa körlemesine devam etme.

Kaynak: https://ardupilot.org/sub/docs/ ve https://www.ardusub.com/developers/full-parameter-list.html

## Kayıt şablonu
`test_id | motor_PWM | toplam_akim_A | yaw_reference_deg | yaw_measured_deg | mag_norm_uT | pusula_konum_mm | fotograflar | karar`
