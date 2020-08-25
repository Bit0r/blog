# 前言
Python的包管理工具是`pip`，虚拟环境工具是`venv`。本文介绍它们的使用方法。

# 使用pip

## 给本用户安装和卸载
```fish
pip3 install <package>
pip3 uninstall <package>
```

## 为所有用户安装和卸载
```fish
sudo pip3 install <package>
sudo pip3 uninstall <package>
```

## 安装特定版本的包
在包名称后跟`==`和版本号来安装特定版本的包
```shell
pip3 install requests==2.6.0
```

## 显示有关特定包的信息
```shell
pip3 show requests
```

## 查看和编辑配置文件
```fish
pip3 config list
pip3 config [--editor <editor>] edit
```

## 编辑全局配置文件
```fish
sudo pip3 config --global [--editor <editor>] edit
```

## 换源
1. 这里直接配置全局文件，因为有时候需要将包安装到`/usr/local`下
```shell
sudo pip3 config --global --editor micro edit
```
2. 粘贴以下内容
```ini
[global]
index-url = https://mirrors.huaweicloud.com/repository/pypi/simple
trusted-host = mirrors.huaweicloud.com
timeout = 120
```

# 使用venv

## 创建虚拟环境
请确定要放置它的目录，并将`venv`模块作为脚本运行目录路径，虚拟环境的常用目录位置是`.venv`
```shell
python3 -m venv .venv/
```

## 激活
激活虚拟环境将改变你所用终端的提示符，以显示你正在使用的虚拟环境，并修改环境以使`python`命令所运行的将是已安装的特定`Python`版本。

### bash环境
```shell
source .venv/bin/activate
```

### fish环境
```shell
source .venv/bin/activate.fish
```

## 输出所有安装的包
`pip list`将显示虚拟环境中安装的所有软件包
```shell
pip list
```

## 生成依赖列表
`pip freeze` 将生成一个类似的已安装包列表，但输出使用`pip install`期望的格式，通常将此列表放在`requirements.txt`文件中
```shell
pip freeze > requirements.txt
```

## 从列表安装
可以使用`install -r`解析`requirements.txt`，来安装所有必需的包
```shell
pip install -r requirements.txt
```
