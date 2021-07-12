# 将表导出为CSV文件

## Step 1

如果 `MySQL` 服务器已使用 `–secure-file-priv` 选项启动，则必须使用 `SELinux` 允许 `MySQL` 访问的目录保存输出文件。

```sql
SHOW VARIABLES LIKE "secure_file_priv"
```

例如在 `Ubuntu` 下默认为 `/var/lib/mysql-files/`，只能将输出文件存储在此目录中。

## Step 2

选择表的所有数据并指定输出文件的位置。

```sql
SELECT id, download, COALESCE(gift, ''), COALESCE(cdk, '')
INTO OUTFILE '/var/lib/mysql-files/downlink.csv'
FIELDS TERMINATED BY ','
OPTIONALLY ENCLOSED BY '"'
ESCAPED BY '"'
LINES TERMINATED BY '\n'
FROM downlink;
```

或者使用非正式的 `"\"` 进行转义。

```sql
TABLE downlink
INTO OUTFILE '/var/lib/mysql-files/downlink.csv'
FIELDS TERMINATED BY ','
OPTIONALLY ENCLOSED BY '"'
LINES TERMINATED BY '\n';
```
