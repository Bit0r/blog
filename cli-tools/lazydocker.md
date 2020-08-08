## 前言

docker含有大量命令，这些命令在操作时有些不方便。

而lazydocker就是为了解决这个问题而诞生的，“lazy”顾名思义

## 下载
在[此处](https://github.com/jesseduffield/lazydocker/releases)下载最新的`Linux_x86_64`版`lazydocker`

## 安装
因为使用golang编写，所以这个软件没有依赖，直接就能使用
```shell
sudo install lazydocker /usr/bin/local/
```

## 启动
在终端输入`lazydocker`将启动这个软件

## 界面
![ui](../img/cli-tools/lazydocker/ui.webp)

### 左侧区域
* `Project`是表示项目，一般是工作目录
* `Container`是容器列表，相当于`docker container ls -a`
* `Images`是镜像列表，相当于`docker image ls`
* `Volumes`是卷列表

### 右侧区域
* `Logs`顾名思义，就是Log记录
* `Stats`是状态监控，顶部一般是概览动画，鼠标向下滚动可以查看更详细的信息
* `Config`是配置文件，如果是可编辑的配置则可按`o`键打开(open)配置文件进行编辑
* `Top`展示的是`Container`内的`top`

## 操作
这个软件支持大量快捷键和**鼠标操作**，其中全部快捷键在[此处](https://github.com/jesseduffield/lazydocker/tree/master/docs/keybindings)，这里主要介绍最常规的操作方式。

鼠标单击即可选择菜单选项或者切换区域，界面上的所以按钮都能用鼠标点击。

按下`x`键可以打开该区域所对应的菜单，鼠标单击进行选择。

其中有两个选项拥有子菜单，分别是`run predefined custom command`(运行预定义的用户命令)和`view bulk commands`(查看批量命令)。\
其中的用户命令一般是一些实用命令，而批量命令则一般是管理命令。

`esc`键返回上级菜单或者退出软件。
