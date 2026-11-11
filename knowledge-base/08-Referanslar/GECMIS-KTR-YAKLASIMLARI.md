---
title: "GECMIS-KTR-YAKLASIMLARI"
created: 2026-11-09
category: referans
status: belgelendi
tags: [isas, umman, arastirma]
---

# Geçmiş KTR'lerde navigasyon yaklaşımları

**Bu tablo diğer takımların raporlarında *anlattığı* çözümleri özetler; bağımsız tamamlanma veya saha doğrulaması değildir.**

| Rapora ait dosya | Takım | İlgili PDF sayfası | Yaklaşım | Bizim için yararı / sınırı |
|---|---|---|---|---|
| `gecmis-yil-rapor-1.pdf` | BAUROV | 17–18 | ROS+EKF, IMU+DVL+görsel derinlik, AMCL, ZED stereo ve duvar referansı | Zengin mimari; DVL bütçe dışı. |
| `gecmis-yil-rapor-2.pdf` | Dolunay | 19–20 | Havuz köşesi referansı, spiral tarama, OpenCV/HSV ile nesne arama | Kontrollü havuzda mutlak hassas konum yerine çevre kullanımı; deniz için kısıtlı. |
| `gecmis-yil-rapor-3.pdf` | SUSONA | 19–22 | Jetson Nano + Pixhawk 4, kamera/ultrasonik/Ping sonar, görüntüyle konum ve hız komutu | İki bilgisayarlı mimariye örnek; Ping/A02YYUW su altı uyumu karıştırılmamalı. |
| `gecmis-yil-rapor-4.pdf` | EVA ROV | 24–25 | Akustik lokalizasyon / hidrofon ve çoklu istasyondan menzil-zaman yaklaşımı | Kod ve maliyet doğrulanmadan satın alma çözümü değil. |
| `gecmis-yil-rapor-5.pdf` | BARBAROV | 17–19; 23 | Renk, hedef ve pinger görev akışları, simülasyon | Görev durum makinesi ve KTR anlatım örneği. |
| `gecmis-yil-rapor-6.pdf` | KAZGAN-SAB | 6 vd. | Görüntü işleme ve otonom hareket birlikte raporlanmış | Uygulama/test detayları ham log olmadan kanıt sayılmaz. |

## Araştırma notu
2026 hedefi su altında göreli konum kestirimi olduğundan **doğrudan kopyalanacak tek bir hazır çözüm bulunmadı**. U-VIP-SLAM, UR-MVO ve BlueROV Visual Servoing bileşen bazında denenebilir. Bak: [ACIK-KAYNAK-PROJELER](ACIK-KAYNAK-PROJELER.md).
