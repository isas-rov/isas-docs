---
tags: [jetson, vnc, gui, xfce]
---

# VNC ile Grafik Arayüz

VNC, Jetson'ın grafik masaüstünü HDMI olmadan başka bilgisayarda gösterir. Mevcut kurulum TigerVNC + XFCE kullanır.

## 1. Gerekli Paketler

İnternet varken:

```bash
sudo apt update
sudo apt install tigervnc-standalone-server tigervnc-common dbus-x11 xfce4
```

Paketler zaten kuruluysa APT bunu bildirir.

## 2. VNC Parolası

```bash
vncpasswd
```

- En az 6 karakter gir.
- Yazarken karakter görünmez.
- `Would you like to enter a view-only password?` sorusunda normal kontrol için `n` seç.
- View-only parola, fare/klavye kullanmadan yalnızca görüntüleme içindir.

## 3. XFCE Başlatma Dosyası

Dosya:

```bash
nano ~/.vnc/xstartup
```

İçerik:

```sh
#!/bin/sh
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
vncconfig -nowin &
exec dbus-launch --exit-with-session startxfce4
```

Kaydet: `Ctrl+O`, `Enter`, `Ctrl+X`.

Çalıştırma izni:

```bash
chmod +x ~/.vnc/xstartup
```

## 4. Sunucuyu Başlat

```bash
vncserver :1 -geometry 1280x720 -depth 24 -localhost no
```

Kısaltma tanımlıysa:

```bash
vncgui
```

Parametreler:

| Parça | Anlamı |
|---|---|
| `:1` | VNC ekran numarası; TCP portu 5901 |
| `-geometry 1280x720` | Sanal ekran çözünürlüğü |
| `-depth 24` | Renk derinliği |
| `-localhost no` | Ağdaki diğer cihazlardan bağlantıya izin verir |

## 5. Viewer ile Bağlan

PdaNet/ICS USB ağında:

```text
192.168.137.2:1
```

NVIDIA varsayılan USB ağında:

```text
192.168.55.1:1
```

Normal router'da:

```text
JETSON_LAN_IP:1
```

## 6. VNC Oturumlarını Gör

```bash
vncserver -list
```

Örnek:

```text
:1    6204
```

## 7. Durdur ve Yeniden Başlat

```bash
vncserver -kill :1
```

```bash
vncserver :1 -geometry 1280x720 -depth 24 -localhost no
```

`stale` yazarsa eski PID dosyası kalmış olabilir. TigerVNC genellikle yeni başlatmada bunu temizler. Önce `vncserver -kill :1`, sonra tekrar başlat.

## 8. Kopyala/Yapıştır

Mevcut oturumda clipboard yardımcısı:

```bash
vncconfig -nowin &
```

Sondaki `&`, komutu arka planda çalıştırır. Bu satır `xstartup` içine eklendiyse her VNC oturumunda otomatik başlar.

## 9. Siyah/Gri Ekran

Log:

```bash
tail -n 100 ~/.vnc/jetson-desktop:1.log
```

Kontroller:

```bash
command -v startxfce4
command -v dbus-launch
ls -l ~/.vnc/xstartup
```

## 10. Güvenlik

`-localhost no`, VNC'yi bağlı ağa açar. Bunu yalnızca güvenilir USB veya yerel ağda kullan.

Güvenilmeyen ağda daha güvenli yol:

Jetson'da VNC'yi yalnızca localhost'a aç:

```bash
vncserver :1 -geometry 1280x720 -depth 24 -localhost yes
```

Bilgisayarda SSH tüneli:

```powershell
ssh -L 5901:localhost:5901 jetson@JETSON_IP
```

Viewer adresi:

```text
localhost:1
```
