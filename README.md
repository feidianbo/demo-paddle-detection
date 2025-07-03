## 设置 APT 国内源，Ubuntu 24.04
```shell
$ sudo vim /etc/apt/sources.list.d/ubuntu.sources

# 根据需要选择以下国内镜像源之一，并粘贴到文件中：

# 阿里云源
>>>
Types: deb
URIs: http://mirrors.aliyun.com/ubuntu/
Suites: noble noble-updates noble-security
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
<<<
```

## 安装 CUDA，Ubuntu
```shel
$ sudo apt install nvidia-cuda-toolkit
```

## 设置 Proxy 代理
```shell
$ nano ~/.bashrc

>>>
# add for proxy
export hostip=$(ip route | grep default | awk '{print $3}')
export hostport=10800
alias proxy='
    export HTTPS_PROXY="socks5://${hostip}:${hostport}";
    export HTTP_PROXY="socks5://${hostip}:${hostport}";
    export ALL_PROXY="socks5://${hostip}:${hostport}";
    echo -e "Acquire::http::Proxy \"http://${hostip}:${hostport}\";" | sudo tee -a /etc/apt/apt.conf.d/proxy.conf > /dev/null;
    echo -e "Acquire::https::Proxy \"http://${hostip}:${hostport}\";" | sudo tee -a /etc/apt/apt.conf.d/proxy.conf > /dev/null;
'
alias unproxy='
    unset HTTPS_PROXY;
    unset HTTP_PROXY;
    unset ALL_PROXY;
    sudo sed -i -e '/Acquire::http::Proxy/d' /etc/apt/apt.conf.d/proxy.conf;
    sudo sed -i -e '/Acquire::https::Proxy/d' /etc/apt/apt.conf.d/proxy.conf;
'
<<<
```

## 检查操作系统CPU架构
```shell
$ python3 -c "import platform;print(platform.architecture()[0]);print(platform.machine())"
```

## 安装 Wget
```shell
$ sudo apt install wget
```

## 安装 CUDA Toolkit Installer，以网络方式安装
```shell
# CUDA 12.9
$ wget https://developer.download.nvidia.com/compute/cuda/repos/debian12/x86_64/cuda-keyring_1.1-1_all.deb
$ sudo dpkg -i cuda-keyring_1.1-1_all.deb
$ sudo apt-get update
$ sudo apt-get -y install cuda-toolkit-12-9
```

## 安装 CUDA Toolkit Installer，以本地方式安装
```shell
# CUDA 12.9

$ wget https://developer.download.nvidia.com/compute/cuda/12.9.1/local_installers/cuda-repo-debian12-12-9-local_12.9.1-575.57.08-1_amd64.deb
$ sudo dpkg -i cuda-repo-debian12-12-9-local_12.9.1-575.57.08-1_amd64.deb
$ sudo cp /var/cuda-repo-debian12-12-9-local/cuda-*-keyring.gpg /usr/share/keyrings/
$ sudo apt-get update
$ sudo apt-get -y install cuda-toolkit-12-9
```

## 安装 cuDNN，以网络方式安装
```shell
# cuDNN 12
$ wget https://developer.download.nvidia.com/compute/cudnn/9.10.2/local_installers/cudnn-local-repo-debian12-9.10.2_1.0-1_amd64.deb
$  sudo dpkg -i cudnn-local-repo-debian12-9.10.2_1.0-1_amd64.deb
$ sudo cp /var/cudnn-local-repo-debian12-9.10.2/cudnn-*-keyring.gpg /usr/share/keyrings/
$ sudo apt-get update
$ sudo apt-get -y install cudnn
# 安装 CUDA 12 对应版本
$ sudo apt-get -y install cudnn-cuda-12
```

## 安装 cuDNN，以本地方式安装
```shell
# cuDNN 12
$ wget https://developer.download.nvidia.com/compute/cuda/repos/debian12/x86_64/cuda-keyring_1.1-1_all.deb
$ sudo dpkg -i cuda-keyring_1.1-1_all.deb
$ sudo apt-get update
$ sudo apt-get -y install cudnn
# 安装 CUDA 12 对应版本
$ sudo apt-get -y install cudnn-cuda-12
```

## 安装 Driver Installer
```shell
$ sudo apt-get install -y nvidia-open
$ sudo apt-get install -y cuda-drivers
```

## 安装 PaddlePaddle
```shell
# CUDA 12.9
$  python -m pip install paddlepaddle-gpu==3.1.0 -i https://www.paddlepaddle.org.cn/packages/stable/cu129/
```

## 配置 LibCuda
```shell
$ sudo nano /etc/profile
>>>
# CUDA 12.9
export PATH=/usr/local/cuda-12.9/bin:$PATH

# export LD_LIBRARY_PATH=/usr/local/cuda-12.9/lib64:$LD_LIBRARY_PATH

# 库文件：libcuda.so
export LD_LIBRARY_PATH=/usr/lib/wsl/lib:$LD_LIBRARY_PATH

# 验证
$ nvcc -V
```

## 安装 SetupTools
```shell
$ source .venv/bin/activate
$ pip install --upgrade setuptools
```

## 安装 Ccache
```shell
$ sudo apt install ccache
```

## 检查 PaddlePaddle 版本
```shell
$ python -c "import paddle;paddle.utils.run_check();print(paddle.__version__);"

# 或

$ python3
>>> import paddle
>>> paddle.utils.run_check()
# 确认PaddlePaddle版本
>>> print(paddle.__version___)
```

## 安装 PaddleDetection
```shell
$ git clone https://github.com/PaddlePaddle/PaddleDetection.git
$ cd
$ python -m venv .venv
$ source .venv/bin/activate
$ pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
# 编译安装paddledet
$ python setup.py install
```

