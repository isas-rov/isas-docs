---
title: "KANIT-VE-KAYNAK-ESLESTIRMESI"
created: 2026-11-09
updated: 2026-11-09
status: belgelendi
category: kaynak
tags: [isas, umman, rov]
---

# Hangi iddiayı hangi kaynak destekliyor?

Bu tabloda **kaynaktan bildirilen özellikler**, **kodda gerçekten görülen davranış** ve **henüz denenmemiş tasarımlar** ayrı tutulur. Geçmiş takım KTR'leri ile UMMAN'ın kendi belgeleri aynı kanıt sınıfında değildir.

| İddia / konu | Birincil kaynak | Kaynak kapsamı | Kullanılabilir sonuç | Durum |
|---|---|---|---|---|
| 2026 görev-2 koordinat ile şamandıra ve bitiş | `2026_İNSANSIZ_SU_ALTI_SİSTEMLERİ_YARIŞMASI_-_TÜRKÇE_Y5D0m.pdf`, PDF s.29 | 2026 yarışma kuralı | 2026 için doğrulanabilir; 2027 için değil | BELGEDE |
| Ana aracın 6 iticili bütçesi | `UMMAN-MALZEME-GUNCELxlsx.xlsx`, `Ana Gider Listesi` satır 42–43 | 6 itici + 6 ESC maliyeti | 8 itici revizyonu henüz BOM'da yok | BELGEDE |
| Pixhawk 4 + Jetson Nano planı | `GUNCELL-teknik-yeterlilik-formu-güncel.pdf`, PDF s.6–8 | Beyan edilen donanım | Fiilî kart modeli fotoğrafla kontrol edilmeli | BELGEDE |
| Bar30 ile derinlik kontrolü | `GUNCELL-teknik-yeterlilik-formu-güncel.pdf`, PDF s.7–8 | Tasarlanan sistem | Derinlik tutma gerçek logla doğrulanmalı | BELGEDE |
| Ön/alt kamera amaçları | `GUNCELL-teknik-yeterlilik-formu-güncel.pdf`, PDF s.7–8 | Ön nesne, alt hat tespiti | Alt kameradan VO üretimi yeni araştırmadır | BELGEDE / ONERI |
| Hat takibinde HSV, CLAHE, PID | `isas-rov/ISAS-yazilim/aktif/hat_takibi_guncel.py` | Statik kod incelemesi | Arayüzde sayısal komut üretiliyor; MAVLink motor komutu yok | KODDA |
| Şamandıra tespit modeli | `isas-rov/ISAS-yazilim/aktif/tahmin.py` | YOLO inference kodu | Model ağırlığı/test görseli repo ağacında bulunmadı | KODDA / EKSİK |
| Mini ROV'un Pi Zero/Pico mimarisi | `MiniROV_Yazilim_KTR_v2.pdf` | Yazılım tasarımı | Çalışan Mini firmware ve telemetri kodu görülmedi | BELGEDE |
| Kör uçuş Haversine + gyro/PWM süreleri | `KTR-Genel-Yazilim.pdf`, PDF s.7–8 | Önceki tasarım | Mutlak konum doğruluğu kanıtı değildir | BELGEDE |
| Gerçek test sonuçları | `KTR_Test_Tecrube_Zaman_Butce_Risk.docx` | Test hedefleri ve metin örnekleri | Ham log olmadan yapılan test iddiası kesinleştirilemez | DOGRULANMADI |
| Mono kamera+IMU+basınç SLAM yöntemi | https://github.com/chintha/U-VIP-SLAM | Dış açık kaynak araştırma | Bizim Jetson Nano'da çalıştığı doğrulanmadı | ARASTIRMA |
| Şamandıra visual servoing | https://github.com/abhimanyubhowmik/Visual_Servoing | Dış açık kaynak araştırma | Yerel kontrol örneği; mutlak konum çözümü değil | ARASTIRMA |

Kaynakların orijinal halleri tam Obsidian kasasındaki `99-Kaynaklar/Orijinal-Dosyalar` klasöründedir. GitHub'a yalnızca dokümantasyon konulacaksa bu orijinal dosyalar arşive dâhil edilmez.
