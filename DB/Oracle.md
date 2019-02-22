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