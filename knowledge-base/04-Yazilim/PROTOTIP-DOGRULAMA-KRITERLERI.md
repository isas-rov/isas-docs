---
title: "PROTOTIP-DOGRULAMA-KRITERLERI"
created: 2026-11-09
updated: 2026-11-09
status: taslak
category: yazilim
tags: [isas, umman, rov]
---

# Kör uçuş prototipi — doğrulama ve başarı kriterleri

**Bu sayfa yapılacak iş ataması değil**, sistemin hangi kanıtlarla güvenilir kabul edilebileceğine dair mühendislik ölçüm rehberidir. Sayısal eşikler başlangıç önerisidir; şartname sonucu veya elde edilmiş test sonucu sayılmaz.

## Veri arayüzü asgari koşulları

| Kaynak | Kayıt | Neden |
|---|---|---|
| Pixhawk IMU | Timestamp, açısal hız, ivme, quaternion, estimator durumu | Dönüş düzeltme ve sensör sağlığı |
| Bar30 | Timestamp, basınç, derinlik, sensör durumu | Derinlik kontrolü |
| Alt kamera | Kare zamanı, çözünürlük, kalibrasyon, özellik/eşleşme sayısı | Görsel odometri değerlendirmesi |
| Ön kamera | Kare zamanı, tespit kutusu, güven skoru | Şamandıra/alan görsel güdümü |
| Pixhawk/ESC | Hedef kontrol komutları, motor çıkışları, batarya V/A | Komut–gerçek davranış analizi |
| Dış referans | Havuz grid'i, marker veya dış kamera ile ölçülen X/Y | Görsel konum tahminini bağımsız karşılaştırma |

**Zaman senkronizasyonu:** Farklı cihazların saatini doğrudan eşitlemeden kare zamanı ile IMU zamanı aynı kabul edilmez. `camera-to-body` eksen dönüşümü ayrıca kalibre edilir.

## Testlerin geçme mantığı

1. **Optical Flow yön testi:** Kamera bilinen yatay yönlerde hareket ettirilir. Algoritmanın yön işareti ve kararlılığı gerçek hareketle karşılaştırılır.
2. **Ölçek testi:** Aynı hareket farklı kamera–zemin yüksekliklerinde tekrar edilir. Sonar/DVL olmadan **zemin mesafesi bilinmiyorsa metrik hız verilmez**; güven bilgisi düşürülür.
3. **Yön kontrolü:** Motor açık/kapalı ve farklı akım durumlarında baş yönü/tutarsızlık kaydı incelenir.
4. **Derinlik kontrolü:** Hedef ve ölçülen derinlik zamana göre grafiğe çizilir. Taşma, yerleşme süresi ve kalıcı hata raporlanır.
5. **Teach & Repeat:** Kaydedilen PWM'nin değil, harici referansla kontrol edilen **yeniden izlenen yörüngenin** sapması ölçülür.
6. **Görsel hedef takibi:** Şamandıra tespiti başarı/yanlış pozitif/yaklaşma hızı ve kamera görüş kaybı durumlarında değerlendirilir.
7. **Güvenlik:** VO, pusula veya Jetson kaybolduğunda simülasyonda ve kontrollü havuzda tanımlanmış güvenli tepki görülür.

## Kabul kararında mutlaka aranan kanıtlar

- Test tarihi, araç revizyonu, ortam (havuz/deniz) ve katılanlar.
- Ham video + sensör/motor CSV ya da binary log + kullanılan yazılım commit SHA'sı.
- Bağımsız referansa göre hata grafikleri. **Hata ölçülmüyorsa 'başarılı' hükmü verilmez.**
- Başarısız tekrarlar da saklanır; sıfırdan yeni logla performans değerlendirilir.

İlgili: [TEST-STRATEJISI](../07-Test/TEST-STRATEJISI.md) · [TEST-KAYDI-SABLONU](../07-Test/TEST-KAYDI-SABLONU.md) · [KOR-UCUS-MIMARISI](KOR-UCUS-MIMARISI.md)
