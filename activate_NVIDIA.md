# how to activate NVIDA GTX10 series GTX1080 Ti

## install driver
#### search and download driver from official website
![](/img/driver1.png)
![](/img/driver2.png)

#### execute downloaded .run
cd ~/download
sudo chmod +x NVIDIA-Linux-x86_64-450.80.02.run
./NVIDIA-Linux-x86_64-450.80.02.run

## solve `Failed to fetch cdrom` error [ref](https://linuxconfig.org/failed-to-fetch-cdrom-ubuntu-debian-apt-get-error-message-solution)
#### turn off apt source from cdrom
turn on 'Software & Updates'
uncheck "Cdrom with Ubuntu 20.04 'Focal Fossa'"
![](/img/driver3.png)

## solve `The Nouveau kernel driver is currently in use by your system` [ref](https://clay-atlas.com/blog/2020/02/11/linux-chinese-note-nvidia-driver-nouveau-kernel/)

sudo vim /etc/modprobe.d/blacklist-nouveau.conf
#### settings in blacklist-nouveau.conf
```
blacklist nouveau
options nouveau modeset=0
```

#### regenerate kernel and reboot
sudo update-initramfs -u
sudo reboot

#### check if Nouveau stopped
lsmod | grep nouveau

## install CUDA [ref](https://www.tensorflow.org/install/gpu#software_requirements)

#### Add NVIDIA package repositories
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-repo-ubuntu1804_10.1.243-1_amd64.deb
sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub
sudo dpkg -i cuda-repo-ubuntu1804_10.1.243-1_amd64.deb
sudo apt-get update
wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64/nvidia-machine-learning-repo-ubuntu1804_1.0.0-1_amd64.deb
sudo apt install ./nvidia-machine-learning-repo-ubuntu1804_1.0.0-1_amd64.deb
sudo apt-get update

#### Install development and runtime libraries (~4GB)
sudo apt-get install --no-install-recommends \
    cuda-10-1 \
    libcudnn7=7.6.5.32-1+cuda10.1  \
    libcudnn7-dev=7.6.5.32-1+cuda10.1


#### Install TensorRT. Requires that libcudnn7 is installed above.
sudo apt-get install -y --no-install-recommends libnvinfer6=6.0.1-1+cuda10.1 \
    libnvinfer-dev=6.0.1-1+cuda10.1 \
    libnvinfer-plugin6=6.0.1-1+cuda10.1
