---
title: "DEGISIKLIK-GUNLUGU"
created: 2026-11-09
updated: 2026-11-09
status: belgelendi
category: degisiklik
tags: [isas, umman, rov]
---

# Değişiklik günlüğü — 09.11.2026

## Tasarım farkları (önceki kayıtlarla karşılaştırma)
| Alan | Önce | Yeni öneri / bulgu | Son durum |
|---|---|---|---|
| Ana şase | 2026 6 motor | Küp form, 8 motor, iki hazne, Mini ROV yuvası | öneri; CAD ve güç hesabı yok |
| Navigasyon | Haversine + gyro + motor süresi / görüntü takibi | Optical Flow/VO + IMU/derinlik füzyonu + visual servo | araştırma; henüz kod entegrasyonu yok |
| GPS altında konum | Hedef koordinatlara baş yönü hesabı | DVL/sonar bütçe dışı; gerçek yanal hız gözlenebilirliği risk | sınırlama açık |
| Pusula | Pixhawk dahili | harici pusula ve motorlu manyetik kalibrasyon | satın alma/model belirsiz |
| Mini bırakma | elektromıknatıs | mekanik mandal/kızak karşılaştırması | karar bekliyor |
| Proje belgeleri | PDF/DOCX/XLSX ve dağınık sohbet | Obsidian Markdown, kaynak göstergesi, hata kaydı, elektrik şeması taslağı | bu teslimde hazırlandı |
| GitHub yazılım | çalışan olduğu varsayılan hat takibi | statik inceleme: GUI+PID komutu var, Pixhawk komutu yok | `KODDA` |
| Sensor A02YYUW | su altı mesafe sensörü olarak yazılmış | su altı kullanım iddiası kaldırılmalı | önerilen düzeltme |
| Bar30 hassasiyet | ±2mm denmiş | 2mm çözünürlük, mutlak doğruluk farklı | teknik düzeltme |

## Bu dokümantasyon paketinde hazırlanan içerik
- Kaynak envanteri ve orijinal dosya kopyaları
- Ana sistem ve Mini ROV notları
- BOM sekmeleri ve her ana kalemin açıklaması
- Ana güç/sinyal ve Mini ROV **kavramsal** Mermaid şemaları
- Kör uçuş, Optical Flow, VO, EKF, PID, Teach & Repeat ve ArduSub notları
- GitHub mevcut kod denetimi ve sorun listesi
- Test ve risk defteri, kaynak kartları, Obsidian bağlantıları
- Seçilmiş proje PDF sayfa görselleri ve kaynak gösterimleri

## GitHub durumu
`isas-rov/ISAS-yazilim` görünür. İstenen `isas-doc` ayrı repo erişilemediği için `ISAS-yazilim` içinde **ayrı `docs/` ağacı** önerildi; mevcut uygulama kodlarına dokunulmadı. Deponun gerçek değişiklik/PR bağlantısı ayrıca teslim yanıtında belirtilir.

## Revizyon 2 — Son kalite kontrolü (09.11.2026)
- README bağlantı tekrarları temizlendi.
- BOM bütçe özeti gerçek çalışma kitabındaki hesapla güncellendi; 6→8 itici + ESC tahmini ek maliyet ayrı gösterildi.
- Kaynak–iddia eşleştirmesi, test kanıtı rehberi ve QA raporu eklendi.
- GitHub kopyasındaki wiki bağlantıları taşınabilir Markdown bağlantısına dönüştürüldü.
- `isas-doc` görünürlüğü ve yetkisiz yazma durumu çözüldü diye işaretlenmedi.
