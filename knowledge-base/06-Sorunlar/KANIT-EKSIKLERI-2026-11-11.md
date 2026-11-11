---
title: Doğrulama ve kanıt eksikleri
updated: 2026-11-11
status: acik
tags: [sorun, kanit, test, risk]
---
# Gerçek araca geçmeden önce doğrulanacaklar

> [!CAUTION] Test edildi ≠ dokümana yazıldı
> Bu liste teknik belirsizlik ve eksik ölçüm envanteridir; tüm maddelerin çözülmüş olduğu varsayılmaz.

| Kod | Konu | Sorun / muhtemel sonuç | Gerekli kanıt / çözüm |
|---|---|---|---|
| V-01 | 6/8 itici revizyonu | Motor geometrisi ve mixer yanlış olabilir | Ağırlık merkezi referanslı motor koordinat tablosu + test kaydı |
| V-02 | Pixhawk sürümü | PWM kanal/firmware uyumsuzluğu | Fiziksel kart fotoğrafı, firmware sürümü ve motor test logu |
| V-03 | Kamera alt modülü | OV2710–IMX335 model uyuşmazlığı | USB/CSI ürün kimliği ve sahadaki kurulum kanıtı |
| V-04 | Bar30 ve taban irtifası | Basınçtan kamera–zemin mesafesi çıkarılamaz | Havuz taban kalibrasyonu veya ilave mesafe referansı |
| V-05 | Optical Flow | Düşük doku/ışıkta XY hatası | Zemin video seti, kalibrasyon ve bağımsız ölçülen yer değiştirme |
| V-06 | Pusula | Motor akımıyla manyetik sapma | Motorlara kademeli yük verirken manyetik/yaw ölçümleri |
| V-07 | Su sızıntısı | Hazne su alabilir | Enerjisiz basınç/sızdırmazlık testi, video, tutanak |
| V-08 | Güç bütçesi | 8 motor aşırı akım/gerilim çökmesi | ESC, kablo, sigorta, batarya ölçümleri ve termal test |
| V-09 | MAVLink | Komut modu yanlış kullanım | SITL ve denetimli gerçek havuz kayıtları |
| V-10 | Mini ROV kontrol ve bırakma | Kilit mekanizması/ayrılma sırasında denge | Güvenli bırakma deneyi ve CG/CB gözlemi |
| V-11 | 2026/2027 şartname | Eski görev yeni sezona uymayabilir | Yeni sezonun resmi kural ve SSS sürüm numarası |
| V-12 | A02YYUW | Su geçirmez gövde ≠ su altında akustik sonar | Üretici veri sayfası; su altı performansı doğrulanana kadar navigasyonda kullanma |

## Ölçüm şablonu

Kayıt: `TEST-ID`, tarih, ortam, donanım sürümü, yazılım SHA, kullanılan yöntem, hedef metrik, ölçülen sonuç, ham log/video, kabul/red, takip kararı. [Test şablonu](../07-Test/TEST-KAYDI-SABLONU.md).
