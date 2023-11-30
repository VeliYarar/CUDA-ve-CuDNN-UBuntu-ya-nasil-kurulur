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


.bashrc dosyasında yolu ayarlayın.

home dizininden Terminal'de aşağıdakileri çalıştırın:
```bash

gedit .bashrc

´´´


















