---
title: "HAZNE-SIZDIRMAZLIK"
created: 2026-11-09
updated: 2026-11-09
status: taslak
category: mekanik
tags: [isas, umman, rov]
---

# Hazneler / penetratörler / sızdırmazlık

**BOM:** H-100 (ana), H-60, Mucif/Degz Neo penetratörler, conta/O-ring ve optik kubbe/kapak gibi bileşenler listeleniyor. `H-100` içinde Jetson'ın USB/CSI konnektörleri dahil paketlenmesi doğrulanmalı.

## Riskler ve tedbirler
- Haznenin **iç çapı** kart PCB ölçüsünden büyük olsa da USB fişi, standoff, kablo çıkışı ve ısıl boşluk sığmayabilir.
- Penetratör malzemesi, diş, O-ring, sıkma torku, kablo dış çapı ve basınç sınıfı üretici dökümanıyla doğrulanır.
- Nem emici silica gel yalnız yoğuşmayı azaltabilir; **su sızıntısını onarmaz**.
- ESC epoksi gömme ısı dağılımını bozabilir; gerçek sıcaklık ve malzeme uyumu test edilmeden yapılmaz.
- Her yeni delik kablo/kapak/conta için yeni sızıntı potansiyelidir; minimum penetrasyon tercih edilir.

## Test sırası
1. Boş muhafaza + kağıt/hassas nem etiketi ile enerjisiz sızdırmazlık denemesi.
2. Gerekli durumda kontrollü basınç/vakum ve üretici prosedürü.
3. Dış elektrik/güç bağlantıları izole kuru test.
4. Kontrollü sığ su test, gözlemci ve kurtarma mekanizması.
5. Elektronik enerjili düşük akım test ancak yukarıdaki koşullardan sonra.

Kaydedilecek: `hazne_id, delik_id, O-ring tipi, sıkma yöntemi, basınç/derinlik, süre, sıcaklık, sızıntı, fotoğraf`.
