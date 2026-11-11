---
title: "DURUM-VE-KARARLAR"
created: 2026-11-09
updated: 2026-11-09
status: belgelendi
category: yonetim
tags: [isas, umman, rov]
---

# Mevcut durum / tasarım kararları

| Konu | 2026 belge/BOM | Yeni karar/konuşma | Nihai durum |
|---|---|---|---|
| Ana itici sayısı | 6× Mitras, 6× Blu 30A | Küp şase, 8 itici | **ONERI**, yeni güç/itki hesabı gerekli |
| Ana görev bilgisayarı | Jetson Nano 4GB | Korunuyor | BELGEDE, fiziksel/çalışma testi ayrı doğrulanacak |
| Otopilot | Holybro Pixhawk 4 listede | Eski motor sohbetlerinde Pixhawk 2.8 sözü var | Model/kart seri numarası doğrulanmalı |
| Derinlik | Bar30 | Korunuyor | BELGEDE, fiziksel kurulum ve kalibrasyon kanıtı bekliyor |
| Ana kamera | IMX219 ön / OV2710 alt | Görsel hedef + görsel odometri | Önceki mimari BELGEDE; VO **ONERI** |
| Sonar/DVL | Bütçe dışı | Kullanılmayacak | Tasarım tercihi: test limitleri belirsiz |
| Mesafe sensörü | A02YYUW ×6 yazılmış | Deniz altında güvenilmez | Hata düzeltmesi zorunlu, su altı sonarı diye geçmemeli |
| Mini ROV bırakma | IP68 elektromıknatıs önerisi | Daha güvenilir mekanik mandal/kızak | Karar verilmedi; iki seçenek incelenecek |
| Batarya | 4S 16000 mAh / Mini 3S 5000 mAh BOM | Li-ion alternatif değerlendirme | Li-ion kararı YOK |
| Pusula | Pixhawk dahili | Motor etkisinden uzak harici pusula | Model/yerleşim ve motorlu test bekliyor |

## Kesinleştirilecek teknik kararlar
- Pixhawk 4 mü 2.8 mi; `FRAME_CONFIG` ve uygun kanal sayısı ne?
- İticiler dört yatay + dört düşey mi, açıları ne? Geometri ile `Vectored_6DOF` gerçekten eşleşiyor mu?
- Kamera alt zemini görebilecek mi? VO ölçeği nasıl belirlenecek?
- Mini ROV elektronik sistemi için ayrı batarya mı kullanılacak ve acil stop kapsamı ne?
- Kablolu iletişimde güvenlik hattı ve görev sırasında kesilmesi gereken veri bağlantısı nasıl uygulanacak?

## Kanıt tanımı
- `PLAN`: öneri/şartname.
- `CAD`: tasarım modeli dosyası mevcut.
- `BENCH`: masa testi ölçümleri + video + tarih.
- `POOL`: havuz testi + su/derinlik bilgisi + log.
- `SEA`: açık deniz testi + dış referans.
Henüz bu kasada doğrulanmış BENCH/POOL/SEA ham logları yoktur.
