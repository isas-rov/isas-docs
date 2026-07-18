---
tags: [jetson, sorun-giderme, troubleshooting]
---

# Arıza Çözme

## Altın Kural: Katman Katman İlerle

```text
Güç
 ↓
Boot / seri konsol
 ↓
Yerel IP bağlantısı
 ↓
SSH / VNC
 ↓
İnternet / proxy
 ↓
Uygulama / Python / donanım
```

Üst katmana geçmeden alt katmanı doğrula.

## 1. Jetson Açılmıyor Gibi

1. Güç LED'ini kontrol et.
2. 5 V / 4 A kaynağı ve konektörü kontrol et.
3. PuTTY seri konsolu `COM5`, `115200` ile aç.
4. COM portunun yeniden numaralanıp numaralanmadığını kontrol et.
5. SD kart takılı mı kontrol et; mevcut boot SD kökü bekliyor.
6. 15 dakikalık sessizlik normal değilse seri logu incele; gücü rastgele kesmeden önce boot durumunu anla.

## 2. `sudo reboot` Sonrası Terminal Dondu

`reboot`, mevcut oturumu kapatır. Seri/SSH terminalinin yanıt vermemesi normaldir. Yeni boot için:

- Seri COM portunu yeniden aç.
- USB ağ adaptörünün yeniden gelmesini bekle.
- IP adresini yeniden kontrol et.
- SSH/VNC'yi yeniden bağla.

## 3. `command not found`

### Prompt kopyalandı

Yanlış:

```bash
jetson@jetson-desktop:~$ hostname -I
```

Doğru:

```bash
hostname -I
```

### Windows komutu Jetson'a yazıldı

`Get-NetIPAddress` PowerShell komutudur; Jetson Bash'te çalışmaz.

### Yazım hatası

Yanlış: `i route`, `nmcli device statu`, `target-pwm`.

Doğru:

```bash
ip route
nmcli device status
/sys/devices/pwm-fan/target_pwm
```

## 4. Alias `command not found`

```bash
grep -n "alias jetip" ~/.bashrc ~/.bash_aliases 2>/dev/null
source ~/.bashrc
type jetip
```

PowerShell/CMD/Git Bash/Jetson alias dosyalarını karıştırma.

## 5. IP Var ama SSH Yok

Windows:

```powershell
ping 192.168.137.2
Test-NetConnection 192.168.137.2 -Port 22
```

Jetson seri konsol:

```bash
sudo systemctl status ssh
sudo ss -lntp | grep ':22'
```

## 6. `Connection timed out`

```bash
hostname -I
ip -br address
ip route
```

Windows:

```powershell
Get-NetIPAddress -AddressFamily IPv4 | Format-Table InterfaceAlias,IPAddress,PrefixLength
```

Windows `192.168.137.1/24`, Jetson `192.168.137.2/24` olmalı. Aynı IP iki cihaza verilmemeli.

## 7. `Permission denied (publickey,password)`

- Kullanıcı: `jetson`.
- Parola yazarken karakter görünmez.
- Klavye dili ve Caps Lock kontrol edilir.
- Seri konsolda aynı parola denenir.
- `waveshare` kullanıcı adı mevcut cihazda yanlıştır.

## 8. VNC Bağlanmıyor

```bash
vncserver -list
```

Yoksa:

```bash
vncserver :1 -geometry 1280x720 -depth 24 -localhost no
```

Doğru adres:

```text
192.168.137.2:1
```

`:1`, IP'nin parçası değil; VNC ekran numarasıdır.

Log:

```bash
tail -n 100 ~/.vnc/jetson-desktop:1.log
```

## 9. `stale` VNC Oturumu

```bash
vncserver -kill :1
vncserver :1 -geometry 1280x720 -depth 24 -localhost no
```

Yeni başlatma stale PID'i otomatik temizleyebilir.

## 10. Jetson'da İnternet Yok

