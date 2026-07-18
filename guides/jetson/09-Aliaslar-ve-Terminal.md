---
tags: [jetson, bash, alias, terminal]
---

# Aliaslar ve Terminal Kullanımı

## Alias Nedir?

Alias, uzun bir komuta kısa bir ad vermektir.

Örnek:

```bash
alias jetip='sudo ip address replace 192.168.137.2/24 dev l4tbr0'
```

Bundan sonra:

```bash
jetip
```

yazıldığında Bash uzun komutu çalıştırır.

## Jetson ve Windows Aliasları Aynı Değildir

| Ortam | Ayar dosyası/konumu | Örnek |
|---|---|---|
| Jetson Bash | `/home/jetson/.bashrc` veya `~/.bash_aliases` | `jetip`, `fanmid`, `vncgui` |
| Windows PowerShell | `$PROFILE` | `jetproxy` fonksiyonu |
| Windows CMD | `C:\Users\kolay\bin\jetproxy.cmd` | `jetproxy` |
| Windows Git Bash | `C:\Users\kolay\.bashrc` | `jetproxy` |

Git Bash'teki `~` Windows kullanıcı klasörüdür; Jetson'daki `~` ise `/home/jetson` klasörüdür.

## Önerilen Jetson Alias Dosyası

Aliasları ana `.bashrc` yerine ayrı dosyada tutmak düzenlidir:

```bash
nano ~/.bash_aliases
```

İçerik:

```bash
alias jetip='sudo ip address replace 192.168.137.2/24 dev l4tbr0'
alias fanstop="sudo sh -c 'echo 0 > /sys/devices/pwm-fan/target_pwm'"
alias fanmid="sudo sh -c 'echo 128 > /sys/devices/pwm-fan/target_pwm'"
alias fanfull="sudo sh -c 'echo 255 > /sys/devices/pwm-fan/target_pwm'"
alias vncgui='vncserver :1 -geometry 1280x720 -depth 24 -localhost no'
alias vnckill='vncserver -kill :1'
alias vnclist='vncserver -list'
```

Ubuntu'nun varsayılan `.bashrc` dosyası genellikle `~/.bash_aliases` dosyasını otomatik yükler. Kontrol:

```bash
grep -n "bash_aliases" ~/.bashrc
```

## Ayarı Hemen Yüklemek

```bash
source ~/.bashrc
```

veya yalnızca alias dosyası:

```bash
source ~/.bash_aliases
```

`source`, dosyayı yeni bir kabuk açmadan mevcut terminalde çalıştırır. `source` kullanılmazsa yeni alias ancak yeni terminal açıldığında tanınır.

## Alias Kontrolü

```bash
type jetip
type fanmid
type vncgui
```

Tüm aliaslar:

```bash
alias
```

Dosyada ara:

```bash
grep -n "alias" ~/.bash_aliases
```

## `tail` Ne Yapar?

```bash
tail -n 10 ~/.bashrc
```

- `tail`: Dosyanın sonunu gösterir.
- `-n 10`: Son 10 satır.
- `~/.bashrc`: Ana klasördeki dosya.

`tail -n 10 .bashrc` sadece o anda bulunduğun klasördeki `.bashrc` dosyasını okur. `~/.bashrc` daha açıktır.

## Yinelenen Aliasları Bulmak

```bash
grep -n "alias jetip" ~/.bashrc ~/.bash_aliases 2>/dev/null
```

Aynı alias iki kez tanımlıysa son okunan tanım geçerli olur. Dosyayı `nano` ile açıp fazlalığı silmek en temiz yöntemdir.

## Tırnak Mantığı

### Tek tırnak `'...'`

İçerideki karakterleri olduğu gibi korur. `$`, `>`, boşluk gibi karakterler Bash tarafından erken yorumlanmaz.

```bash
echo 'Merhaba $USER'
```

Çıktı gerçekten `Merhaba $USER` olur.

### Çift tırnak `"..."`

Boşlukları tek metin olarak tutar fakat `$USER` gibi değişkenleri genişletir.

```bash
echo "Merhaba $USER"
```

Çıktı `Merhaba jetson` olur.

### Ters bölü `\`

Sonraki karakterin özel anlamını kaçırır.

```bash
echo "Bu bir \"alıntı\" metnidir"
```

Burada `\"`, çift tırnağı metnin bir parçası yapar.

## `sudo sh -c` Neden Gerekir?

Bu komut genellikle çalışmaz:

```bash
sudo echo 128 > /sys/devices/pwm-fan/target_pwm
```

Çünkü `sudo` yalnızca `echo` komutuna uygulanır; `>` yönlendirmesini normal kullanıcı kabuğu yapar.

Doğrusu:

```bash
sudo sh -c 'echo 128 > /sys/devices/pwm-fan/target_pwm'
```

- `sh`: Yeni bir kabuk çalıştırır.
- `-c`: Sonraki metni komut olarak çalıştır der.
- `sudo`: Bu kabuğun tamamını root yapar.
- Böylece `>` işlemi de yetkili olur.

## `>>` ve `>` Farkı

```bash
echo "satır" > dosya
```

Dosyanın eski içeriğini siler ve yeniden yazar.

```bash
echo "satır" >> dosya
```

Dosyanın sonuna ekler.

`.bashrc` için yanlışlıkla `>` kullanmak mevcut ayarları silebilir. Düzenleme için `nano` daha güvenlidir.

## Alias Ne Zaman Yetersizdir?

Parametre alan, koşul içeren veya birden fazla adım yapan işler için fonksiyon/script daha doğrudur.

Örnek fonksiyon:

```bash
jetinfo() {
    hostname -I
    ip route
    df -h /
}
```

Sonra:

```bash
jetinfo
```
