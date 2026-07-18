---
tags: [jetson, pdanet, proxy, internet, windows]
---

# PdaNet Proxy ile Jetson'a İnternet Verme

## Neden Proxy Gerekti?

Mevcut sistemde:

- Windows, PdaNet üzerinden internete çıkabiliyor.
- `Test-NetConnection www.google.com -Port 443` sonucu başarılı.
- Windows ICS hizmeti `Running` ve Windows USB IP'si `192.168.137.1`.
- Windows, Jetson `192.168.137.2` adresine ping atabiliyor.
- Buna karşın Jetson'dan doğrudan `1.1.1.1:80` TCP bağlantısı zaman aşımına uğruyor.

Bu nedenle Windows üzerinde, Jetson'dan gelen HTTP/HTTPS isteklerini PdaNet'e taşıyan yerel bir proxy oluşturuldu.

```text
Jetson uygulaması
      ↓ HTTP/HTTPS proxy
192.168.137.2
      ↓ USB ağı
Windows 192.168.137.1:3128
      ↓ PdaNet
Telefon interneti
```

## Adresler

| Rol | Adres |
|---|---|
| Windows–Jetson USB tarafı | `192.168.137.1` |
| Jetson | `192.168.137.2` |
| Proxy | `http://192.168.137.1:3128` |
| PdaNet'in kendi dinamik adresi | Değişebilir; ayarlara yazılmaz |

PdaNet IP'si her bağlantıda değişse bile proxy Windows'ın sabit Jetson tarafına bağlı olduğu için ayar değişmez.

## 1. Windows IP Kontrolü

PowerShell:

```powershell
Get-NetIPAddress -InterfaceAlias "Ethernet" -AddressFamily IPv4
```

Beklenen:

```text
IPAddress    : 192.168.137.1
PrefixLength : 24
```

Jetson:

```bash
jetip
hostname -I
```

Beklenen adres:

```text
192.168.137.2
```

## 2. Proxy Programı

Dosya Windows'ta:

```text
C:\Users\kolay\Desktop\İSAS\jetson_apt_proxy.py
```

Bundled Python:

```text
C:\Users\kolay\.cache\codex-runtimes\codex-primary-runtime\dependencies\python\python.exe
```

Proxy yalnızca Windows `192.168.137.1:3128` adresinde dinler ve yalnızca Jetson `192.168.137.2` istemcisini kabul eder.

## 3. Windows Güvenlik Duvarı

Yönetici PowerShell'de bir kez:

```powershell
New-NetFirewallRule -DisplayName "Jetson APT Proxy" -Direction Inbound -Action Allow -Protocol TCP -LocalAddress 192.168.137.1 -LocalPort 3128 -RemoteAddress 192.168.137.2
```

Kuralı kontrol et:

```powershell
Get-NetFirewallRule -DisplayName "Jetson APT Proxy"
```

## 4. Proxy'yi Başlat

Uzun komut:

```powershell
& "C:\Users\kolay\.cache\codex-runtimes\codex-primary-runtime\dependencies\python\python.exe" "C:\Users\kolay\Desktop\İSAS\jetson_apt_proxy.py"
```

Kısaltma:

```text
jetproxy
```

PowerShell, CMD veya Git Bash alternatiflerinden yalnızca birinde çalıştır. Aynı anda iki proxy başlatılırsa `address already in use` / `WinError 10048` gelir.

Beklenen:

```text
Jetson APT proxy hazir: ('192.168.137.1', 3128)
Durdurmak icin Ctrl+C basin.
```

Pencere açık kalmalıdır.

## 5. Jetson'dan Proxy Portunu Test Et

```bash
python3 -c "import socket; s=socket.create_connection(('192.168.137.1',3128),5); print('PROXY PORTU ACIK'); s.close()"
```

Beklenen:

```text
PROXY PORTU ACIK
```

Gerçek HTTP testi:

```bash
python3 -c "import urllib.request; p=urllib.request.ProxyHandler({'http':'http://192.168.137.1:3128','https':'http://192.168.137.1:3128'}); o=urllib.request.build_opener(p); r=o.open('http://ports.ubuntu.com/ubuntu-ports/dists/bionic/InRelease',timeout=20); print('HTTP:',r.status); r.close()"
```

Beklenen:

```text
HTTP: 200
```

## 6. APT Proxy Ayarı

Dosya:

```text
/etc/apt/apt.conf.d/95pdanet-proxy
```

İçerik:

```text
Acquire::http::Proxy "http://192.168.137.1:3128/";
Acquire::https::Proxy "http://192.168.137.1:3128/";
```

