---
tags: [jetson, ssh, ip, uzaktan-erisim]
---

# IP, SSH ve Başka Bilgisayardan Bağlanma

## SSH Nedir?

SSH, Jetson terminalini ağ üzerinden güvenli ve şifreli olarak kullanma yöntemidir. Varsayılan TCP portu `22`'dir.

## 1. Jetson SSH Hizmetini Kontrol Et

Jetson'da:

```bash
sudo systemctl status ssh
```

`active (running)` beklenir. Kurulu değilse ve internet varsa:

```bash
sudo apt install openssh-server
```

```bash
sudo systemctl enable --now ssh
```

## 2. Hangi IP'yi Kullanacağını Seç

Jetson'da:

```bash
hostname -I
```

Birden fazla IP görülebilir:

| IP                   | Anlamı                       | Ne zaman kullanılır?                     |
| -------------------- | ---------------------------- | ---------------------------------------- |
| `192.168.55.1`       | NVIDIA USB Device Mode       | Windows USB tarafı `192.168.55.100` iken |
| `192.168.137.2`      | Windows ICS/PdaNet yerel ağı | Windows Ethernet `192.168.137.1` iken    |
| `172.17.0.1`         | Docker bridge                | Bilgisayardan SSH için kullanılmaz       |
| Router'ın verdiği IP | Normal LAN                   | Bilgisayar da aynı router'daysa          |

## 3. `192.168.137.2` Adresini Jetson'a Ver

PuTTY seri konsolda:

```bash
sudo ip address replace 192.168.137.2/24 dev l4tbr0
```

Kısaltma tanımlıysa:

```bash
jetip
```

Kontrol:

```bash
hostname -I
```

> [!note]
> `replace`, aynı adres varsa hata vermeden günceller; yoksa ekler. `add` tekrar çalıştırıldığında `File exists` verebilir.

## 4. Windows IP'sini Kontrol Et

Windows PowerShell:

```powershell
Get-NetIPAddress -InterfaceAlias "Ethernet" -AddressFamily IPv4
```

Beklenen:

```text
IPAddress      : 192.168.137.1
PrefixLength   : 24
AddressState   : Preferred
```

## 5. Windows'tan Bağlantı Testi

```powershell
ping 192.168.137.2
```

Başarılıysa:

```powershell
ssh jetson@192.168.137.2
```

İlk bağlantıda:

```text
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Tam kelimeyi yaz:

```text
yes
```

Parola yazılırken karakter görünmez.

## 6. Varsayılan USB Adresiyle SSH

Windows USB adaptörü `192.168.55.100` ise:

```powershell
ping 192.168.55.1
ssh jetson@192.168.55.1
```

Bu yol internet gerektirmez.

## 7. Normal Router'daki Başka Bilgisayardan Bağlanma

Koşullar:

1. Jetson ve diğer bilgisayar aynı modem/router'a bağlı olmalı.
2. Jetson'ın LAN IP'si bulunmalı.
3. Router'da istemci izolasyonu olmamalı.
4. SSH hizmeti çalışmalı.

Jetson:

```bash
ip -4 address
ip route
```

Örnek LAN IP `192.168.1.45` ise diğer bilgisayarda:

```bash
ssh jetson@192.168.1.45
```

Linux/macOS/Windows OpenSSH'ta komut aynıdır.

## 8. Başka Bilgisayarı Doğrudan USB ile Bağlama

1. Jetson Micro-USB veri kablosunu yeni bilgisayara tak.
2. Yeni bilgisayarın USB Ethernet ve seri sürücülerini tanımasını bekle.
3. Bilgisayarın USB ağ IP'sini kontrol et.
4. NVIDIA varsayılan planı oluştuysa `192.168.55.1` ile bağlan.
5. Windows ICS planı gerekiyorsa o bilgisayarda `192.168.137.1/24`, Jetson'da `192.168.137.2/24` yapılandır.

Bir Micro-USB device-mode bağlantısı aynı anda fiziksel olarak tek ana bilgisayara gider. Yeni bilgisayarda IP ve güvenlik duvarı ayarları ayrıdır.

## 9. Host Key Değişti Hatası

Jetson yeniden imajlandıysa SSH anahtarı değişir. Gerçekten aynı cihaz olduğunu seri konsoldan doğruladıktan sonra Windows'ta:

```powershell
ssh-keygen -R 192.168.137.2
```

Sonra yeniden SSH kur.

## 10. Hata Anlamları

### `Connection timed out`

- Yanlış IP
- Cihazlar aynı alt ağda değil
- USB ağ adaptörü kopuk
- SSH trafiği engelleniyor

### `Connection refused`

IP'ye ulaşılıyor fakat SSH hizmeti o adreste dinlemiyor.

### `Permission denied`

- Kullanıcı adı/parola yanlış
- Mevcut cihazın kullanıcısı `jetson`; `waveshare` değil
- Klavye dili/parola karakteri farkı olabilir

## 11. İnternet Üzerinden Uzak Erişim

> [!danger] SSH/VNC portunu doğrudan internete açma
> Router'da 22 veya 5901 port yönlendirmesi yapmak cihazı parola saldırılarına açar. Dış ağdan erişim gerekiyorsa Tailscale/WireGuard gibi kimlik doğrulamalı VPN tasarımı kullan ve VNC'yi SSH tüneli arkasında tut.
