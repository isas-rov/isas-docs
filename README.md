# İSAS Dokümantasyonu

CELEBİ–UMMAN sisteminin mimarisi, alt sistemleri, kurulum süreçleri, test kayıtları ve yarışma izlenebilirliği için merkezi bilgi deposu.

## Başlangıç Noktaları

- [`index.md`](index.md): Dokümantasyon ana sayfası
- [`architecture/`](architecture/): Proje özeti ve sistem mimarisi
- [`electrical/`](electrical/): Elektrik sistemi ve bağlantı haritası
- [`subsystems/`](subsystems/): Jetson, Pixhawk, kamera, Mini ROV ve haberleşme
- [`guides/jetson/`](guides/jetson/): Jetson Nano kurulum ve kullanım rehberi
- [`procurement/`](procurement/): Envanter ve eksik parça analizi
- [`competition/`](competition/): Yarışma isterleri ve kaynak belgeler
- [`testing/`](testing/): Test planları ve sonuç kayıtları
- [`decisions/`](decisions/): Mimari karar kayıtları (ADR)
- [`reports/`](reports/): Teslim edilen teknik raporlar

## Dokümantasyon İlkeleri

- Her sayfa bir sahibi ve güncellenme bağlamı taşımalıdır.
- Karar ile varsayım birbirinden açıkça ayrılır.
- Sayısal değerler birim ve kaynakla yazılır.
- Şema/BOM/yazılım gibi başka depodaki kaynaklar kopyalanmaz; sabit bağlantıyla referans verilir.
- Test sonucu; donanım revizyonu, yazılım commit/tag ve tarih olmadan tamamlanmış sayılmaz.

## Obsidian Kullanımı

Depo Obsidian kasası olarak açılabilir. Kişisel workspace ve cache dosyaları commit edilmez. Wiki bağlantıları (`[[Sayfa-Adı]]`) ekip içi gezinme için korunur.

## Büyük Dosyalar

PDF raporlar Git LFS ile izlenir. Harici yarışma kaynağı güncellenirse dosya adı, sürüm ve erişim tarihi ilgili notta belirtilmelidir.
