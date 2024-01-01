# 前言

由于深度学习经常使用不同版本的框架，所以需要安装多个版本的cuda和cudnn，这里记录一下安装过程。

# CUDA

## 网络安装

~~在进行后续的本地安装之前，最好先使用网络安装方式进行安装，这两者不会冲突。~~

> **NOTE**: 最好要么只用网络安装，要么只用本地安装，否则很容易产生软件包冲突。

如果要使用网络安装，可以使用我的[脚本](https://github.com/Bit0r/fish-config/blob/main/cuda.fish)

## 查看驱动和cuda版本匹配表

cuda和驱动版本必须匹配，否则会出现问题，所以在安装cuda之前，需要查看cuda和驱动版本匹配表。
一般来说，高版本的驱动可以兼容低版本的cuda，但是低版本的驱动不一定能兼容高版本的cuda。

可以在官方的[cuda与驱动版本匹配表](https://docs.nvidia.com/cuda/cuda-toolkit-release-notes/index.html#id5)查看cuda与驱动版本的匹配情况。

## 下载cuda

在[CUDA Toolkit Archive](https://developer.nvidia.com/cuda-toolkit-archive)网站上下载所需要的版本，这里以11.3.1为例。

![cuda11.3.1](cuda_11_3_1.jpg)

## 安装cuda

下载deb(local)版本的cuda包。

![deb_local](deb_local.jpg)

安装cuda，这里以11.3.1为例。一般来说最后一位数字不需要安装，因为是补丁版本，所以这里是cuda-11-3。
也可以安装cuda-toolkit-11-3，这个包不会安装nvidia驱动，只会安装cuda工具包，如果已经安装了nvidia驱动，可以使用这个包。
推荐先使用cuda-toolkit-11-3，如果运行出项，再使用cuda-11-3。这样可以减少依赖冲突。
安装的版本模式是cuda-M-m或者是cuda-toolkit-M-m，M是主版本号，m是次版本号，这里以11.3.1为例。

具体情况可以查看[元包详情](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/#meta-packages)

按照网页上的命令安装，但是命令需要修改一下。

![command](cuda_install.jpg)

修改成如下命令：

```fish
wget https://xxxxx/cuda-repo-xxx.deb
sudo apt install ./cuda-repo-xxx.deb
sudo apt update
#sudo apt install cuda-11-3  # 这里的cuda-11-3中的11-3是版本号，不需要安装最后一位数字，这个包同时会安装nvidia驱动
sudo apt install cuda-toolkit-11-3  # 只安装cuda工具包，不会安装nvidia驱动，避免Nvidia驱动冲突
```

# cuDNN

## 下载cudnn

在[cudnn archive](https://developer.nvidia.com/rdp/cudnn-archive)下载和**cuda版本对应**cudnn版本，这里以8.2.1为例。

注意⚠️：必须要下载tgz格式的安装包。

![cudnn8.2.1](cudnn_8_2.jpg)

## 安装cudnn

解压cudnn安装包，这里以8.2.1为例。

```fish
unar cudnn-11.3-linux-x64-v8.2.1.32.tgz
cd cudnn-11.3-linux-x64-v8.2.1.32/
sudo mv ./include/* /usr/local/cuda-11.3/include/
sudo mv ./lib64/* /usr/local/cuda-11.3/lib64/
```

# NCCL

## 下载NCCL

在NCCL的[下载页面](https://developer.nvidia.com/nccl/nccl-download)或[旧版本下载页面](https://developer.nvidia.com/nccl/nccl-legacy-downloads)下载和**cuda版本对应**的NCCL版本，这里以2.9.9为例。

注意⚠️：必须要下载os无关的安装包。

![nccl legacy](nccl.jpg)

## 安装NCCL

解压NCCL安装包，这里以2.9.9为例。

```fish
unar nccl_2.9.9-1+cuda11.3_x86_64.txz
cd nccl_2.9.9-1+cuda11.3_x86_64/
sudo mv ./lib/* /usr/local/cuda-11.3/lib64/
sudo mv ./include/* /usr/local/cuda-11.3/include/
```

# 环境变量

我这里使用`fish-config`仓库中的`cuda-home`函数切换cuda版本，这里以11.3.1为例。

```fish
cuda-home /usr/local/cuda-11.3
```
# 问题与解决

## 问题1

运行`nvidia-smi`出现 `NVIDIA-SMI has failed because it couldn't communicate with the NVIDIA driver. Make sure that the latest NVIDIA driver is installed and running.` 错误。

解决方法：重新安装驱动和dkms，其中`xxx`为驱动版本号。

```fish
sudo apt install --reinstall nvidia-driver-xxx nvidia-dkms-xxx
```
