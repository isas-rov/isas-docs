---
title: "ACIK-KAYNAK-PROJELER"
created: 2026-11-09
updated: 2026-11-09
status: belgelendi
category: referans
tags: [isas, umman, rov]
---

# Araştırılmış açık kaynak proje ve yöntemler

## En alakalı kaynaklar
| Kaynak | Link | Neden önemli? | Düzey / sınır |
|---|---|---|---|
| U-VIP-SLAM | https://github.com/chintha/U-VIP-SLAM | Monoküler kamera+IMU+basınç su altı SLAM | Araştırma kodu, ROS/derleme bağımlılıkları, Jetson Nano garanti değil |
| AQUALOC | https://www.lirmm.fr/aqualoc/ ; https://arxiv.org/abs/1910.14532 | Gerçek su altı görüntü/IMU/basınç test seti | Çevrimdışı benchmark, yarışma koşullarımız değil |
| UR-MVO | https://github.com/be2rlab/UR-MVO | Su altında monoküler VO, SuperPoint/SuperGlue | Güçlü GPU/çevrimdışı pipeline; ölçek/gerçek zaman teyidi |
| BlueROV Visual Servoing | https://github.com/abhimanyubhowmik/Visual_Servoing | Şamandıra tespit ve IBVS kontrolü | Göreli hedef kontrolü; global lokalizasyon değil |
| OpenNav Teach & Repeat | https://github.com/open-navigation/opennav_teach_and_repeat | Kaydedilmiş rota/eylem tekrarı | ROS2/Nav2 bağımlı; lokalizasyon kaynağı sağlamaz |
| Duke RoboSub ROS2 | https://github.com/DukeRobotics/robosub-ros2 | Sensör–füzyon–görev–kontrol ayrımı | Yüksek karmaşıklık; pahalı sensörler kullanabilir |
| ArduSub Frame | https://ardupilot.org/sub/docs/sub-frames.html | 8 itici / Vectored_6DOF geometri | Fiziksel motor açıları eşleşmeli |
| ArduSub Modes | https://ardupilot.org/sub/docs/modes.html | ALT_HOLD ve konuma bağlı mod farkı | Firmware sürümü kontrol edilmeli |
| ArduPilot External Nav | https://ardupilot.org/dev/docs/mavlink-nongps-position-estimation.html | ODOMETRY yoluyla GPS'siz kestirim | Kart/sürüm/koordinat kalibrasyonu gerekli |
| Blue Robotics Bar | https://bluerobotics.com/learn/bar-sensors-guide/ | Montaj, kablo, I2C, revizyon | Üretici teknik belge |

## Geçmiş TEKNOFEST örnekleri (yerel dosyalar)
- `gecmis-yil-rapor-1.pdf` — BAUROV, EKF+IMU+DVL+stereo kamera/AMCL, yüksek bütçe.
- `gecmis-yil-rapor-2.pdf` — Dolunay, havuz köşe referansı ve spiral tarama/görsel hedef.
- `gecmis-yil-rapor-3.pdf` — SUSONA, Jetson/Pixhawk + kamera/Ping; 2026 UMMAN ile kısmen benzer.
- `gecmis-yil-rapor-4.pdf` — EVA ROV, akustik konumlandırma metodu açıklaması.
- `gecmis-yil-rapor-5.pdf` — BARBAROV, görev bazlı nesne/pinger algılama.
- `gecmis-yil-rapor-6.pdf` — KAZGAN-SAB, referans KTR örneği.

Bu raporlar **diğer takımların beyanlarını** gösterir; çözümün kendi aracımıza doğrudan çalıştığını kanıtlamaz.
