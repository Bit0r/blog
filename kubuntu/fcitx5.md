## 前言
Kubuntu 20.04默认安装时，安装的是`ibus`输入法和`fcitx4`输入法，但这两个输入法都很老旧且输入体验不好
而新出的`fcitx5`则在输入体验和响应速度上有了明显的提升，所以才使用`fcitx5`输入法

## 安装和配置
1. 在**Muon**内搜索**fcitx5**，将除有`-dev`后缀的包全部安装，如图
![fcitx5](../img/kubuntu/fcitx5/fcitx5.webp)

2. 将`~/.config/fcitx5/profile`改为以下内容
```ini
[Groups/0]
# Group Name
Name=默认
# Layout
Default Layout=us
# Default Input Method
DefaultIM=pinyin

[Groups/0/Items/0]
# Name
Name=keyboard-us
# Layout
Layout=

[Groups/0/Items/1]
# Name
Name=pinyin
# Layout
Layout=

[GroupOrder]
0=默认
```

3. 将`~/.config/fcitx5/conf/pinyin.conf`里的云拼音关闭
```ini
CloudPinyinEnabled=False
```

4. 在开始菜单里启用`Fcitx 5`
![start-menu](../img/kubuntu/fcitx5/start-menu.webp)

5. 清除所有`fcitx`和`ibus`的包，防止冲突
![remove](../img/kubuntu/fcitx5/remove.webp)

6. 删除KDE中的设置插件
![kde-fcitx](../img/kubuntu/fcitx5/kde-fcitx.webp)

7. 重启电脑，默认输入法将变成`Fcitx 5`
