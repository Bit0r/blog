## 前言
Kubuntu 20.04默认安装时，安装的是`ibus`输入法和`fcitx4`输入法，但这两个输入法都很老旧且输入体验不好
而新出的`fcitx5`则在输入体验和响应速度上有了明显的提升，所以才使用`fcitx5`输入法

## 安装和配置
1. 添加PPA
```shell
sudo add-apt-repository ppa:liuwenguo/fcitx5test
sudo apt update
```

2. 在*Muon*内选择*过滤*->*按来源*->*fcitx5*，将没有`-dev`后缀的包全部安装
![fcitx5](../img/kubuntu/fcitx5/install.webp)

3. 转到*设置*->*区域设置*->*输入法*，勾选*显示高级选项*，然后取消勾选*全角字符*、*快速输入*、*简繁转换*和*剪贴板*
![高级选项](../img/kubuntu/fcitx5/advanced_options.webp)

4. 取消勾选*显示高级选项*，然后在*模块*->*云拼音*上点击右侧的配置按钮，选择*后端*为`Baidu`
![云拼音](../img/kubuntu/fcitx5/cloud.webp)

5. 在开始菜单里启用`Fcitx 5`
![start-menu](../img/kubuntu/fcitx5/start-menu.webp)

6. 清除所有`fcitx`和`ibus`的包，防止冲突
![remove](../img/kubuntu/fcitx5/remove.webp)

7. 删除KDE中的设置插件
![kde-fcitx](../img/kubuntu/fcitx5/kde-fcitx.webp)

8. 重启电脑，默认输入法将变成`Fcitx 5`
