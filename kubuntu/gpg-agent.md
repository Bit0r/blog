# 前言
在设置ssh密钥对的时候，会提示你输入一个密码来加密私钥，这个密码叫`passphrase`。

虽然设置一个`passphrase`更加安全，但是在每次使用私钥的时候都需要输入`passphrase`，这就非常麻烦。

所以我们可以用`gpg-agent`来保存`passphrase`，这样就不用每次都手动输入了。

# 方法
1. 在`~/.gnupg/gpg-agent.conf`的首行添加如下内容
```
enable-ssh-support
```
2. 在`~/.ssh/config`添加以下内容
```
AddKeysToAgent yes
```
3. 重启电脑
