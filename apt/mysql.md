# 问题

在`apt`更新`mysql`时，会在安装过程中卡住。

## 原因

因为`mysql`服务正在后台运行，而`apt`又需要修改`mysql`的配置文件，于是`apt`会一直等待文件锁被释放。

# 解决方案

运行下列命令，杀死所有`mysql`的后台进程。`apt`就能重新获得文件锁，从而让安装继续。

```shell
sudo pkill mysql
```

## 更好的解决方案

在更新`mysql`前，应该停止`mysql`的后台服务

```shell
sudo systemctl stop mysql
```