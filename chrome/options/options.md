# 命令行选项

chrome有很多命令行选项，有些选项非常实用，这里介绍一些。

## 减少cpu和内存消耗

以下选项可以显著减少cpu和内存消耗

```shell
google-chrome --disable-gpu-sandbox --in-process-gpu --process-per-site
```

## 设置代理

以下是chrome设置代理的选项用法

```shell
google-chrome --proxy-server='socks://localhost'	# socks5代理
google-chrome --proxy-server='http://localhost:8800'	# http代理
```

# 添加到.desktop文件

1.在应用程序菜单找到chrome启动器图标

![菜单](menu.avif)

2.在图标上右键，选择“编辑应用程序”

3.在“应用程序”选项卡中，找到“命令”输入框，添加上面的选项

![编辑应用程序](edit.avif)
