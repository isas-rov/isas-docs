---
title: "MALZEME-DURUM-VE-NEDEN"
created: 2026-11-09
updated: 2026-11-09
status: taslak
category: donanim
tags: [isas, umman, rov]
---

# Hangi malzemeyi neden kullanıyoruz?

> **Eldelik durumu:** Konuşmalarda Jetson ve Pixhawk'a bağlanıldığı, motor testleri yapıldığı anlatılmıştır. Ancak liste içindeki her ürün için fatura, seri numarası ve güncel fiziksel sayım yoktur. Bu sayfadaki adetler **BOM planı** olarak tutulur.

| Alt sistem | Seçilen malzeme | Neden? | Bağımlılık / risk |
|---|---|---|---|
| Ana işlem | Jetson Nano 4GB | OpenCV / görev yönetimi / iki kamera | 5V güçlü regülatör; Linux sürücüsü; Nano performansı |
| Otopilot | Holybro Pixhawk 4 (listede) | IMU, stabilizasyon, ESC sinyali | Eski sohbetlerde 2.8 geçti; model/port sayısı teyidi |
| Derinlik | BlueRobotics Bar30 | Basınçtan derinlik ve ArduSub depth hold | Sadece ön yüz suya; JST GH/DF13 sürümleri; kısa I2C |
| Ön görüş | IMX219 CSI | Şamandıra ve hedef tespiti | CSI kablosu/jetson sürücüsü ve optik pencere |
| Alt görüş | OV2710 USB | Hat izleme, Optical Flow/VO araştırması | USB fiziksel sığma, ışık, kalibrasyon, ölçek |
| Ana itki | Mitras BLDC ×6 BOM / ×8 öneri | İtki | 4S uygunluk, yük, itki eğrisi ve dağıtım matrisi |
| Ana ESC | Blu 30A ×6 BOM / ×8 öneri | Üç faz sürme | Nötr/reverse PWM; termal/sızdırmazlık |
| Güç | 4S 16000mAh LiPo | Ana batarya | SoC izleme, sigorta, kesici, yük/akım testi |
| Güç dağıtım | Özgün Ana PDB | Akımı alt sistemlere bölme | 8 ESC için çizim revizyonu şart |
| Veri | Sublink/Hi-com, tether | Karaya kablolu iletim | Modüllerin gerçekten birbirine uyumu, kablo çiftleri ve bant genişliği |
| Su kaçağı | Leak probe | Hazne güvenliği | Nem ve gerçek su ayrı değerlendirilir |
| Mini görüntü | Pi Zero 2 W + Camera Module 3 Wide | Boru içinde canlı görüntü | Video gecikmesi, 5V besleme, ana araç üzerinden aktarım |
| Mini kontrol | Pi Pico | 4 ESC ve acil güvenlik | UART ve watchdog protokolü |
| Mini enerji | 3S 5000mAh ve mini PDB | Ayrı güç kaynağı | Araç içi stop ve iki araç arası kablo güvenliği |
| Mekanik | H-100/H-60, penetratör, conta, PETG | Sızdırmaz hacim ve şase | CAD paketleme, IP derinlik testi |
| LED | Ana/mini su altı lambaları | Düşük ışıkta görüntü | Isı, güç, kamera parlaması |
| A02YYUW | BOM'da 6 | Eski tasarımda su altı engel algılama diye yazılmış | **KULLANIM HATALI:** su altında sonar gibi kullanılamaz |

## Tedarik kontrol şablonu
Her kalem için tablo genişletilir: `ürün SKU | sayım | seri no | satın alma tarihi | gerçek model | konum | test sonucu | fotoğraf | sorumlu | firmware | kaynak`.
