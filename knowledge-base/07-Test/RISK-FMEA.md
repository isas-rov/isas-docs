---
title: "RISK-FMEA"
created: 2026-11-09
updated: 2026-11-09
status: taslak
category: test
tags: [isas, umman, rov]
---

# Teknik risk / FMEA başlangıç defteri

| Risk | Etki | Tespit | Azaltma | Kanıt |
|---|---|---|---|---|
| Su kaçağı | Elektronik ve LiPo hasarı | Leak probe / hazne kontrol | enerjisiz test, fail-safe, kontrollü kurtarma | test logu yok |
| ESC aşırı ısınma | itki kaybı | sıcaklık ölçümü | termal tasarım ve yük testleri | test logu yok |
| Pusula bozulması | yanlış yaw | gyro–mag tutarsızlığı | harici pusula yerleşimi, motor testleri | test logu yok |
| Görsel VO kaybı | yatay konum belirsizliği | inlier/covariance/ışık | güven skoru ve düşük hız/hold | test logu yok |
| Servo/pinle Mini sıkışması | Mini çıkamaz veya düşer | tekrar test, akım/tork | mekanik fail-safe ve emniyet pimi | test logu yok |
| Batarya/konnektör | yangın/kısa devre | voltaj/akım/ısı | sigorta, E-stop, uygun şarj | test logu yok |
| Tether kopması | veri/komut kaybı | heartbeat/CRC | mekanik strain relief, görev bazlı kurtarma | test logu yok |
| Mini bırakılınca CG değişimi | kontrol sapması | eğim / havuz test | yerleşim, trim/ kontrol ayarı | test logu yok |

FMEA olasılık ve şiddet puanlarını gerçek test/operasyon tecrübesi ile birlikte daha sonra girin; şu an sayısal risk puanları varsayılmasın.
