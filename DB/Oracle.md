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

# docker
```
$ docker search oracle-xe
$ docker pull oracleinanutshell/oracle-xe-11g
$ docker run --name oracle11g -d -p 11521:1521 oracleinanutshell/oracle-xe-11g
```

- Host: localhost
- Port: 11521
- system/oracle

## link
- [Mac] Docker를 이용해 oracle-xe-11g 실행하기
    - https://clearstar0817.tistory.com/11

# 인스톨후
```
create user oracleuser identified by password;

grant connect, resource, dba to #user명#
```