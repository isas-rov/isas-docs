---
tags: [jetson, ag, temel-kavramlar]
---

# Sistem Özeti ve Temel Kavramlar

## Mevcut Donanım/Yazılım

| Bileşen | Mevcut durum |
|---|---|
| Kart | Waveshare Jetson Nano IO-BASE-A tabanlı geliştirme kiti |
| SoC | Tegra X1, 128 CUDA çekirdeği, 4 GB RAM |
| Dahili depolama | 16 GB eMMC, Linux'ta `/dev/mmcblk0` |
| Haricî depolama | 64 GB SD, Linux'ta `/dev/mmcblk1` |
| Kök `/` | `/dev/mmcblk1p1` |
| Ubuntu | 18.04.6 LTS, ARM64 |
| Jetson Linux | L4T R32.7.5 |
| JetPack | 4.6.5-b29 |
| CUDA | 10.2.300 |
| Kullanıcı | `jetson` |
| Makine adı | `jetson-desktop` |

## Terminal Türleri

Komutun nereye yazılacağı, komutun kendisi kadar önemlidir.

### Jetson Bash

```text
jetson@jetson-desktop:~$
```

Linux komutları burada çalışır: `ls`, `cat`, `ip`, `nmcli`, `sudo`, `vncserver`, `python3`.

### Windows PowerShell

```text
PS C:\WINDOWS\system32>
```

PowerShell komutları burada çalışır: `Get-NetIPAddress`, `Get-Service`, `Test-NetConnection`.

### Windows CMD

```text
C:\Users\kolay>
```

CMD komutları: `ping`, `where`, `type`, `doskey` ve `.cmd` dosyaları.

### Git Bash

```text
kolay@korAY MINGW64 ~
$
```

Windows'ta Bash benzeri bir kabuktur. Git Bash'in `~/.bashrc` dosyası ile Jetson'ın `~/.bashrc` dosyası aynı dosya değildir.

## IP, Alt Ağ ve Port Farkı

> [!important] "IP'leri eşitlemek" yanlış ifadedir
> Windows ve Jetson'a aynı IP verilmez. Aynı alt ağda, birbirinden farklı IP verilir.

Mevcut USB/ICS ağı:

```text
Alt ağ: 192.168.137.0/24
Windows:  192.168.137.1
Jetson:   192.168.137.2
```

`/24`, ilk üç sayı grubunun ağı tanımladığı anlamına gelir. Cihazların son sayısı farklı olmalıdır.

Port, IP'den farklıdır:

| Hizmet | Varsayılan port | Kullanım |
|---|---:|---|
| SSH | 22 | Terminal |
| VNC `:1` | 5901 | Grafik masaüstü |
| Yerel proxy | 3128 | HTTP/HTTPS internet |

`192.168.137.2` vermek SSH portunu değiştirmez; SSH yine 22 numaralı porttadır.

## USB Ağının İki Adres Planı

### NVIDIA varsayılan USB Device Mode

```text
Jetson:  192.168.55.1
Windows: 192.168.55.100
```

Sadece cihazlar arası bağlantı için yeterlidir. Tek başına Jetson'a internet vermez.

### Windows ICS planı

```text
Windows: 192.168.137.1
Jetson:  192.168.137.2
```

Windows internet paylaşımı etkinleştiğinde yaygın olarak bu plan kullanılır. Mevcut sistemde SSH, VNC ve PdaNet proxy için bu plan kullanılıyor.

## Adres Kontrol Komutları

Jetson:

```bash
hostname -I
ip -br address
ip route
```

Windows PowerShell:

```powershell
Get-NetIPAddress -AddressFamily IPv4 | Format-Table InterfaceAlias,IPAddress,PrefixLength
```

## Aynı Alt Ağ Testi

Windows'tan Jetson'a:

```powershell
ping 192.168.137.2
```

Jetson'dan Windows'a:

```bash
ping -c 3 192.168.137.1
```

Windows güvenlik duvarı ping yanıtını engelleyebilir. Bu nedenle Windows'tan Jetson'a başarılı ping ve SSH/VNC bağlantısı daha güçlü kanıttır.

## Komut ile Çıktıyı Ayırmak

Bu metin bir komut değildir:

```text
jetson@jetson-desktop:~$
```

Doğru kopyalama:

```bash
hostname -I
```

Yanlış kopyalama:

```bash
jetson@jetson-desktop:~$ hostname -I
```

Yanlış kopyalama `command not found` hatasına neden olur.
