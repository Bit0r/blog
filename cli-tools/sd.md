## 前言

[sd](https://github.com/chmln/sd) 是一个类似 `sed` 的工具，但是它更加容易使用，而且性能更好，下面通过例子来学习使用。

### 修改sql文件

有一个 `1G` 的 `SQL` 备份文件，其中包含大量单行插入。现在要将其转换少量的多行插入，提升导入数据时的运行性能。

#### 输入

```sql
INSERT INTO `movie_genre` VALUES ('43007', '17331', '10');
INSERT INTO `movie_genre` VALUES ('43010', '17332', '4');
INSERT INTO `movie_genre` VALUES ('43009', '17332', '6');
...
...
...
INSERT INTO `movie_genre` VALUES ('43008', '17332', '10');
INSERT INTO `movie_genre` VALUES ('43012', '17333', '6');
```

#### 输出

```sql
INSERT INTO `movie_genre` VALUES ('43007', '17331', '10'),
 ('43010', '17332', '4'),
 ('43009', '17332', '6'),
 ...
 ...
 ...
 ('43008', '17332', '10'),
 ('43012', '17333', '6');
```

#### 代码

```shell
sd ';\s+INSERT INTO `\w+` VALUES' ',\n' movie_recommend_db.sql
```

注意 `pattern` 中必须使用 `\s+`，而不能使用 `\n`。使用 [ripgrep](https://github.com/BurntSushi/ripgrep) 进行搜索时也一样，因为它们都使用 `rust` 正则匹配引擎。
