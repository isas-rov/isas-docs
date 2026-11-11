---
title: "BOM-BUTCE-OZETI"
created: 2026-11-09
updated: 2026-11-09
status: belgeden-aktarim
category: donanim
tags: [isas, umman, rov]
---

# Bütçe özeti — çalışma kitabıyla karşılaştırıldı

**Tek veri kaynağı:** `UMMAN-MALZEME-GUNCELxlsx.xlsx`, `Ana Gider Listesi`, `150K Denizaltı Giderleri`, `50K Elektronik Giderleri` ve `Bütçe Özeti` sayfaları. Tutarlar **planlanan malzeme listesi fiyatlarıdır**; gerçek harcama, satın alma veya mevcut stok değeri değildir.

| Bölüm | Hedef bütçe | Alt listedeki 2026 toplamı | Hedefe göre fark |
|---|---:|---:|---:|
| 150K Denizaltı Giderleri | 150.000,00 TL | 149.035,64 TL | 964,36 TL altında |
| 50K Elektronik Giderleri | 50.000,00 TL | 42.131,10 TL | 7.868,90 TL altında |
| **Genel plan** | **200.000,00 TL** | **191.166,74 TL** | **8.833,26 TL altında** |

**Hesap yöntemi:** Alt listelerde adet × birim fiyat yerine doğrudan `TOPLAM MALİYET (TL)` sütunundaki satır toplamları toplanmıştır. `Ana Gider Listesi`, iki alt listenin birleşimidir; **üç ayrı liste toplanmaz**. Excel `Bütçe Özeti` sayfasındaki `C4/C5/C6` hücreleri alt sayfaların genel toplam hücrelerine formülle bağlıdır; kullanılan okuyucu önbellekli sonuçları döndürmediği için rakamlar 150K/50K satır toplamlarından ayrıca doğrulanmıştır.

## 6 → 8 ana itici değişikliğinin tahmini maliyet etkisi

Kaynak çalışma kitabında 6 Mitras iticinin satır toplamı **39.602,88 TL**, 6 Blu 30A ESC'nin satır toplamı **5.124,00 TL** olarak yer alır. Birim bedel sabit kalırsa:

- İtici birim maliyeti: 39.602,88 / 6 = **6.600,48 TL**.
- ESC birim maliyeti: 5.124,00 / 6 = **854,00 TL**.
- **2 ek itici + 2 ek ESC = 14.908,96 TL** (yalnız referans fiyat hesabı).
- Diğer her kalem ve bedel aynı kalırsa yeni toplam **206.075,70 TL**, 200K hedefinin **6.075,70 TL üzerinde** olur.

Bu değer **satıcı teklifi veya nihai bütçe değil**. 8 ESC'ye uygun PDB, penetratör, kablo, koruma, batarya yükü, şase revizyonu ve yeni fiyatlar ayrıca hesaplanmalıdır. Mevcut BOM'da 8 iticili tasarım için henüz onaylanmış revizyon yoktur.

## Bütçe kararından önce doğrulanacaklar

- [ ] Gerçekte satın alınmış ve elde bulunan stok ayrıştırılacak.
- [ ] 8 motor için güncel birim fiyat/tedarikçi teklifi alınacak.
- [ ] Akım, kablo, PDB, batarya ve penetratör revizyonu maliyetlenecek.
- [ ] 150K / 50K bütçe sınıflandırması yeni tasarıma göre güncellenecek.

İlgili: [MALZEME-ANA-LISTE](MALZEME-ANA-LISTE.md) · [GUC-BATARYA-PDB](GUC-BATARYA-PDB.md) · [TUTARSIZLIK-DENETIMI](../09-Degisiklikler/TUTARSIZLIK-DENETIMI.md)
