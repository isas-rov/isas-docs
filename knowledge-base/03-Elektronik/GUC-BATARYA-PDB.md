---
title: "GUC-BATARYA-PDB"
created: 2026-11-09
updated: 2026-11-09
status: taslak
category: elektronik
tags: [isas, umman, rov]
---

# Güç / batarya / PDB mühendislik notları

## Belgelenen ana batarya
`Leopard Power 16000mAh 14.8V 4S 25C LiPo` güncel BOM'da. Bu veriler **nominal ve liste özellikleridir**, kapasite/kalite/yük test sonucu değil.

Nominal enerji: `14.8 V × 16 Ah = 236.8 Wh` (ideal etiket hesabı). Sürücü/yük altında kullanılabilir enerji bundan düşük olabilir. 25C etiketine bakarak kablo, PDB, ESC ve hücrelerin gerçek güvenli sürekli akımı doğrulanmış kabul edilemez.

Güç hesabı şablonu: `P_toplam = Σ(V_motor×I_motor) + P_jetson + P_pixhawk + P_LED + P_haberlesme + P_kayip`. İtici akımları pervane su altında test edilerek ve üretici tablosuyla teyit edilerek girilir.

## 6→8 itici etkisi
- Ana ESC sayısı: 6 → **8 öneri**.
- Ana PDB dağıtım kolu, sigorta, kablo, batarya anlık gerilim düşümü ve ısı hesabı tekrar yapılacak.
- Şase kuvvet ve akım testleri Mini ROV takılı/takılı değil iki halde değerlendirilir.

## Besleme hijyeni
- Jetson için regülatör 5V **yükte** kararlı olmalı; 5V 3A düzeyi tek başına güvenli marj olmayabilir.
- Pixhawk power input ve servo rail gereksinimi otopilot kart revizyonuna göre incelenir; USB ile masa beslemesi gerçek araç tasarımına eşit değildir.
- Sensör beslemesi motor akım darbelerinden ayrılmalı; ortak referans ve ekranlama doğru tasarlanmalı.
- ESC'ye üç faz güç hattının sırası motorun dönüş yönünü etkiler; eşdeğer kontrol komutunu her motorda gerçek ölçümle doğrulayın.
- Ana sigorta, LiPo şarj, fiziksel güç kesici, sızıntı ve sıcaklık koruması güvenlik incelemesine girer.

## Li-ion alternatifi
Hücre nominal kapasitesinin büyüklüğü yetmez: sürekli/tepe deşarj, grup yapısı, hücre dengelemesi, kaynak, BMS/koruma, sıcaklık ve kütle/CG karşılaştırılmadan karar verilmez. **Henüz seçilmiş değil.**
