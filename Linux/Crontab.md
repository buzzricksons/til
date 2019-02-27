# logging
On a default installation the cron jobs get logged to

```Shell
/var/log/syslog
```

You can see just cron jobs in that logfile by running

```Shell
 grep CRON /var/log/syslog
 ```
 
If you haven't reconfigured anything,the entries will be in there.

# Time
https://crontab.guru/