Oluşturma komutu:

```bash
printf 'Acquire::http::Proxy "http://192.168.137.1:3128/";\nAcquire::https::Proxy "http://192.168.137.1:3128/";\n' | sudo tee /etc/apt/apt.conf.d/95pdanet-proxy
```

Kontrol:

```bash
cat /etc/apt/apt.conf.d/95pdanet-proxy
sudo apt update
```

Doğrulanmış başarılı depolar:

```text
http://ports.ubuntu.com/ubuntu-ports
https://repo.download.nvidia.com/jetson/common
https://repo.download.nvidia.com/jetson/t210
```

## 7. Genel HTTP/HTTPS Proxy Ayarı

Dosya:

```text
/etc/profile.d/pdanet-proxy.sh
```

İçerik:

```bash
export http_proxy="http://192.168.137.1:3128/"
export https_proxy="http://192.168.137.1:3128/"
export HTTP_PROXY="$http_proxy"
export HTTPS_PROXY="$https_proxy"
export no_proxy="localhost,127.0.0.1,192.168.55.1,192.168.137.1,192.168.137.2"
export NO_PROXY="$no_proxy"
```

Mevcut terminalde yükle:

```bash
source /etc/profile.d/pdanet-proxy.sh
```

Kontrol:

```bash
env | grep -i proxy
```

Yeni VNC/oturumdan sonra Chromium, `pip`, `git`, `wget` ve proxy ortam değişkenlerini destekleyen programlar bu ayarı kullanabilir.

Chromium'u mevcut terminalden test etmek için:

```bash
pkill -f chromium
chromium-browser &
```

Gerekirse kesin parametre:

```bash
chromium-browser --proxy-server="http://192.168.137.1:3128" &
```

## 8. Windows Kısaltmaları

### PowerShell

PowerShell `$PROFILE` içindeki fonksiyon:

```powershell
function jetproxy { & "C:\Users\kolay\.cache\codex-runtimes\codex-primary-runtime\dependencies\python\python.exe" "C:\Users\kolay\Desktop\İSAS\jetson_apt_proxy.py" }
```

Kontrol:

```powershell
Get-Command jetproxy
```

### CMD

Dosya:

```text
C:\Users\kolay\bin\jetproxy.cmd
```

Kontrol:

```cmd
where jetproxy
```

### Git Bash

Git Bash `~/.bashrc`:

```bash
alias jetproxy='"/c/Users/kolay/.cache/codex-runtimes/codex-primary-runtime/dependencies/python/python.exe" "/c/Users/kolay/Desktop/İSAS/jetson_apt_proxy.py"'
```

Kontrol:

```bash
type jetproxy
```

## 9. Proxy'nin Sınırları

Proxy ile çalışanlar:

- APT HTTP/HTTPS depoları
- Chromium web trafiği
- `pip`, `git`, Python `requests/urllib` gibi proxy destekleyen istemciler
- HTTPS `CONNECT` tüneli kullanan uygulamalar

Doğrudan çalışmayabilecekler:

- ICMP/ping
- UDP
- NTP saat eşleme
- Ham MQTT/RTSP/oyun protokolleri
- Docker daemon (ayrı servis proxy ayarı ister)
- Proxy desteği olmayan özel SDK'lar

Pixhawk seri bağlantısı, CSI kamera, GPIO, fan, CUDA ve yerel VNC bu proxy'den etkilenmez.

## 10. Kapatma ve Normal İnternete Dönüş

Windows proxy penceresinde:

```text
Ctrl+C
```

Jetson ayarlarını devre dışı bırakmak için [[07-Normal-İnternet#PdaNet proxy'sinden normal internete geçiş]] bölümünü uygula.

## 11. Hata Tablosu

| Belirti | Olası neden | Kontrol |
|---|---|---|
| `Connection refused` | Proxy çalışmıyor | Windows'ta `jetproxy` |
| `timed out` | IP/firewall/USB bağlantısı | `ping 192.168.137.2`, port testi |
| `WinError 10048` | Proxy zaten açık | İkinci kopyayı kapat |
| APT proxy'ye ulaşamıyor | Windows Ethernet IP'si değişmiş | `Get-NetIPAddress` |
| Chromium direkt bağlanıyor | Oturum eski ortamı kullanıyor | Yeniden login/VNC veya `--proxy-server` |
| PdaNet yeniden bağlandı | Devam eden indirme koptu | `apt`/indirmeyi yeniden çalıştır |
