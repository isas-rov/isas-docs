---
title: "SOHBET-KARARLARI-ZAMAN-CIZELGESI"
created: 2026-11-09
category: tarihce
status: kaynak-ozeti
tags: [isas, umman, rov]
---

# 2026 sohbet ve tasarım kararları zaman çizelgesi

> **Kaynak niteliği:** Bu kronoloji, erişilebilen proje sohbet özetleri ve oturumda görülen proje konuşmalarından derlenmiştir. Geçmiş bütün ham sohbet mesajları, resimler ve dosyalar tek tek erişilebilir değildir; tarihsel olayların doğrulama seviyesi belirtilir.

| Tarih/dönem | Konuşmalarda gündeme gelen gelişme | Bağlı belge / doğrulama |
|---|---|---|
| Nisan–Mayıs 2026 | Ana + Mini ROV hibrit mimarisi, Mini ROV sinyalinin ana ROV üzerinden aktarılması, KTR bölümleri ve elektronik şema ihtiyacı | `GUNCELL-teknik-yeterlilik-formu-güncel.pdf`, resmî SSS derlemesi |
| 20 Mayıs 2026 | Ana araçta 6 itici, Jetson Nano, Pixhawk 4, Mini'de Pi Zero 2 W + Pico ve 4 motor belgelenmiş | KTR/TYF; satın alma ayrı teyit |
| Temmuz 2026 | Jetson kurulum, USB/VNC, Pixhawk–Mission Planner/QGroundControl, motor doğrudan testleri, ESC/PWM ileri-geri yön sorunları | Geçmiş sohbet raporları; ölçüm kaydı erişilemedi |
| 25–29 Temmuz 2026 | Motor 2000 PWM ile yavaş dönüyor / ters dönüş belirsiz; motor/ESC bağlantıları konuşuldu | [SORUN-KAYDI](../06-Sorunlar/SORUN-KAYDI.md) PR-01/02 |
| 4–18 Ağustos 2026 | 8 motorlu küp şase, iki ana hazne, pusula–güç hattı ayrımı, havuz manyetik alan kaygısı ve harici pusula önerisi | Yeni tasarım önerisi, CAD/ölçüm yok |
| 2026 yaz sonu | Mini ROV video ve bırakma, motor/ESC sızdırmazlığı, Mini elektrik mimarisi | MiniROV KTR ve BOM; gerçek test belirsiz |
| Ekim 2026 | 8 motorlu sistemde görsel odometri, IMU ve Bar30 ile düşük maliyetli kör uçuş; DVL/sonar yüksek maliyetten dolayı rafa kaldırıldı | Araştırma notları ve bu oturumdaki kararlar |
| 9 Kasım 2026 | Görev atamalarından önce kaynak, BOM, şema, sorun ve test belgelerini Obsidian MD olarak toplama | Bu kasa, MANIFEST ve değişiklik günlüğü |

## Eksik özgün kaynaklar
- Eski sohbetlerdeki görsel olarak gönderilen gerçek Pixhawk/ESC/kumanda fotoğrafları, mekanik CAD ekran görüntüleri ve çizim resimleri bu kasaya otomatik alınamadı.
- Yerel Jetson/STM kodları, KiCad projeleri, PCB Gerber, Motor test log CSV, video ve 3D CAD kaynak dosyaları ayrıca eklenmeli.
- Hangi ekip üyesinin hangi işi yapacağı **bilinçli olarak şu an atanmadı**; bu bir görev yönetimi planı değil, teknik bilgi tabanı.
