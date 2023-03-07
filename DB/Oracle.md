# SYSDATE
Querry:
```Shell
SELECT TO_CHAR
    (SYSDATE, 'MM-DD-YYYY HH24:MI:SS') "NOW"
     FROM DUAL;
```

Result:
```Shell
NOW
-------------------
04-13-2001 09:45:51
```


# Sql Developer Date format
1. SQL Developerを起動する。
2. メニューから ツール > プリファレンス を選び、ダイアログを開く。
3. 左の一覧から データベース > NLS を選ぶ。
4. 右の一覧から日付書式(RR-MM-DD)を変更する。(YYYY-MM-DD HH24:MI:SS)
5. 右下のOKボタンを押す。

# Timesten
## document
https://docs.oracle.com/en/database/other-databases/index.html#OracleTimesTenIn-MemoryDatabase


## url sample
```
url: jdbc:timesten:client:TTC_SERVER=localhost;TCP_PORT=12023;TTC_SERVER_DSN=my_dsn;UID=hello;PWD=world;
```

# get oracle version
```
SELECT BANNER, BANNER_FULL FROM v$version;
```