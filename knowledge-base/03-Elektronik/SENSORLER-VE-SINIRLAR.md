---
title: "SENSORLER-VE-SINIRLAR"
created: 2026-11-09
updated: 2026-11-09
status: taslak
category: elektronik
tags: [isas, umman, rov]
---

# Sensörler: ne ölçer, neyi ölçemez?

| Parça | Ölçtüğü | Ölçemediği / risk |
|---|---|---|
| Pixhawk jiroskop | açısal hız | konum değil; gyro drift birikir |
| Pixhawk ivmeölçer | özgül kuvvet | hız/konum doğrudan ölçmez; çift integrasyon hata biriktirir |
| Manyetometre | manyetik vektör | manyetik parazitte doğru baş yönü garanti değil |
| Bar30 | basınç ve sıcaklık | yatay konum ve deniz tabanına mesafe değil |
| Ön kamera | şamandıra/nesne görüntüsü | nesne görünmeden menzil/konum değil |
| Alt kamera | zemin dokusu/optik akış | metrik ölçek için zemin mesafesi/ölçek referansı gerekir |
| A02YYUW | havada ultrasonik mesafe/seviye (üretici kullanım sahası) | su altında ölçüm yaptığı doğrulanmadı; sonar yerine geçmez |
| Leak probe | su kaçağı durumuna göre elektriksel iletim | nem artışı ile doğrudan aynı şey değil |

## Bar30 önemli teknik ayrıntıları
- Blue Robotics Bar30, MS5837-30BA kullanır; eski DF13 / güncel JST GH konnektör revizyonu olabilir.
- I2C lojik seviyeleri 3.3V sınıfındadır; uzun I2C kabloları güvenilir değildir.
- Nominal derinlik **çözünürlüğü** 2 mm sınıfı diye mutlak doğruluğu ±2 mm diye yazmayın. Datasheet/üretici farklı doğruluk ve sıcaklık parametreleri verir.
- Sensörün **ön yüzü** suya, arka elektronik/konnektör tarafı sızdırmaz hazneye bakmalı.

Kaynak: https://bluerobotics.com/learn/bar-sensors-guide/ ve https://github.com/bluerobotics/Bar30-Pressure-Sensor

## Tedarik kararını etkileyen soru
DVL/sonar olmadan görüş kaybolursa hız ve yatay konum belirsizliği büyür. Bu sınırlama yazılım algoritmasının basitçe `PID` eklenmesiyle çözülmez.
