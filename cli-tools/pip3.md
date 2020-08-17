# 前言
Python的包管理工具是pip，本文介绍其使用方法

# 使用方法

## 给本用户安装和卸载
```fish
pip3 install <package>
pip3 uninstall <package>
```

## 全局安装和卸载
```fish
sudo pip3 install <package>
sudo pip3 uninstall <package>
```

## 查看和编辑配置文件
```fish
pip3 config list
pip3 pip config [--editor <editor>] edit
```

## 编辑全局配置文件
```fish
sudo pip3 pip config --global [--editor <editor>] edit
```

## 换源
这里直接配置全局文件，因为有时候需要将包安装到`/usr/local`下
```fish
sudo pip3 config --global --editor micro edit
```
粘贴以下内容
```ini
[global]
index-url = https://mirrors.huaweicloud.com/repository/pypi/simple
trusted-host = mirrors.huaweicloud.com
timeout = 120
```
