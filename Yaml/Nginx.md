# CentOS 8 problem
```
Error: Failed to download metadata for repo 'appstream'
```

対応
```
[root@autocontroller ~]# cd /etc/yum.repos.d/
[root@autocontroller ~]# sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*
[root@autocontroller ~]# sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*
[root@autocontroller ~]# yum update -y
```