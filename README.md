# Ubuntu 20.04' e GPU, CUDA, cuDNN ve TensorFlow Kurulumu

Bu rehber, Ubuntu 20.04 üzerine GPU sürücüleri, CUDA, cuDNN ve TensorFlow kurulumunu kapsamaktadır. Adımlar, Nvidia GeForce RTX3060 (m-Notebook) grafik kartı için gösterilmiş olsa da, CUDA uyumlu herhangi bir GPU için izlenebilir.

## Adım 1: Grafik Kartı Sürücüsünü Yükleyin

Yeni bir Ubuntu 20.04 kurulumu üzerinde çalıştığınızı varsayarsak, ilk adım grafik kartınız için sürücüyü yüklemektir.

Terminal'de şu komutları çalıştırın:

```bash
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt install nvidia-driver-470
```
Sürücüyü yükledikten sonra, kurulumu doğrulamak için terminalde şu komutu çalıştırın:
```bash

nvidia-smi

```
![MasterHead](https://github.com/VeliYarar/CUDA-ve-CuDNN-Ubuntu-ya-nasil-kurulur/blob/main/Ekran%20g%C3%B6r%C3%BCnt%C3%BCs%C3%BC%202023-11-30%20215720.png)
Not: Lütfen CUDA sürümünü sağ üstte dikkate alın. Benim durumumda 11.4. Doğru CUDA sürümünü takip etmek önemlidir.
## Adım 2: CUDA'yı Yükleyin
CUDA, GPU'nun genel amaçlı işlemlerde kullanılmasını sağlamak için Nvidia tarafından geliştirilen bir paralel hesaplama platformu ve uygulama programlama arayüzü modelidir.
Nvidia Grafik kartı sürücüsünü yükledikten sonra, nvidia-smi çıktısından sürüme göre CUDA'yı yükleyin.
Biz CUDA 11.4'ü yükleyeceğiz. Lütfen doğru CUDA Sürümünü kullanın.

Aşağıdakileri Terminal'de çalıştırın:

```bash

wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin
sudo mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/11.4.0/local_installers/cuda-repo-ubuntu2004-11-4-local_11.4.0-470.42.01-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2004-11-4-local_11.4.0-470.42.01-1_amd64.deb
sudo apt-key add /var/cuda-repo-ubuntu2004-11-4-local/7fa2af80.pub
sudo apt-get update
sudo apt-get -y install cuda

```
![MasterHead](https://github.com/VeliYarar/CUDA-ve-CuDNN-Ubuntu-ya-nasil-kurulur/blob/main/Ekran%20g%C3%B6r%C3%BCnt%C3%BCs%C3%BC%202023-11-30%20215424.png)

## Adım 3: cuDNN'i yükleyin
cuDNN, Nvidia tarafından derin sinir ağları için geliştirilen GPU hızlandırmalı ilkel kütüphanedir.

Yine yukarıdaki adımda yüklenen CUDA sürümüne göre doğru cuDNN sürümünü yüklemeniz gerekir. Benim CUDA Sürümüm 11.2 olduğu için cuDNN Arşivinden "Download cuDNN v8.2.1 (June 7th, 2021), for CUDA 11.x" >> "cuDNN Library for Linux (x86_64)" indirmeyi seçtim. Lütfen buna göre seçim yapın.

İndirmek için bir Nvidia hesabı oluşturmanız gerekecek. İndirdikten sonra aşağıdaki talimatları kullanın.

Aşağıdakileri Terminal'de çalıştırın:
```bash
tar -xzvf cudnn-11.4-linux-x64-v8.2.1.32.tgz
sudo cp cuda/include/cudnn.h /usr/local/cuda/include
sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*

```


.bashrc dosyasında yolu ayarlayın.

home dizininden Terminal'de aşağıdakileri çalıştırın:
```bash

gedit .bashrc

```
Yukarıdaki komut .bashrc dosyasını metin editöründe açacaktır. Farklı CUDA Sürümü kullanıyorsanız lütfen aşağıdaki yoldaki sürümü değiştirin. Aşağıdaki kodu eklendikten sonra metin düzenleyiciyi kaydedin ve kapatın.

```bash
export LD_LIBRARY_PATH=/usr/local/cuda-11.4/lib64:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
```

home dizininden Terminal'de aşağıdakileri çalıştırın:

```bash

source ~/.bashrc

```

## Adım 4: PIP'i Kurun
Python3.8 Ubuntu 20.04'te önceden yüklenmiş olarak gelir. PIP'i yüklemek için aşağıdaki komutu çalıştırın.

Aşağıdaki komutu Terminal'de çalıştırın:

```bash
sudo apt update
sudo apt install python3-pip

```

## Adım 5: Tensorflow'u yükleyin
Tensorflow varsayılan olarak GPU desteği ile birlikte gelir, bu nedenle özellikle tensorflow-gpu yüklemenize gerek yoktur

Aşağıdakileri Terminal'de çalıştırın:

```bash

pip install tensorflow

```

## Adım 6: Tensorflow'u kontrol edin
GPU'nun Tensorflow tarafından algılandığını kontrol edin

Aşağıdakileri Terminal'de çalıştırın:
```bash
python3
```
Aşağıdakileri python komut satırından çalıştırın:
(çift tırnak kullanın)
```bash
import tensorflow as tf
tf.config.list_physical_devices(“GPU”)
```
[PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')]" ifadesini aşağıdaki gibi görebilmeniz gerekir.


![MasterHead](https://raw.githubusercontent.com/VeliYarar/CUDA-ve-CuDNN-Ubuntu-ya-nasil-kurulur/main/1_DhNy8tIk9ht1d5z9bo7d5A.webp)

Not: Sorunlarla karşılaşıyorsanız, bunun nedeni büyük olasılıkla sürüm uyuşmazlığı olacaktır.
Not: Tüm gerekli linkler "indirme bağlantılar" da mevcuttur

# Okuduğunuz için teşekkür ederim umarım işinize yaramıştır….






