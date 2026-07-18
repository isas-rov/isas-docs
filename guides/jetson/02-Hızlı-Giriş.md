---
tags: [jetson, hizli-baslangic, checklist]
---

# Hızlı Giriş

Bu not, ayrıntıya girmeden günlük açılış sırasını verir. Bir adım çalışmazsa [[15-Arıza-Çözme]] notuna git.

## A. PdaNet ile Günlük Açılış

### Windows tarafı

- [ ] Telefonu PdaNet ile Windows'a bağla.
- [ ] Windows tarayıcısından interneti kontrol et.
- [ ] Jetson'ın Micro-USB veri kablosunun takılı olduğunu kontrol et.
- [ ] Windows IP'sini kontrol et:

```powershell
Get-NetIPAddress -InterfaceAlias "Ethernet" -AddressFamily IPv4
```

Beklenen:

```text
IPAddress : 192.168.137.1
```

- [ ] PowerShell, CMD veya Git Bash'te proxy'yi başlat:

```text
jetproxy
```

Beklenen:

```text
Jetson APT proxy hazir: ('192.168.137.1', 3128)
```

Bu pencereyi kapatma.

### Jetson tarafı

PuTTY seri konsolda veya mevcut SSH oturumunda:

```bash
jetip
```

```bash
hostname -I
```

Beklenen adreslerden biri:

```text
192.168.137.2
```

SSH ile bağlan:

```powershell
ssh jetson@192.168.137.2
```

VNC sunucusunu başlat:

```bash
vncgui
```

TigerVNC Viewer adresi:

```text
192.168.137.2:1
```

İnternet/depoyu kontrol et:

```bash
sudo apt update
```

> [!note]
> PdaNet proxy yönteminde `ping 1.1.1.1` çalışmayabilir. `apt update` ve Chromium'ın çalışması asıl testtir.

## B. Normal Modem/Router ile Hızlı Açılış

PdaNet proxy ayarı açıksa önce [[07-Normal-İnternet#PdaNet proxy'sinden normal internete geçiş]] bölümünü uygula.

- [ ] Ethernet kablosunu Jetson ile modeme/router'a tak.
- [ ] Jetson'da:

```bash
nmcli device status
hostname -I
ip route
```

- [ ] `eth0` için router'dan gelen IP'yi bul.
- [ ] Aynı router'daki bilgisayardan:

```powershell
ssh jetson@JETSON_LAN_IP
```

- [ ] VNC:

```text
JETSON_LAN_IP:1
```

Bu senaryoda `jetip` ve Windows `jetproxy` gerekmez.

## C. Yalnızca USB ile Hızlı Bağlantı

Windows tarafında NVIDIA USB ağ adaptörü `192.168.55.100`, Jetson `192.168.55.1` ise:

```powershell
ping 192.168.55.1
ssh jetson@192.168.55.1
```

VNC:

```text
192.168.55.1:1
```

Bu bağlantı, internet paylaşımı olmadan yalnızca bilgisayar–Jetson iletişimi sağlar.

## D. Ağ Hiç Çalışmıyorsa

PuTTY ile seri konsola dön:

```text
Connection type: Serial
Serial line: COM5
Speed: 115200
```

Oturum aç:

```text
login: jetson
password: <Jetson parolası>
```

Sonra:

```bash
hostname -I
ip -br address
ip route
```

## E. Güvenli Kapatma

Jetson terminalinde:

```bash
sudo poweroff
```

Terminal kapandıktan ve kartın etkinlikleri durduktan sonra gücü kes. CSI kamera, SD kart ve fan kablosunu cihaz enerjiliyken söküp takma.
