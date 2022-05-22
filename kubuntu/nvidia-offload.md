# 开启 Nvidia On-Demand 模式

## 前言

现在的 Nvidia Prime 支持开启 On-Demand 模式。顾名思义就是在需要的时候才使用独显，一般情况使用核显更省电。不过由于自动切换不太成熟，所以需要手动指定程序在独显下运行。

## 开启 On-Demand 模式

在 `nvidia-settings` 里找到 `PRIME Profiles`，选定 `Nvidia Ob-Demand`。模式切换完成后需要重启才能生效。

![nvidia-setting](../img/kubuntu/nvidia-offload/nvidia-setting.png)

## 环境变量

在 `Ubuntu` 下，使用 `Nvidia` 来运行程序需要手动指定环境变量，开启 `Nvidia-Offload`。

```ini
DRI_PRIME=1
__NV_PRIME_RENDER_OFFLOAD=1
__GLX_VENDOR_LIBRARY_NAME=nvidia
__VK_LAYER_NV_optimus=NVIDIA_only
VK_ICD_FILENAMES=/usr/share/vulkan/icd.d/nvidia_icd.x86_64.json
```

## 修改应用快捷方式

以百度网盘为例，百度网盘可以播放视频，适合使用GPU来解码。
方法是编辑应用程序桌面快捷方式，在执行路径之前加上环境变量。

![nvidia-setting](../img/kubuntu/nvidia-offload/desktop-shortcut.png)

## Steam

`Steam` 中的启动游戏可以附带参数，可以将环境变量写到启动参数里。
这里以饥荒为例，**库**->**右键单击饥荒**->**属性**->**通用**->**启动选项**，填写以下命令。

```shell
... %command%
```

`%command%` 用于替代 `Steam` 将在您启动游戏时内部使用的实际游戏命令，前面的`...`省略的是环境变量。

![steam](../img/kubuntu/nvidia-offload/steam.png)

## Q4Wine

有时我们需要在 `Wine` 下运行一些需要 `Nvidia` 的软件，解决方案是在 `Q4Wine` 中添加前缀。

**前缀**->**创建新的**。

![new-prefix](../img/kubuntu/nvidia-offload/new-prefix.png)

名称填 `Game`，其它都省缺。在**高端**的 `%ENV_ARGS%` 之后加上环境变量。

![prefix-args](../img/kubuntu/nvidia-offload/prefix-args.png)

下次运行需要 `Nvidia` 的软件时选择 `Game` 即可，以*植物大战僵尸*为例。

![q4wine-game](../img/kubuntu/nvidia-offload/q4wine-game.png)
