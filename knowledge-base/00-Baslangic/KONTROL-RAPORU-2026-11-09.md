---
title: "KONTROL-RAPORU-2026-11-09"
created: 2026-11-09
updated: 2026-11-09
status: belgelendi
category: kalite
tags: [isas, umman, rov]
---

# Dokümantasyon kalite kontrolü — 9 Kasım 2026, revizyon 2

## Denetim kapsamı

- Tam Obsidian kasasındaki Markdown notlar, Canvas dosyası, PDF sayfa haritaları ve kaynak dosya envanteri kontrol edildi.
- Yerel XLSX dosyasındaki dört sayfa, satır toplamları ve `Bütçe Özeti` formül referansları incelendi.
- `isas-rov/ISAS-yazilim` deposunda `main` dalının 4d6e2a03324e423175bf041642d2768ffd75a445 SHA'sında kod ağacı ve README incelendi; eski kodlara yazma yapılmadı.
- Ayrı `isas-doc` deposu bağlı GitHub görünümünde bulunamadı. **Görünmüyor = bulunmuyor** sonucu çıkarılmadı; özel depo veya bağlanmamış organizasyon izni olabilir.

## Giderilen problemler

1. Obsidian ana README'sindeki üçlü yinelenen bağlantılar kaldırıldı; yeni başvuru ve kalite kontrol bağlantıları eklendi.
2. `BOM-BUTCE-OZETI` sayfasındaki yanlış tablo başlıkları ve eksik fiyatlar gerçek çalışma kitabı satır toplamlarıyla düzeltildi. Ana ve alt bütçeler mükerrer toplanmıyor.
3. 6→8 itici ve ESC revizyonunun yalnızca mevcut listedeki birim fiyatlara göre tahmini etkisi açıklandı; PDB ve diğer donanım ek maliyetleri ayrıca açık bırakıldı.
4. `MALZEME-ANA-LISTE` son sütununun kesilmiş kaynak metin olduğunu belirten uyarı eklendi; yanlışlıkla mühendislik gerekçesi sanılmamalı.
5. GitHub paketindeki Obsidian biçimindeki sayfa bağlantıları, GitHub tarafından tıklanabilir **göreli Markdown dosya bağlantılarına** dönüştürüldü. Kaynak PDF ve görseller özel Obsidian arşivinde tutuldu.
6. Kaynak–iddia/karar eşleştirmesi, prototip doğrulama kriterleri ve aktarım yönergesi eklendi.

## Bilinçli olarak çözülemeyen fiziksel belirsizlikler

- Gerçek Pixhawk model/revizyonu, 8 motorun fiili sayısı ve yerleşimi, ESC tipi, güç devresi pinout'u, fiziksel konnektör ölçüleri.
- Gerçek KiCad/ERC raporları, gerçek CAD, kamera kalibrasyon dosyaları, bağımsız ölçümlü havuz logları.
- Geçmiş sohbetlere iliştirilmiş ama burada ham dosya olarak bulunmayan fotoğraf/video ve çizimler.
- Yeni sezona ait resmî yarışma kuralları.

**Dolayısıyla hiçbir kavramsal elektrik şeması üretilmiş/kullanıma hazır şema, hiçbir KTR performans ifadesi doğrulanmış gerçek araç testi olarak işaretlenmedi.**

## GitHub aktarım durumu

9 Kasım 2026'daki bağlantı üzerinden `isas-rov/ISAS-yazilim` deposunda dal oluşturma isteği `403 Resource not accessible by integration` ile reddedildi. Bu sorun içerik hatası değil, bağlantının GitHub App organizasyon yazma yetkisi sorunudur. Güncel izinle tekrar denenecek, doğrudan `main` üzerine yazılmayacaktır. `GitHub` aktarım ZIP'i ve patch ayrı üretildi.
