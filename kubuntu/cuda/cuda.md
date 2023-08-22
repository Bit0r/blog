# 前言

由于深度学习经常使用不同版本的框架，所以需要安装多个版本的cuda和cudnn，这里记录一下安装过程。

# CUDA

## 网络安装

在进行后续的本地安装之前，最好先使用网络安装方式进行安装，这两者不会冲突。

使用我的[脚本](https://github.com/Bit0r/fish-config/blob/main/cuda.fish)即可

## 下载cuda

在[CUDA Toolkit Archive](https://developer.nvidia.com/cuda-toolkit-archive)网站上下载所需要的版本，这里以11.3.1为例。

![cuda11.3.1](cuda_11_3_1.jpg)

## 安装cuda

下载deb(local)版本的cuda包。

![deb_local](deb_local.jpg)

安装cuda，这里以11.3.1为例。一般来说最后一位数字不需要安装，因为是补丁版本，所以这里是cuda-11-3。模式一般是cuda-M-m。

按照网页上的命令安装，但是命令需要修改一下。

![command](cuda_install.jpg)

修改成如下命令：

```fish
wget https://xxxxx/cuda-repo-xxx.deb
sudo apt install ./cuda-repo-xxx.deb
sudo apt update
sudo apt install cuda-11-3
```

# cuDNN

## 下载cudnn

在[cudnn archive](https://developer.nvidia.com/rdp/cudnn-archive)下载和**cuda版本对应**cudnn版本，这里以8.2.1为例。

注意⚠️：必须要下载tgz格式的安装包。

![cudnn8.2.1](cudnn_8_2.jpg)

## 安装cudnn

解压cudnn安装包，这里以8.2.1为例。

```fish
mkdir -p cudnn-8-2/
tar xvf cudnn-11.3-linux-x64-v8.2.1.32.tgz --directory cudnn-8-2
cudnn-8-2/
sudo cp include/cudnn*.h /usr/local/cuda-11.3/include/
sudo cp lib64/libcudnn* /usr/local/cuda-11.3/lib64/
```

# 环境变量

我这里使用`fish-config`仓库中的`cuda-home`函数切换cuda版本，这里以11.3.1为例。

```fish
cuda-home /usr/local/cuda-11.3
```
