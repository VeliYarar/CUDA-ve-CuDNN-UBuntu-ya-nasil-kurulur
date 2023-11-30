Bu repository Ubuntu 20.04'te GPU, CUDA, cuDNN ve Tensorflow kurulumunu kapsamaktadır. Aşağıda Nvidia GeForce RTX3060 (m-Notebook) Grafik kartı için gösterdim, ancak herhangi bir CUDA uyumlu GPU için aşağıdaki adımları takip edebilirsiniz.

## Adım 1: Grafik Kartı Sürücüsünü Yükleyin

Yeni bir Ubuntu 20.04 kurulumu üzerinde çalıştığınızı varsayarsak, ilk adım grafik kartınız için sürücü yüklemektir.

Terminal'de aşağıdaki komutu çalıştırın:

sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt install nvidia-driver-470
