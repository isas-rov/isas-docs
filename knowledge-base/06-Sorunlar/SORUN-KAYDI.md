---
title: "SORUN-KAYDI"
created: 2026-11-09
updated: 2026-11-09
status: belgelendi
category: sorun
tags: [isas, umman, rov]
---

# Sorun–belirti–muhtemel neden–çözüm kataloğu

> `Kaynakta rapor edildi` ile `kanıtlı olarak çözüldü` ayrı şeylerdir. Bu sayfa konuşmalardaki olayları ve mühendislik yorumlarını sınıflandırır.

| ID | Belirti / bağlam | Olası nedenler | Çözüm / doğrulama | Durum |
|---|---|---|---|---|
| PR-01 | QGroundControl'de 2000 PWM, motor yavaş dönüyor | ESC kalibrasyonu, güç beslemesi, motor yükü, failsafe, mod/kanal eşlemesi, ESC ileri/geri protokolü | servo çıkışı osiloskop/logic analyzer; voltaj yükte ölçümü; bir ESC-motor referans testi | Kullanıcı sohbetinde raporlu, çözüm kanıtı yok |
| PR-02 | Motor bir yönde dönüyor, reverse çalışmıyor | çift yönlü ESC aralığı, neutral ayarı, arming, `MOTx_DIRECTION`/PWM uçları | üretici PWM nötr–ileri–geri spesifikasyonu ve motor stand testi | Açık |
| PR-03 | Havuzda pusula sapıyor | havuz metal donatısı, yerel manyetik alan, motor/güç kablosu | güç kapalı/açık vektör kaydı; dış pusula konum testi | Açık |
| PR-04 | Jetson USB takınca hazneye sığmıyor | kablo/fiş hacmi CAD'e eklenmemiş | gerçek soket/fiş/bükülme mesafesi 3D yerleşim | Geçmiş olay, nihai CAD görülmedi |
| PR-05 | Mini ROV magnet bırakma mekanizması güvenilirliği | güç kesintisi, mekanik yük, korozyon, manyetik alan | servo kilit/yaylı kızak konsept prototipleri | Yeniden tasarım |
| PR-06 | A02YYUW su altı engel sensörü gibi yazılmış | IP67 su geçirmezlik ile **su altı akustik menzil ölçümü** karıştırılmış | sonar yerine kullanılmasın; BOM/KTR açıklamaları düzeltilecek | Belgede tespit, kod/şema revizyonu bekleniyor |
| PR-07 | Bar30 ±2 mm doğruluk olarak yazılmış | çözünürlük ile doğruluk karışmış | üretici accuracy çizelgesiyle KTR ifadeleri düzeltilmeli | Düzeltme gerekli |
| PR-08 | 6→8 motor kararı PDB ve kabloya yansımamış | eski BOM farklı revizyonda kalmış | güç/mekanik/ArduSub frame eş zamanlı revizyon | Açık |
| PR-09 | Görsel odometri zemin yüksekliği bilinmediğinde yanlış ölçek | Bar30 derinlik ≠ kameranın zemine mesafesi | düz kalibre havuz; stereo/ölçek kısıtları; güven skoru | Araştırma riski |
| PR-10 | Sadece PWM logu ile rota tekrarı | açık çevrim hareket, akıntı ve batarya değişimi | referans rota + ölçüm bazlı kapalı çevrim | Tasarım iyileştirme |
| PR-11 | Mini video gecikmesi / paket düşmesi | Pi Zero 2 W encode, tether veri ve Jetson yükü | zaman damgası/fps/bitrate/latency ölçümü | Test bekliyor |
| PR-12 | ESC'yi epoksiye gömünce aşırı ısınma riski | termal izolasyon | termal ölçüm/üretici önerisi ve muhafaza seçimi | Önleyici risk |
| PR-13 | Havuz/denizde iletişim kesilmesi | penetratör/tether/haberleşme köprüsü | heartbeat watchdog, görev bağımlı failsafe | Test bekliyor |
| PR-14 | KTR taslağında yapılmış test gibi anlatılan veriler | belge içi tutarsızlık | ham log, foto, tarih, ölçüm raporu olmadan `doğrulandı` denmez | Dokümantasyon riski |
| PR-15 | Repo hat takip kodunda `FAILSAFE` sadece ekrana yazılıyor | motor kontrol bağlantısı yok | gerçek MAVLink kontrol / güvenli durum testleri yapılınca entegrasyon | Kodda gözlendi |
| PR-16 | `M["m00"]` sıfır olabilecekken bölme | kontur moment kenar durumu | `m00 != 0` koruması ve test | Kodda gözlendi |
| PR-17 | Yoğun düşük ışıkta görüntü zayıf | partikül, optik pencere, yanlış LED konumu | açı/LED/parlaklık/CLAHE testleri | Tasarım riski |
| PR-18 | IMU ile GPS'siz konum drift | bias ve çift integrasyon | VO ve dış referans ile test; covariance tabanlı frenleme | Temel kısıt |

## Yeni kayıt formatı
`ID`, tarih, gerçek cihaz/firmware, belirti videosu, ham telemetri, güvenlik etkisi, hipotezler, deney sırası, uygulanan değişiklik, tekrar testi, sonuç, takip kararı.
