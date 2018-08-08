
# Archiveログ出力
`postgresql.conf`ファイルを修正

```Text
archive_mode = on # allows archiving to be done
# (change requires restart)

archive_command = 'cp %p /home/yoda/arch/%f' # command to use to archive a logfile segment

# placeholders: %p = path of file to archive
# %f = file name only
# e.g. 'test ! -f /mnt/server/archivedir/%f && cp %p /mnt/server/archivedir/%f'

archive_timeout = 600 # force a logfile segment switch after this
# number of seconds; 0 disables

wal_level = archive # minimal, archive, or hot_standby
# (change requires restart)
```

※Windowsの場合

```Text
archive_command = ‘copy “%p” “C:\\archive\\%f” ‘ または ‘c:\\execute_archive.bat’.
```
 
## ログにsqlを出力する場合
```Text
#log_min_duration_statement = 10s # -1 is disabled, 0 logs all statements
log_min_duration_statement = 0 # -1 is disabled, 0 logs all statements

log_line_prefix = '%t: %p: %d: %u: ' # special values:
```

# Binary検索
```SQL
select encode(parameter, 'escape'), operation_start_dm, user_serial from log where encode(parameter, 'escape') like '%キーワード%'
and operation_start_dm > '20171207000000' and operation_id = '検索ID';
```

### 日本語が入った場合
```SQL
select convert_from(parameter, 'UTF-8'), operation_start_dm, user_serial from log where convert_from(parameter, 'UTF-8') like '%キーワード%'
and operation_start_dm > '20171207000000' and operation_id = '検索ID';
```

# Copy databse
※dbに接続しているプロセスを全部終了してから実行
```sql
CREATE DATABASE newdb WITH TEMPLATE originaldb OWNER dbuser;
```

### エラーが起きる場合
`ERROR:  source database "originaldb" is being accessed by other users`というメッセージが出る場合、下記の実行する
```sql
SELECT pg_terminate_backend(pg_stat_activity.pid) FROM pg_stat_activity 
WHERE pg_stat_activity.datname = 'originaldb' AND pid <> pg_backend_pid();
```

# 拡張表示
```Shell
\x on
```