# LiveCD

## 制作
1. 从北京外国语镜像站中下载[iso文件](https://mirrors.bfsu.edu.cn/ubuntu-cdimage/kubuntu/releases/groovy/release/kubuntu-20.10-desktop-amd64.iso)
2. Windows下使用[Rufus](https://github.com/pbatard/rufus/releases/download/v3.11/Rufus-3.11.appx)将镜像写入U盘

## 启动
1. 引导加载前按`F7`进入`UEFI模式`
2. 选择进入`LiveCD`
3. 在开机前按`Esc`进入`Grub2菜单`
4. 选择`Start Kubuntu (safe graphics)`

# 安装

## 开始安装
选择语言为**中文（简体）**，然后点击**安装 Kubuntu**
![开始](../img/kubuntu/install/start.png)

## 键盘布局
键盘布局不需要修改

## 安装方案
选择*最小安装*，不要勾选*安装Kubuntu时下载更新*，勾选*为图形或无线硬件，以及其它媒体格式安装第三方软件*
![软件](../img/kubuntu/install/software.png)

## 磁盘配额
### 安装类型
安装类型选择*手动*
![分区](../img/kubuntu/install/disk.png)

### 我的电脑
我的内存是16G，硬盘有两个：一个128G SSD和一个1T HDD。
所以我的方案并不一定能直接照搬到其它电脑上，但是这个方案具有一定的参考性。

### 分区大小

* *引导分区*一个，SSD上分配`512M`，文件格式`FAT32`，挂载点`/boot/efi`\
(如果是双系统，就直接挂载到Windows的EFI分区，而且**不需要格式化此分区**)

* *交换分区*一个，SSD上分配`20GB`，文件格式`交换空间`，具体分区大小请参照[SwapFaq](https://help.ubuntu.com/community/SwapFaq)

* *根分区*一个，剩余所有SSD空间，文件格式`Ext4 日志文件系统`，挂载点`/`

* *日志分区*一个，HDD上分配`240GB`，文件格式`Ext4 日志文件系统`，挂载点`/var`

* *家分区*一个，剩余所有HDD空间，文件格式`Ext4 日志文件系统`, 挂载点`/home`
