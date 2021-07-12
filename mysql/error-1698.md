# 无法用root用户连接

## 问题

在 `Ubuntu` 系统中安装 `MySQL` 后通常无法用 `root` 用户直接登录，即使密码输入正确。

一般给出的报错为 `ERROR 1698 (28000): Access denied for user 'root'@'localhost'`.

## 原因

在 `Ubuntu` 系统上，`root` 用户默认使用 `auth_socket` 认证插件，即 `MySQL` 的 `root` 用户只能被 **主机** 的 `root` 用户登录。

执行以下命令将直接以 `root` 用户登录 `MySQL`，不需要数据库密码。

```shell
sudo mysql
```

## 解决方案

新建一个 `super` 用户来做超级管理员，而 `root` 用户则保留作为根用户。

```sql
CREATE USER 'super'@'localhost' IDENTIFIED BY 'YOUR_PASSWD';
GRANT 'root'@'localhost' TO 'super'@'localhost';
SET DEFAULT ROLE ALL TO 'super'@'localhost';
^D
```
