---
title: "GitHub aktarım rehberi"
created: 2026-11-09
updated: 2026-11-09
status: hazir
category: yonetim
tags: [isas, umman, github]
---

# ISAS teknik dokümantasyon GitHub aktarım notu

Bu klasör `isas-rov/ISAS-yazilim` depoda **sadece `docs/` dizinine** eklenmek üzere hazırlanmıştır. Mevcut `aktif/`, `arsiv/`, `egitim/` kodlarına ve kök README'ye dokunmaz.

- Obsidian biçimindeki sayfa bağlantıları GitHub tarafından açılabilir göreli Markdown bağlantılarına çevrilmiştir.
- Orijinal PDF/DOCX/XLSX ve görsel önizlemeler **bu ZIP'te yer almaz**. Bu kopya açık depoda kişisel veya lisanslı kaynak yayımlamamak içindir.
- Sayfalardaki eski `99-Kaynaklar` dosya yolları tam yerel Obsidian arşivini tarif eder, GitHub içinde bulunmaz.
- Elektrik şemaları **kavramsal**; gerçek pinout ve üretime hazır KiCad şeması değildir.
- Kaynak KTR'lerdeki test iddiaları bağımsız log olmadan doğrulanmış sayılmaz.
- `isas-doc` isimli ayrı depo bağlı GitHub uygulamasına görünmediğinden bu paketin hedefi teyit edilmelidir.

## Önerilen Git yöntemi

```bash
git clone https://github.com/isas-rov/ISAS-yazilim.git
cd ISAS-yazilim
git switch -c docs/obsidian-knowledge-base-2026-11-09
# ZIP içindeki docs klasörünün tümünü depo köküne kopyalayın
git add docs
git commit -m 'docs: add reviewed ISAS Obsidian knowledge base'
git push -u origin docs/obsidian-knowledge-base-2026-11-09
# Sonra PR açın; main dalına doğrudan push etmeyin.
```

Bu adımlar kullanıcıya ait yazma izni bulunan Git ortamında yapılmalıdır.
