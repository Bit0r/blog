## 前言
Linux系统上自带有一个`find`工具，但是这个工具的搜索速度却不快。
于是就有人写了一个新工具，用来执行快速搜索。

## 安装
### Ubuntu
```fish
sudo apt install fd-find
```

## 快速上手

### 在本目录内搜索名字带有curl的文件
```
> fdfind -g '*curl*'
curl.txt
curl.log
```
`g`标志表示**使用glob模式匹配**，默认使用正则匹配

### 搜索特定的文件扩展名
可以用`-e`标志来搜索特定拓展名的文件。例如，在当前目录下搜索文件扩展名为`md`的文件：
```
> fdfind -e md
README.md
cli-tool/fd.md
kubuntu/alt.md
kubuntu/fcitx5.md
```
这个`-e`选项可以与搜索模式结合使用。例如，在当前目录下搜索文件名包含`reademe`且扩展名为`md`的文件：
```
> fdfind -e md readme
README.md
```

### 指定搜索目录
默认会在当前目录和其下所有子目录中搜索，如果你想搜索指定的目录就需要在第二个参数中指定。
例如，要在指定的`/etc`目录中搜索包含`passwd`关键字的文件或目录：
```
> fdfind -g '*passwd*' /etc
/etc/pam.d/chpasswd
/etc/pam.d/passwd
/etc/passwd
/etc/passwd-
/etc/security/opasswd
```

### 搜索隐藏文件
默认不搜索隐藏文件，需要搜索隐藏文件可以加上`-H`参数。例如，在`~`下搜索名字带有`mycli`的隐藏文件：
```
> fdfind -Hg '*mycli*' ~
/home/bit0r/.mycli.log
/home/bit0r/.mycli-history
/home/bit0r/.myclirc
/home/bit0r/.local/share/fish/generated_completions/mycli.fish
```