### Normal router/ICS

```bash
ip route
ip route get 1.1.1.1
ping -c 3 1.1.1.1
ping -c 3 google.com
```

- IP çalışıp alan adı çalışmıyorsa DNS.
- İkisi de çalışmıyorsa route/NAT/bağlantı.

### PdaNet proxy

Ping çalışmayabilir. Test:

```bash
python3 -c "import socket; s=socket.create_connection(('192.168.137.1',3128),5); print('PROXY ACIK'); s.close()"
```

```bash
sudo apt update
```

Windows'ta `jetproxy` penceresi açık olmalı.

## 11. Chromium `DNS_PROBE_FINISHED_NO_INTERNET`

PdaNet proxy senaryosunda Chromium doğrudan çıkıyorsa:

```bash
source /etc/profile.d/pdanet-proxy.sh
pkill -f chromium
chromium-browser --proxy-server="http://192.168.137.1:3128" &
```

Yeni VNC/login oturumu genel proxy ortamını miras alır.

## 12. APT `Could not resolve`

Normal ağda DNS'i kontrol et. PdaNet'te APT proxy dosyasını kontrol et:

```bash
cat /etc/apt/apt.conf.d/95pdanet-proxy
```

Proxy port testi yap. Doğrudan `/etc/resolv.conf` değiştirmek PdaNet proxy senaryosunda gerekli değildir; proxy DNS'i Windows tarafında çözer.

## 13. `nvidia-jetpack` Bağımlılık Çakışması

JetPack meta paketi, alt paketlerin aynı `4.6.5-b29` sürümünü bekledi. Depo varsayılanı `4.6.6-b24` seçtiğinde unmet dependencies oluştu. Çözüm, meta paketle birlikte alt NVIDIA paketlerini aynı sürüme sabitlemekti.

Kurulu sürümler:

```bash
dpkg-query -W nvidia-jetpack nvidia-cuda nvidia-cudnn8 nvidia-tensorrt
```

Yeni bir JetPack/L4T karışımı yapmadan önce simülasyon:

```bash
apt-get -s install PAKET
```

`-s`, gerçek kurulum yapmadan planı gösterir.

## 14. CUDA `helper_cuda.h` Yok

Yalnızca `deviceQuery` alt klasörünü kopyalamak `../../common/inc` yolunu bozar. Tüm `cuda-samples` ağaç yapısı korunmalıdır.

## 15. Fan Dönmüyor

```bash
cat /sys/devices/pwm-fan/target_pwm
sudo sh -c 'echo 255 > /sys/devices/pwm-fan/target_pwm'
```

Hâlâ dönmüyorsa cihazı kapatıp fan konnektörü, yön, kablo ve fan gerilimini kontrol et.

## 16. Pixhawk Var ama Veri Yok

```bash
ls -l /dev/serial/by-id/
ls -l /dev/ttyACM0
groups
sudo lsof /dev/ttyACM0
```

`cat` yerine pymavlink heartbeat testi kullan. `dialout` grubunu kontrol et.

## 17. Kamera `/dev/video*` Yok

```bash
sudo dmesg | grep -A4 -B2 imx219
```

`error -121/no acknowledge` ise gücü keserek kablo yönü, oturma, port, kablo ve kamera modülünü kontrol et.

## 18. Disk Doldu

```bash
df -h /
sudo du -xh --max-depth=1 / 2>/dev/null | sort -h
sudo apt clean
```

NVIDIA/CUDA/boot dosyalarını rastgele silme.

## 19. Sorun Bildirirken Toplanacak Paket

```bash
date
uname -a
cat /etc/nv_tegra_release
hostname -I
ip -br address
ip route
findmnt -n -o SOURCE /
df -h /
nmcli device status
```

Donanıma göre ayrıca:

```bash
dmesg | tail -n 100
lsusb
ls -l /dev/serial/by-id/
ls -l /dev/video*
```
