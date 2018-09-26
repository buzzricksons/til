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