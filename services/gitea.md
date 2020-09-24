# 目录
<!-- TOC -->

- [数据库准备](#%E6%95%B0%E6%8D%AE%E5%BA%93%E5%87%86%E5%A4%87)
    - [创建数据库](#%E5%88%9B%E5%BB%BA%E6%95%B0%E6%8D%AE%E5%BA%93)
    - [创建用户和授予权限](#%E5%88%9B%E5%BB%BA%E7%94%A8%E6%88%B7%E5%92%8C%E6%8E%88%E4%BA%88%E6%9D%83%E9%99%90)
- [安装](#%E5%AE%89%E8%A3%85)
    - [下载](#%E4%B8%8B%E8%BD%BD)
    - [建议的服务器配置](#%E5%BB%BA%E8%AE%AE%E7%9A%84%E6%9C%8D%E5%8A%A1%E5%99%A8%E9%85%8D%E7%BD%AE)
        - [准备环境](#%E5%87%86%E5%A4%87%E7%8E%AF%E5%A2%83)
        - [创建所需的目录结构](#%E5%88%9B%E5%BB%BA%E6%89%80%E9%9C%80%E7%9A%84%E7%9B%AE%E5%BD%95%E7%BB%93%E6%9E%84)
- [运行Gitea](#%E8%BF%90%E8%A1%8Cgitea)
    - [配置文件](#%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6)
    - [激活单元](#%E6%BF%80%E6%B4%BB%E5%8D%95%E5%85%83)
- [首次启动](#%E9%A6%96%E6%AC%A1%E5%90%AF%E5%8A%A8)
    - [数据库设置](#%E6%95%B0%E6%8D%AE%E5%BA%93%E8%AE%BE%E7%BD%AE)
    - [服务器和第三方服务设置](#%E6%9C%8D%E5%8A%A1%E5%99%A8%E5%92%8C%E7%AC%AC%E4%B8%89%E6%96%B9%E6%9C%8D%E5%8A%A1%E8%AE%BE%E7%BD%AE)
    - [管理员帐号](#%E7%AE%A1%E7%90%86%E5%91%98%E5%B8%90%E5%8F%B7)
- [命令](#%E5%91%BD%E4%BB%A4)
    - [web](#web)
        - [选项](#%E9%80%89%E9%A1%B9)
        - [实例](#%E5%AE%9E%E4%BE%8B)
        - [注意](#%E6%B3%A8%E6%84%8F)
- [备份与恢复](#%E5%A4%87%E4%BB%BD%E4%B8%8E%E6%81%A2%E5%A4%8D)
    - [备份](#%E5%A4%87%E4%BB%BD)
    - [恢复](#%E6%81%A2%E5%A4%8D)
        - [例子](#%E4%BE%8B%E5%AD%90)

<!-- /TOC -->

# 数据库准备

## 创建数据库
使用UTF-8字符集和排序规则创建数据库。一定要使用`utf8mb4`字符集而不是`utf8`，因为前者是支持所有Unicode字符（包括表情符号）的*基本多语平面*。
```sql
CREATE DATABASE gitea CHARACTER SET 'utf8mb4' COLLATE 'utf8mb4_unicode_ci';
```

## 创建用户和授予权限
创建Gitea将使用的数据库用户，通过密码进行身份验证。同时将数据库的权限全部授予该用户
```sql
CREATE USER 'gitea'@'localhost' IDENTIFIED BY '$troNgP@$$w0rd';
GRANT ALL PRIVILEGES ON gitea.* TO 'gitea'@'localhost';
```
主机名和密码可以根据自己的实际需求进行更改

# 安装

## 下载
从[下载页面](https://dl.gitea.io/gitea/)选择匹配的平台文件，并替换下面的URL命令
```shell
wget -O gitea https://dl.gitea.io/gitea/1.12.4/gitea-1.12.4-linux-amd64
sudo install gitea /usr/local/bin/
```

## 建议的服务器配置

### 准备环境
检查服务器上是否安装了Git。如果没有，请先安装。
```shell
git --version
```

创建git用户以运行Gitea
```shell
adduser \
   --system \
   --shell /bin/sh \
   --gecos 'Git Version Control' \
   --group \
   --disabled-password \
   --home /home/git \
   git
```

### 创建所需的目录结构
```shell
mkdir -p /var/lib/gitea/{custom,data,log}/
chown -R git:git /var/lib/gitea/
chmod -R 750 /var/lib/gitea/
mkdir /etc/gitea/
chown root:git /etc/gitea/
chmod 770 /etc/gitea/
```

**注意**：注：为`git`用户临时设置了`/etc/gitea`写入权限，以便Web安装程序可以编写配置文件。安装完成后，建议使用以下方式将权限设置为只读：
```shell
chmod 750 /etc/gitea
chmod 640 /etc/gitea/app.ini
```

# 运行Gitea

## 配置文件
参考[gitea.service](https://github.com/go-gitea/gitea/raw/master/contrib/systemd/gitea.service)，配置`/etc/systemd/system/gitea.service`。

关于systemd的配置文件，可以参考[Systemd入门教程](http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-part-two.html)

修改`user`，`home`目录以及其他必须的初始化参数，如果使用自定义端口，则需修改`PORT`参数，反之如果使用默认端口则需删除`-p`标记。

我的配置[在此处](https://gist.githubusercontent.com/Bit0r/5a818bcb70ccc08347814bec1e1977d8/raw/9a659f98941cd9962c1fc6c8462c8df0d06f0b56/gitea.service)

## 激活单元
激活`gitea`并将它作为系统自启动服务：
```shell
sudo systemctl enable gitea
sudo systemctl start gitea
```

# 首次启动
打开<http://localhost:3000>，点击注册配置Gitea服务器

## 数据库设置
1. 字符集：`utf8mb4`

## 服务器和第三方服务设置
1. 勾选*启用验证码*和*启用页面访问限制*
2. 隐藏邮箱地址：noreply.yuschool.cn

## 管理员帐号
首个注册用户将成为管理员。

# 命令
此处只会介绍主要命令，详情请看[gitea官方文档](https://docs.gitea.io/zh-cn/command-line/)

## web
启动服务器：

### 选项
* `--port number`，`-p number`：端口号。可选。（默认：3000）

### 实例
* `gitea web`
* `gitea web --port 80`

### 注意
* Gitea不应作为root用户运行。

# 备份与恢复
Gitea目前有一个`dump`命令将数据保存到zip文件。此文件可以解包并用于恢复实例。

## 备份
切换用户运行Gitea：`su git`，运行`gitea dump -c /etc/gitea/app.ini`。
这个命令会在目录下输出一个名叫`gitea-dump-<timestamp>.zip`的文件，它有如下内容：
* `app.ini`
* `custom/`
* `data/`
* `gitea-db.sql`
* `gitea-repo.zip`
* `log/`

## 恢复
当前不支持恢复命令，所以需要手动将文件移动到正确的位置并恢复数据库转储。

### 例子
```shell
unzip gitea-dump-1482906742.zip
cd gitea-dump-1482906742

mv app.ini /etc/gitea/
unzip gitea-repo.zip
mv gitea-repo/* /home/git/gitea-repositories/
chown -R git:git /etc/gitea/ /home/git/gitea-repositories/

mysql --default-character-set=utf8mb4 -u$USER -p$PASS $DATABASE <gitea-db.sql
systemctl restart gitea
```
