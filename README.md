

## 安装CUDA Toolkit Installer，以网络方式安装
```shell
$ wget https://developer.download.nvidia.com/compute/cuda/repos/debian12/x86_64/cuda-keyring_1.1-1_all.deb
$ sudo dpkg -i cuda-keyring_1.1-1_all.deb
$ sudo apt-get update
$ sudo apt-get -y install cuda-toolkit-12-9
```

## 安装CUDA Toolkit Installer，以本地方式安装
```shell
$ wget https://developer.download.nvidia.com/compute/cuda/12.9.1/local_installers/cuda-repo-debian12-12-9-local_12.9.1-575.57.08-1_amd64.deb
$ sudo dpkg -i cuda-repo-debian12-12-9-local_12.9.1-575.57.08-1_amd64.deb
$ sudo cp /var/cuda-repo-debian12-12-9-local/cuda-*-keyring.gpg /usr/share/keyrings/
$ sudo apt-get update
$ sudo apt-get -y install cuda-toolkit-12-9
```

## 安装 Driver Installer
```shell
$ sudo apt-get install -y nvidia-open
$ sudo apt-get install -y cuda-drivers
```
