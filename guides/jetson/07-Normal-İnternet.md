---
tags: [jetson, internet, ethernet, wifi, ics]
---

# Normal İnternet: Modem, Router, Ethernet ve Wi-Fi

Bu not PdaNet kullanılmayan standart internet senaryolarını anlatır.

## Seçenek 1 — Jetson'u Doğrudan Modem/Router'a Ethernet ile Bağlamak

En temiz ve proje için en güvenilir geliştirme bağlantısıdır.

1. Ethernet kablosunu Jetson `eth0` ile router LAN portu arasına tak.
2. Jetson'da:

```bash
nmcli device status
```

Beklenen:

```text
eth0  ethernet  connected  ...
```

3. Adresi kontrol et:

```bash
ip -4 address show eth0
```

4. Varsayılan yolu kontrol et:

```bash
ip route
```

`default via <router-ip> dev eth0` beklenir.

5. Test:

```bash
ping -c 3 google.com
sudo apt update
```

## Seçenek 2 — Uyumlu Wi-Fi Adaptörü

Waveshare'in bazı Kit A paketlerinde RTL8822CE tabanlı kablosuz kart bulunur; mevcut cihazda `nmcli device status` çıktısında `wlan` görünmediyse kart takılı olmayabilir, anten/driver eksik olabilir veya farklı paket alınmış olabilir.

Kontrol:

```bash
nmcli device status
```

Wi-Fi cihazı varsa ağları listele:

```bash
nmcli device wifi list
```

Bağlan:

```bash
sudo nmcli device wifi connect "AG_ADI" password "WIFI_PAROLASI"
```

Durum:

```bash
nmcli connection show --active
hostname -I
ip route
```

Parolayı komut geçmişinde bırakmak istemiyorsan grafik NetworkManager arayüzünü veya etkileşimli yöntemi kullan.

## Seçenek 3 — Windows'un Normal İnternetini USB Üzerinden Paylaştırmak

Bu senaryoda Windows internete normal Wi-Fi, Ethernet veya telefonun yerleşik USB tethering özelliğiyle bağlıdır.

Windows:

1. `Win+R` → `ncpa.cpl`.
2. İnterneti olan adaptöre sağ tık → `Özellikler` → `Paylaşım`.
3. `Diğer ağ kullanıcıları...` kutusunu işaretle.
4. Ev ağı olarak Jetson USB adaptörünü (`Ethernet`) seç.
5. Windows Ethernet adresinin `192.168.137.1/24` olduğunu kontrol et.

Jetson:

```bash
sudo ip address replace 192.168.137.2/24 dev l4tbr0
sudo ip route replace default via 192.168.137.1 dev l4tbr0
```

DNS gerekiyorsa NetworkManager profiline DNS verilebilir:

```bash
sudo nmcli connection modify l4tbr0 ipv4.dns "1.1.1.1 8.8.8.8"
```

Test:

```bash
ip route get 1.1.1.1
ping -c 3 1.1.1.1
ping -c 3 google.com
```

Normal ICS/NAT çalışıyorsa tarayıcı ve ham TCP/UDP trafiği proxy olmadan çıkabilir. PdaNet bazı modlarda bu aktarımı engellediği için ayrı proxy çözümü kullanıldı.

## PdaNet Proxy'sinden Normal İnternete Geçiş

Mevcut Jetson, HTTP/HTTPS trafiğini `192.168.137.1:3128` proxy'sine yönlendirir. Normal router'a geçince proxy kapatılmazsa internet çalışmıyor gibi görünebilir.

APT proxy'sini devre dışı bırak:

```bash
sudo mv /etc/apt/apt.conf.d/95pdanet-proxy /etc/apt/apt.conf.d/95pdanet-proxy.disabled
```

Genel proxy profilini devre dışı bırak:

```bash
sudo mv /etc/profile.d/pdanet-proxy.sh /etc/profile.d/pdanet-proxy.sh.disabled
```

Mevcut terminalde değişkenleri temizle:

```bash
unset http_proxy https_proxy HTTP_PROXY HTTPS_PROXY no_proxy NO_PROXY
```

Yeni oturum aç veya VNC/Jetson'ı yeniden başlat.

PdaNet'e geri dönerken:

```bash
sudo mv /etc/apt/apt.conf.d/95pdanet-proxy.disabled /etc/apt/apt.conf.d/95pdanet-proxy
sudo mv /etc/profile.d/pdanet-proxy.sh.disabled /etc/profile.d/pdanet-proxy.sh
source /etc/profile.d/pdanet-proxy.sh
```

## Hangi Bağlantıyı Projede Kullanmalı?

| Aşama | Önerilen bağlantı |
|---|---|
| Paket/model indirme | Router Ethernet veya kararlı Wi-Fi |
| Masa üstü geliştirme | Ethernet + SSH/VNC |
| PdaNet zorunlu durum | Yerel Windows proxy |
| Araçta gerçek zamanlı kontrol | Yerel ağ/seri; internete bağımlı olmamalı |
| Sahadan telemetri | Ayrı ve tasarlanmış modem/VPN hattı |
