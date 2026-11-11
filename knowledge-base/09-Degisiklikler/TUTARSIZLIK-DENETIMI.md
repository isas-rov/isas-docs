---
title: "TUTARSIZLIK-DENETIMI"
created: 2026-11-09
updated: 2026-11-09
status: belgelendi
category: degisiklik
tags: [isas, umman, rov]
---

# Kaynaklar arası çelişkiler / açıklama bekleyenler

1. **6 motor – 8 motor:** 2026 BOM 6 ana itici ve ESC; yeni sohbetler 8 tasarımı. Yeni tasarımı mevcut üretim diye yazma.
2. **Pixhawk 4 – Pixhawk 2.8:** rapor 4, eski motor testleri 2.8. Fiziksel kart ve firmware doğrula.
3. **Bar30 2mm:** çözünürlüğü mutlak doğrulukla karıştıran rapor satırları var.
4. **A02YYUW IP67:** su altı mesafe çalışması için kanıt değil; BOM ve KTR risk.
5. **2026 KTR test belgeleri:** bir paragrafta bütünleşik testler başlamadı derken ileride mm, ms, dakika ve yaşanmış olaylar anlatılıyor. Bağımsız log yok. *Olası taslak örnekler* olarak sınıflandır.
6. **Batarya:** güncel BOM ana 4S 16000 mAh; diğer KTR test kısmında 4S 10000 mAh. Güncel fiziksel etiket ve test verisi şart.
7. **EM kilit – mekanik mandal:** ikisi farklı revizyonlar; mevcut kurulu mekanizma belgelenmedi.
8. **E-Stop / failsafe:** teorik otomatik yüzeye çıkış ile 2026 bitiş alanı dışına yüzeye çıkmama kuralı çatışabilir; görev güvenlik analizi şart.
9. **Sublink + Hi-com:** BOM birden çok modül içeriyor, gerçek bağlantı/uyumluluk testi yok.
10. **Mini ROV sensörleri:** MiniROV KTR bazı ultrasonik yakınlık varsayımlarını içeriyor; su ortamına uygun sonarla karıştırma.
11. **Kod ve KTR arasında olgunluk:** KTR görsel odometri, yörünge ve kontrol iddialarını açıklıyor; incelenen GitHub kodunda MAVLink, EKF, VO ve 8 motor kontrolü görülmüyor.
12. **Ekip görevleri:** bu kasada sorumlulara görev atanmadı, kullanıcı tercihi gereği planlama sonraya bırakıldı.
