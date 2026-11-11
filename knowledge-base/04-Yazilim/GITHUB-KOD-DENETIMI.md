> [!CAUTION] Eski kod denetimi — 9 Kasım 2026
> Bu sayfa eski `isas-rov/ISAS-yazilim` deposundaki prototipi inceler. Güncel geliştirme iskeleti: [isas-software](https://github.com/isas-rov/isas-software). Güncel ayrım için [repo durumu](../09-Degisiklikler/GUNCEL-REPO-DURUMU-2026-11-11.md) sayfasına bakın.

---
title: "GITHUB-KOD-DENETIMI"
created: 2026-11-09
updated: 2026-11-09
status: kodda-gozlendi
category: yazilim
tags: [isas, umman, rov]
---

# `isas-rov/ISAS-yazilim` — kaynak kod denetimi (09.11.2026)

**GitHub:** https://github.com/isas-rov/ISAS-yazilim/tree/main

## Mevcut ağaç
```text
README.md
aktif/hat_takibi_guncel.py
aktif/tahmin.py
egitim/birlestir.py
egitim/egit.py
egitim/egit2.py
arsiv/goruntu_isleme.py
arsiv/hat_takibi.py
arsiv/hat_takibi_webcam.py
arsiv/nesne_mesafe.py
arsiv/nesne_mesafe_foto.py
arsiv/yeni-test.py
```

## Kanıtlanan kod davranışı
- `aktif/hat_takibi_guncel.py`: OpenCV capture (`--csi`, `--video`, `--kamera`); HSV renk örnekleme; CLAHE; Gaussian blur; maskeleme/morfoloji; en büyük kontur; hata/çizgi açısı; lokal PID sayısal kontrol komutu; opsiyonel CSV log.
- Bu dosyada **Pixhawk/MAVLink importu veya araca motor komutu gönderimi yoktur**; `FAILSAFE` yazısı gösterilir fakat gerçek araç durdurma mekanizması uygulanmamış.
- `aktif/tahmin.py`: model ağırlığı `runs/detect/samandira_v1/weights/best.pt` ve `test.jpg` bekler; dosya/model ağırlığı kod deposunda görülmüyor. YOLO tek görüntü tahmini, otonom şamandıra yörüngesi değil.
- `egitim/egit.py` ve `egit2.py`: Ultralytics `yolo11n.pt` eğitim scriptleri; `veri/data.yaml` veya `veri_birlesik/data.yaml` gibi yerel dataset yolları bekliyor.
- `egitim/birlestir.py`: iki veri kümesi birleşirken bütün sınıf kimliklerini `0` yapıyor; modelin sınıf ayrımı (`green_buoy`/`orange_buoy`) gerekiyorsa problem oluşturur.
- `arsiv/nesne_mesafe.py`: tek kamera ve **varsayılan 20 cm şamandıra çapı** ile mesafe hesabı yapıyor; hedef ölçüsü doğrulanmadan güvenli navigasyon değildir.

## Gözlenmeyen / repo içinde bulunmayan parçalar
- Pixhawk MAVLink köprüsü; çalışan SITL/ArduSub otomasyon kodu; VO/SLAM/Optical Flow uygulaması; sensör füzyonu/EKF; görev durum makinesi; Mini ROV Pico firmware; sızıntı/E-stop runtime; 8 motor mixer testi; CI/test altyapısı; eğitim veri seti ve model ağırlıkları.
- Bunların başka gizli depolarda/yerel makinelerde bulunmadığı iddia edilmiyor; sadece incelenen repo ağacında yoklar.

## Tespit edilen kod riskleri
- `cv2.moments(en_buyuk)` içinde `M["m00"]` sıfıra bölme kontrolü yok.
- Renk kalibrasyonunda gri/çok düşük satürasyon için güçlü ışık değişimi hassas.
- Piksellerin şerit merkezine uzaklığı, otomatik olarak santimetre cinsinden sapma değildir.
- `--csi` kullanım yorumundaki dosya adı `hat_takibi_jetson.py`, gerçek dosya adı `hat_takibi_guncel.py` — README/komut uyuşmazlığı.
- `CLAHE` uygulanırken fareyle örneklenen `son_kare` ham görüntüden renk öğreniyor; ön işlemli ROI HSV dağılımı farklılaşabilir.
- `tahmin.py` içinde GPU/Jetson sürücü ve performans hedefi tanımlanmamış.

**Not:** İnceleme statik kod okumasıdır; motor/camera üzerinde gerçek çalıştırma yapılmamıştır.
