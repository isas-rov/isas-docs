---
tags: [jetson, guvenlik, yedek, operasyon]
---

# Güvenlik, Yedekleme ve Operasyon

## 1. Parolalar

- Jetson kullanıcı parolasını ekip dışında paylaşma.
- VNC parolasını SSH parolasıyla aynı yapma.
- Parolaları komut satırına veya Git deposuna yazma.
- Varsayılan/fabrika parolası varsa değiştir:

```bash
passwd
```

## 2. SSH

- SSH'yi yalnızca gerekli ağlarda açık tut.
- Dış internete 22 portunu doğrudan yönlendirme.
- Uzun vadede parola yerine SSH anahtarı kullan.
- Anahtar ekledikten ve test ettikten sonra parola girişini kapatmayı değerlendir.
- SSH ayarını değiştirmeden seri konsol kurtarma yolunun çalıştığını doğrula.

## 3. VNC

`-localhost no` yalnızca güvenilir yerel/USB ağda kullanılmalı. Ortak Wi-Fi'de VNC'yi SSH tüneli arkasında çalıştır.

## 4. PdaNet Proxy Güvenliği

Hazırlanan proxy:

- Yalnızca Windows `192.168.137.1` adresine bağlanır.
- Yalnızca `192.168.137.2` Jetson istemcisini kabul eder.
- Windows güvenlik duvarı kuralı da uzak adresi `192.168.137.2` ile sınırlar.
- Genel internete açık bir proxy olarak kullanılmamalıdır.

HTTPS içerik, `CONNECT` tünelinde hedef site ile istemci arasında TLS şifreli kalır. HTTP içerik şifreli değildir.

## 5. Paket ve Sürüm Güvenliği

- JetPack/L4T/NVIDIA paketlerini aynı sürüm ailesinde tut.
- `dist-upgrade` öncesi tam yedek ve uyumluluk kontrolü yap.
- Bilinmeyen scriptleri doğrudan `curl | sudo sh` ile çalıştırma.
- APT kaynak dosyalarını kontrol et:

```bash
grep -R "^deb" /etc/apt/sources.list /etc/apt/sources.list.d/ 2>/dev/null
```

## 6. Kod Yedeği

Kodlar:

```text
/home/jetson/projects/isas
```

Önerilen:

- Her proje Git deposu olsun.
- `.venv`, model cache ve büyük veri setleri Git'e eklenmesin.
- Uzak Git deposu veya düzenli bilgisayar kopyası olsun.
- Gizli anahtar/token için `.env` kullan ve `.gitignore`a ekle.

Örnek `.gitignore`:

```text
.venv/
__pycache__/
*.pyc
.env
logs/
models/
datasets/
```

## 7. Yapılandırma Yedeği

Önemli dosyalar:

```text
/boot/extlinux/extlinux.conf
/etc/apt/apt.conf.d/95pdanet-proxy
/etc/profile.d/pdanet-proxy.sh
/home/jetson/.bashrc
/home/jetson/.bash_aliases
/home/jetson/.vnc/xstartup
```

Yedek klasörü:

```bash
mkdir -p ~/backups/jetson-config
```

Kullanıcı dosyaları:

```bash
cp ~/.bashrc ~/.bash_aliases ~/.vnc/xstartup ~/backups/jetson-config/
```

Sistem dosyaları:

```bash
sudo cp /boot/extlinux/extlinux.conf ~/backups/jetson-config/
sudo cp /etc/apt/apt.conf.d/95pdanet-proxy ~/backups/jetson-config/
sudo cp /etc/profile.d/pdanet-proxy.sh ~/backups/jetson-config/
sudo chown -R jetson:jetson ~/backups/jetson-config
```

Dosya yoksa `cp` hata verebilir; bu, diğer kopyaların bozuk olduğu anlamına gelmez.

## 8. SD Kart Yedeği

Tam SD imajı alma işlemi hedef diski karıştırma riski taşır. En güvenli prosedür:

1. Jetson'ı `sudo poweroff` ile kapat.
2. SD kartı enerjisizken çıkar.
3. Windows/Linux ana bilgisayarda kapasite ve aygıtı iki kez doğrula.
4. Okuma yönünde imaj al; yanlış yönde yazma veri kaybına yol açar.
5. İmajı tarih, L4T ve kart kimliğiyle adlandır.
6. Yedeği ayrı fiziksel diskte tut.

## 9. Log ve Disk Aşınması

SD kart yazma ömrü sınırlıdır.

- Sonsuz ve çok sık log yazma.
- Log rotasyonu kullan.
- Kamera ham videosunu sürekli kök SD'ye yazmak yerine ayrı depolama planla.
- Swap ve veri setleri için high-endurance kart tercih et.
- Disk doluluğunu izle:

```bash
df -h /
```

## 10. Güvenli Güç Kesme

```bash
sudo poweroff
```

Güç kesme sırasında yazılan ext4 journal/dosyalar bozulabilir. Fiziksel ana şalter tasarımında Jetson'a yazılımsal kapanma süresi ver.

## 11. Sahada İnternetsiz Çalışma

Araç kontrolü, Pixhawk heartbeat ve emniyet mantığı Windows/PdaNet/proxy'ye bağlı olmamalıdır.

Dağıtım öncesi:

- Gerekli Python paketlerini yerel sanal ortama kur.
- Model dosyalarını yerel depola.
- DNS/internet olmadan boot testi yap.
- Windows proxy kapalıyken ana uygulamayı test et.
- Pixhawk bağlantısı koptuğunda fail-safe davranışını test et.
- Kamera yokken uygulamanın kontrollü hata vermesini sağla.

## 12. Operasyon Kontrol Listesi

### Önce

- [ ] SD kart ve güç konektörleri sabit.
- [ ] Fan dönüyor.
- [ ] Diskte yeterli alan var.
- [ ] Sistem saati doğru.
- [ ] Pixhawk portu ve heartbeat doğru.
- [ ] Kamera doğrulanmış.
- [ ] Güçlü akım/motor hattı kontrol elektroniğinden ayrı.

### Sonra

- [ ] Uygulama ve sistem logları kopyalandı.
- [ ] Kod değişiklikleri commit edildi.
- [ ] `sudo poweroff` uygulandı.
- [ ] Güç kesildikten sonra kablo/sensör söküldü.
