---
title: Kullanım Rehberi
status: belgelendi
updated: 2026-11-11
tags: [isas, kullanim, obsidian]
---
# Bilgi tabanı nasıl kullanılır?

## Hızlı başlangıç
1. [Ana sayfayı](../README.md) açın; önce **mevcut 2026 raporu** ile **2026 sonu tasarım önerisini** ayırın.
2. [Sistem akışlarından](../02-Sistem/GORSEL-MIMARI.md) araç ve veri zincirini öğrenin.
3. [Malzeme kayıtları](../03-Elektronik/MALZEME-DURUM-VE-NEDEN.md) ile [güncel hardware reposunu](https://github.com/isas-rov/isas-hardware) yan yana kontrol edin.
4. [Ölçüm ve kanıt eksiklerini](../06-Sorunlar/KANIT-EKSIKLERI-2026-11-11.md) kapatmadan hiçbir modülü "test edildi" olarak işaretlemeyin.
5. Test için [şablonu](../07-Test/TEST-KAYDI-SABLONU.md) çoğaltın; kullanılan yazılım SHA, donanım revizyonu, ortam, metrik ve ham log bağlantısını ekleyin.

## Etiket sistemi

| Etiket | Anlamı | Nasıl doğrulanır? |
|---|---|---|
| `BELGEDE` | Eski KTR, bütçe veya şartnamede yazıyor | Kaynak/sayfa |
| `KODDA` | İlgili repo/commit içinde kod var | Dosya/commit |
| `ÖNERİ` | Yeni tasarım, henüz doğrulanmadı | ADR + gerekçe |
| `DENEY` | Test planlandı veya kısmi ölçüm var | Log + test koşulu |
| `TEST EDİLDİ` | Kabul ölçütü ve gerçek ölçüm var | Tekrar edilebilir ham sonuç |
| `BELİRSİZ` | Parça/revizyon/beklenti henüz net değil | Açık soru / kararı bekleyen kişi |

## Kim neyi düzenlemeli?
- Envanter/maliyet: `isas-hardware` BOM kaynak dosyası güncellenince bu bilgi tabanı senkronize edilir.
- Jetson/Pixhawk/Python: `isas-software` koduna link verilir, kod kopyalanmaz.
- Teknik kararlar: `isas-docs/decisions` altında ADR oluşturulur.
- Kaynak PDF'ler: lisans ve paylaşım izni doğrulanmadan public depoya aktarılmaz.

## Obsidian ve GitHub

Bu bilgi tabanı **göreli Markdown linkleri** kullanır; GitHub üzerinden gezinilebilir. Obsidian'da da bağlantılar açılır. Teknik belgeleri çift klasöre kopyalamak yerine özgün dosyaya link verin.

## Görsel düzen

[Görsel atlas](../98-Gorseller/GORSEL-ATLAS.md) seçilmiş KTR sayfalarını gösterir; tek tek görsel alt metniyle erişilebilir. [Mimari harita](../00-Baslangic/ISAS-Mimari.canvas) Obsidian içinde açılır. Mermaid diyagramları hem GitHub hem Obsidian tarafından desteklenir.
