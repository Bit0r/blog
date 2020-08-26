<!-- TOC -->

- [前言](#%E5%89%8D%E8%A8%80)
- [安装](#%E5%AE%89%E8%A3%85)
- [连接](#%E8%BF%9E%E6%8E%A5)
    - [连接方法](#%E8%BF%9E%E6%8E%A5%E6%96%B9%E6%B3%95)
    - [参数](#%E5%8F%82%E6%95%B0)
- [查询](#%E6%9F%A5%E8%AF%A2)
    - [获取游标](#%E8%8E%B7%E5%8F%96%E6%B8%B8%E6%A0%87)
    - [执行SQL](#%E6%89%A7%E8%A1%8Csql)
    - [拉取结果集](#%E6%8B%89%E5%8F%96%E7%BB%93%E6%9E%9C%E9%9B%86)
    - [拉取全部](#%E6%8B%89%E5%8F%96%E5%85%A8%E9%83%A8)
    - [游标重用](#%E6%B8%B8%E6%A0%87%E9%87%8D%E7%94%A8)
    - [关闭游标](#%E5%85%B3%E9%97%AD%E6%B8%B8%E6%A0%87)
- [插入多行](#%E6%8F%92%E5%85%A5%E5%A4%9A%E8%A1%8C)
- [关闭连接](#%E5%85%B3%E9%97%AD%E8%BF%9E%E6%8E%A5)
    - [提交](#%E6%8F%90%E4%BA%A4)
    - [关闭连接](#%E5%85%B3%E9%97%AD%E8%BF%9E%E6%8E%A5)

<!-- /TOC -->

# 前言
Python有很多MySQL驱动，其中`mysql-connector`是oracle官方推出的MySQL驱动，本文介绍其用法

# 安装
这是Ubuntu下的安装方法，其它安装方法我也不会（：
```shell
sudo apt install mysql-connector-python
```

# 连接
操作数据库，首先要连接数据库
```py
import mysql.connector

cnx = mysql.connector.connect(user='root',
                              password='$troNgP@$$w0rd',
                              database='wrmyx',
                              autocommit=True)
```

## 连接方法
连接数据库的方法是`connect`，它接受一些连接参数，返回一个数据库连接句柄

## 参数
`connect`可以函数接受接受很多参数，这里重点其中几个参数
* `user`是MySQL登录用户
* `password`是MySQL的连接密码（可选）
* `host`是连接的主机，默认是`127.0.0.1`（可选）
* `port`是连接的端口，默认是`3306`（可选）
* `database`是默认选择的数据库（可选）
* `autocommit`指示是否开启自动提交模式，默认为`False`（可选）

# 查询
```py
cursor = cnx.cursor(prepared=True)

query = '''
SELECT activation_code
FROM download_link
WHERE id = ?
'''

cursor.execute(query, (193, ))

# result=list(cursor)
for (activation, ) in cursor:
    print(activation)

cursor.close()
```

## 获取游标
要进行查询，首先要获取一个`cursor`（游标），参数`prepared=True`表示开启SQL准备，**这个不能省略**

## 执行SQL
`cursor`的`execute`方法用于执行一个准备好的SQL语句。
其第一个参数是一个字符串——预处理SQL语句，第二个参数是一个元组——传入的参数。

当一个SQL语句第一次被执行时会进行准备，而后这个语句就会被缓存，第二次执行相同的语句就会直接传递参数。

语句中的`?`是占位符，每个`?`占位符都与元组中的元素相对应。

## 拉取结果集
调用过`execute`方法后可以对`cursor`进行迭代，每次迭代将返回结果集中的一行，每一行被表示为一个`tuple`

## 拉取全部
如果想直接拉取全部结果，可以用`list(cursor)`来获取一个包含所有元组的列表

## 游标重用
一个游标可以进行重复查询，但是需要确保游标的结果集已经为空——即所有的行都被拉取

## 关闭游标
不再使用的游标需要调用`close`进行关闭。

# 插入多行
```py
query = '''
INSERT INTO download_link (id, download)
VALUES (?, ?)
'''
cursor.executemany(query, [(1, 'http://example.com'),
                           (2, 'http://second.example.com')])
```
有一个专门进行多行插入的方法`executemany`。
该方法第一个参数还是查询语句，但第二个参数需要传递一个参数元组的可迭代对象。

这个方法执行时会转换查询语句来提升插入效率，例如上面的查询语句将被转换为：
```sql
INSERT INTO download_link (id, download)
VALUES (?, ?), (?, ?)
```

# 关闭连接
```py
# cnx.commit()
cnx.close()
```

## 提交
如果没有开启自动提交模式，则需要使用`commit`方法手动提交事务。

## 关闭连接
`close`方法用于关闭连接，此时所有`cursor`都将被关闭
