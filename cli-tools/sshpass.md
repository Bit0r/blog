# 前言
如果你有一台工作环境的ssh服务器，验证方式不是使用密钥对而是密码。
那么你每次登陆ssh都需要输入密码，这会令人抓狂，幸运的是有个软件可以免除你的痛苦。

# 安装
```fish
sudo apt install sshpass
```

# 使用
## 登陆ssh
```fish
sshpass -p 'your_password' ssh <remote_username>@<remote_host>
```

## 登陆mosh
```fish
sshpass -p 'your_password' mosh <remote_username>@<remote_host>
```

# 配合konsole
KDE下的神级终端`konsole`可以[创建标签页](../kubuntu/konsole.md#配置方案)，配合`sshpass`食用更佳哦😉
