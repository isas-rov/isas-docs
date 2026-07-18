---
tags: [jetson, cuda, python, kodlama]
---

# CUDA, Python ve Kodlama Akışı

## Doğrulanmış Yazılım Yığını

```text
Ubuntu:   18.04.6 LTS
Python:   3.6.9
JetPack:  4.6.5-b29
CUDA:     10.2.300
GPU:      NVIDIA Tegra X1, compute capability 5.3
RAM:      yaklaşık 4 GB
```

JetPack paketleri:

```bash
dpkg-query -W nvidia-jetpack nvidia-cuda nvidia-cudnn8 nvidia-tensorrt
```

CUDA derleyicisi:

```bash
/usr/local/cuda/bin/nvcc --version
```

Doğrulanmış sürüm:

```text
Cuda compilation tools, release 10.2, V10.2.300
```

## CUDA Ortam Değişkenleri

Genellikle `.bashrc` sonuna:

```bash
export PATH=/usr/local/cuda/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
```

Yükle:

```bash
source ~/.bashrc
```

Kontrol:

```bash
which nvcc
nvcc --version
```

## `deviceQuery` Testi

İlk denemede yalnızca `deviceQuery` klasörü kopyalandığı için `helper_cuda.h` eksik kaldı. CUDA örneklerinin `common` klasörüne göreli yolu korunmalıdır.

Doğru yapı:

```bash
cd ~/cuda-samples/1_Utilities/deviceQuery
make
./deviceQuery
```

Doğrulanmış sonuç:

```text
Detected 1 CUDA Capable device(s)
Device 0: "NVIDIA Tegra X1"
CUDA Capability: 5.3
Result = PASS
```

## Python ve pip

Sürüm:

```bash
python3 --version
```

pip kurulu değilse:

```bash
sudo apt update
sudo apt install python3-pip python3-venv
```

Kontrol:

```bash
python3 -m pip --version
```

> [!warning] Python 3.6 uyumluluğu
> Python 3.6 artık çok eski olduğu için yeni paketlerin bazıları kurulmaz. Paket dokümanında Python 3.6'yı destekleyen son sürümü bul ve gerekirse sürüm sabitle. Sistem Python'unu rastgele değiştirme; JetPack araçları ona bağlı olabilir.

## Proje Klasörü Oluşturma

```bash
mkdir -p ~/projects/isas
cd ~/projects/isas
```

- `mkdir`: Klasör oluşturur.
- `-p`: Üst klasörler yoksa oluşturur; varsa hata vermez.
- `~`: `/home/jetson`.
- `cd`: Klasör değiştirir.

## Sanal Ortam

```bash
cd ~/projects/isas
python3 -m venv .venv
source .venv/bin/activate
```

Terminal başında `(.venv)` görünür. Paketleri bu projeye kur:

```bash
python -m pip install PAKET_ADI
```

Çık:

```bash
deactivate
```

Sanal ortam, proje paketlerini sistem Python paketlerinden ayırır.

## Kod Editörleri

### Nano

Terminal içinde:

```bash
nano program.py
```

Kaydet: `Ctrl+O`, `Enter`; çık: `Ctrl+X`.

### Mousepad

XFCE grafik editörü:

```bash
mousepad program.py &
```

### Geany

Kur:

```bash
sudo apt install geany
```

Aç:

```bash
geany program.py &
```

## İlk Python Programı

```bash
nano ~/projects/isas/merhaba.py
```

İçerik:

```python
from datetime import datetime

print("Jetson proje ortami calisiyor")
print("Zaman:", datetime.now())
```

Çalıştır:

```bash
python3 ~/projects/isas/merhaba.py
```

## Bir Programı Çalıştırılabilir Yapmak

Dosyanın ilk satırı:

```python
#!/usr/bin/env python3
```

İzin:

```bash
chmod +x program.py
```

Çalıştır:

```bash
./program.py
```

## Git ile Kod Takibi

```bash
sudo apt install git
git --version
```

Yeni depo:

```bash
cd ~/projects/isas
git init
git status
```

Sanal ortamı Git'e ekleme:

```bash
printf '.venv/\n__pycache__/\n*.pyc\n' > .gitignore
```

## Loglama

Python'da `print` yerine zaman damgalı `logging` kullanmak hata ayıklamayı kolaylaştır:

```python
import logging

logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s %(levelname)s %(message)s",
)

logging.info("Uygulama basladi")
```

## Proje Servisi Yapmadan Önce

Bir kodu otomatik başlayan `systemd` servisine çevirmeden önce:

1. Terminalde hatasız çalıştır.
2. Mutlak dosya yolları kullan.
3. Pixhawk/kamera yeniden bağlanma durumunu ele al.
4. Log dosyası veya journald kaydı oluştur.
5. Güvenli kapanış ve istisna yakalama ekle.

## Jetson Nano Kaynak Sınırları

- 4 GB RAM hızla dolabilir.
- Aynı anda Chromium, VNC, CUDA modeli ve derleme çalıştırmak bellek baskısı oluşturur.
- `tegrastats` ile CPU/GPU/RAM/sıcaklık izle:

```bash
tegrastats
```

Durdur: `Ctrl+C`.
