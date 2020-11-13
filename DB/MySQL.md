# datetime formatエラー
```Shell
updated datetime NOT NULL DEFAULT '0000-00-00 00:00:00'

ERROR 1067 (42000): Invalid default value for 'updated'
```

### sql_modeの確認
```Shell
SHOW VARIABLES LIKE 'sql_mode';
```

### 対応
https://stackoverflow.com/questions/36374335/error-in-mysql-when-setting-default-value-for-date-or-datetime/36374690#36374690
```Shell
SET sql_mode = '';
```

# Result to file
```Shell
mysql -uroot -p -e "select * from database_name.table_name" > filename.txt
```

### ex
```Sql
mysql -h ホスト -uyoda -p -e "select a, b from mytable where fav= 1" dbname > result.txt
```

# 起動
```Shell
mysql.server start
```

# install
```Shell
brew install mysql@5.7
```

### link
```Shell
brew link mysql@5.7 --force
```

# パスワード変更
```Shell
sudo mysql

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'your password';
```

# 情報
### port
```Shell
mysql> SHOW VARIABLES WHERE Variable_name = 'port';

+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| port          | 3306  |
+---------------+-------+
1 row in set (0.00 sec)
```

### hostname
```Shell
mysql> SHOW VARIABLES WHERE Variable_name = 'hostname';

+-------------------+-------+
| Variable_name     | Value |
+-------------------+-------+
| hostname          | Dell  |
+-------------------+-------+
1 row in set (0.00 sec)
```

### username
```Shell
mysql> select user();

+----------------+
| user()         |
+----------------+
| root@localhost |
+----------------+
1 row in set (0.00 sec)
```

# docker time zone setting
```
$ docker run -it --rm -e TZ='Asia/Tokyo' mysql:5.7 date
```