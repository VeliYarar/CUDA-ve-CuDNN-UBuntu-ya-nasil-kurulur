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

Not: Lütfen CUDA sürümünü sağ üstte dikkate alın. Benim durumumda 11.4. Doğru CUDA sürümünü takip etmek önemlidir.
