---
tags: [jetson, putty, serial, kurtarma]
---

# Seri Konsol ve PuTTY

Seri konsol, IP adresi veya internet gerektirmeden Jetson'a ulaşmanı sağlar. Ağ ayarı bozulduğunda en güvenilir kurtarma yoludur.

## Seri Konsol ile SSH Arasındaki Fark

| Özellik | Seri konsol | SSH |
|---|---|---|
| Fiziksel yol | Micro-USB seri cihaz | Ağ |
| IP gerekir mi? | Hayır | Evet |
| Port/ayar | `COM5`, 115200 baud | IP, TCP 22 |
| Ağ bozukken | Çalışır | Çalışmaz |
| Hız | Terminal için yeterli | Daha hızlı |

## 1. Windows'ta COM Portunu Bul

Aygıt Yöneticisi → `Bağlantı Noktaları (COM ve LPT)` altında:

```text
USB Seri Cihaz (COM5)
```

PowerShell alternatifi:

```powershell
Get-CimInstance Win32_SerialPort | Format-Table DeviceID,Name,PNPDeviceID
```

Mevcut cihazda görülen USB kimliği:

```text
VID_0955&PID_7020&MI_02
```

COM numarası başka USB portuna takıldığında değişebilir. Her zaman yeniden kontrol edilebilir.

## 2. PuTTY Ayarı

PuTTY ana ekranında:

```text
Connection type: Serial
Serial line: COM5
Speed: 115200
```

`Connection → Serial` altında:

```text
Data bits: 8
Stop bits: 1
Parity: None
Flow control: None
```

`Open` butonuna bas. Siyah ekran gelirse bir kez `Enter` tuşuna bas.

## 3. Oturum Açma

Beklenen ekran:

```text
Ubuntu 18.04.6 LTS jetson-desktop ttyGS0

jetson-desktop login:
```

Kullanıcı:

```text
jetson
```

Parolayı yazarken ekranda yıldız veya karakter görünmez. Bu normaldir. Parolayı yazıp `Enter` bas.

Başarılı giriş:

```text
jetson@jetson-desktop:~$
```

## 4. İlk Tanılama Komutları

```bash
hostname -I
```

```bash
ip -br address
```

```bash
ip route
```

```bash
findmnt -n -o SOURCE /
```

```bash
df -h /
```

## 5. PuTTY'de Kopyalama/Yapıştırma

- PuTTY'de metni fareyle seçmek genellikle Windows panosuna kopyalar.
- PuTTY penceresine sağ tıklamak panodaki metni yapıştırabilir.
- Uzun komutu yapıştırmadan önce doğru terminalde olduğunu kontrol et.
- `PS C:\...>` ile başlayan Windows satırını Jetson'a yapıştırma.
- `jetson@...$` metnini komutla birlikte kopyalama.

## 6. `Ctrl+C` Ne Yapar?

Terminalde `Ctrl+C`, o anda ön planda çalışan komuta kesme sinyali gönderir. Ekranda `^C` görülmesi normaldir.

`sudo reboot` sonrası terminal yanıt vermiyorsa sistem yeniden başlıyor olabilir. Seri bağlantı yeniden oluştuğunda PuTTY'yi kapatıp yeni COM portuyla tekrar açmak gerekebilir.

## 7. Hiç Yazı Gelmiyorsa

1. Micro-USB kablonun veri kablosu olduğunu kontrol et.
2. COM numarasını yeniden bul.
3. PuTTY hızının `115200` olduğunu kontrol et.
4. Flow control'u `None` yap.
5. Jetson'a ayrı ve yeterli güç geldiğini kontrol et.
6. Farklı USB portu/kablo dene.
7. Aygıt Yöneticisi'nde sarı uyarı olup olmadığına bak.

## 8. Seri Konsolun Güvenlik Rolü

Seri konsol fiziksel erişim gerektirir. Araç sahada kapalıyken Micro-USB portuna fiziksel erişimi kontrol altında tut. Parola ve seri konsol kayıtlarında gizli anahtar bırakma.
