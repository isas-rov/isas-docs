---
title: Organizasyon depoları durum kaydı
updated: 2026-11-11
status: belgelendi
tags: [depo, git, degisiklik]
---
# Güncel GitHub depoları — 11 Kasım 2026

> [!NOTE] Görülme zamanı
> Aşağıdaki envanter, bu tarihte GitHub bağlantısı üzerinden görünen `main` durumunu gösterir. Depolar daha sonra değişebilir; uygulama öncesi tekrar `git pull` ve commit kontrolü yapın.

| Depo | `main` commit | Neler var? |
|---|---|---|
| [isas-docs](https://github.com/isas-rov/isas-docs) | `1a6b6e86e67c` | README/index, architecture, electrical, procurement, subsystems, testing ve Jetson kurulum rehberleri |
| [isas-hardware](https://github.com/isas-rov/isas-hardware) | `68b40b28a27f` | KiCad `legacy-umman`, yeni `main-rov` taslak sayfaları, BOM ve revizyon politikası |
| [isas-software](https://github.com/isas-rov/isas-software) | `911d16c22d13` | Python iskeleti, tests, SITL komut/log scriptleri ve Jetson yardımcı araçları |
| [ISAS-yazilim](https://github.com/isas-rov/ISAS-yazilim) | Daha önce incelenen eski depo | Görüntü işleme/hat takibi prototipleri; ana kodun devamı sayılmaz |

## Eski dokümantasyona göre dikkat çeken değişiklikler

1. **Doğru repo adı `isas-docs`:** Önceki metinlerdeki `isaa-doc` / `isas-doc` araması yanlıştı. Yeni ana depo organizasyondadır.
2. **KiCad taslakları artık depoda mevcut:** [Ana ROV güç ve kontrol sayfaları](https://github.com/isas-rov/isas-hardware/tree/main/electrical/kicad/main-rov). Bu dosyaların bulunması devrenin üretilip test edildiği anlamına gelmez.
3. **Yazılım geliştirme iskeleti ayrılmış:** `isas-software` içinde `tools/sitl_gorev_20sn.py`, `tools/sitl_kumanda_kayit.py` ve `src/isas/*` paket alanları var. Kod/test durumunu commit bazında ölçün.
4. **Motor sayısı farklı:** 2026 envanter ve KTR'de 6 itici; sekizli küp şase **konsept ve hesaplama aşamasında**.
5. **Kontrol donanımı isimleri farklı:** Bazı eski listelerde `Pixhawk 2.8`, bazı raporlarda `Pixhawk 4`; gerçek kart ve ArduSub sürümü fiziksel doğrulama gerektirir.
6. **Kamera modeli farklı:** Belgelerde alt kamera için `IMX335` ve proje konuşmalarında `OV2710` geçer; fiziksel ürün/port ile eşleştirin.

## Değişiklik politikası

İki envanter veya iki mimari not uyuşmazsa **eskisini silmeyin**. Kaynak adı, tarih ve donanım revizyonuna göre iki ayrı durum olarak belirtin; tek bir nihai konfigürasyon iddiası kurmayın. Nihai karar için [ADR](https://github.com/isas-rov/isas-docs/tree/main/decisions) açın.
