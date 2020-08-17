# 前言
Discover有一个bug，就是系统的代理配置不能即时反馈到Discover中，这会导致无法联网

# 复现方法
1. *KDE设置->网络->设置->代理->使用手动配置的代理服务器*，然后配置代理
2. 打开*Discover*，此时*Discover*将使用系统代理进行更新操作，等待更新完毕
3. 关闭*Discover*
4. 勾选*KDE设置->网络->设置->代理->无代理*
5. 再次打开*Discover*，提示无法连接到代理，且无法下载软件

# 解决方法

## 重启后台服务
其原因是修改的配置没有写入数据库，强制重启服务可以使其重写数据
```fish
systemctl restart packagekit
```

## 修改数据库
如果上述方法无效，则需要手动编辑sqlite3配置文件

1. 安装litecli客户端（已经安装则可以跳过）
```fish
sudo pip3 install litecli
sudo litecli /var/lib/PackageKit/transactions.db
```

2. TRUNCATE proxy表
```sql
DELETE FROM proxy
```
