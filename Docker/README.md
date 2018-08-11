
# 手順
## ダウンロード
* https://docs.docker.com/docker-for-windows/ にてダウンロードする。

## インストール
1. ダウンロードしたファイルを実行する。
2. Hyper-V veature is not enabled. xxxxx」と言われたらYes.
3. Windowの再起動
4. Windows trayのSettingを実行
5. Shared DriversにてShareするドライブを選択
6. Applyをクリック
7. パスワードを入力する

## CentOS/Ansible
### ダウンロード
* Power Shellにて`docker pull ansible/centos7-ansible`を実行

### 実行
* 現在のdockerイメージの確認

```
PS C:\Users\luke> docker images -a
REPOSITORY                TAG                 IMAGE ID            CREATED             SIZE
ansible/centos7-ansible   latest              f2a16c9283c2        2 days ago          496.6 MB
d4w/nsenter               latest              9e4f13a0901e        10 weeks ago        83.85 kB
```

* Dockerに接続
```Shell
docker run --rm -it ansible/centos7-ansible /bin/bash
```

# Docker imageの作成
## Dcokerファイルが入っている場所に移動

```Shell
cd .\dockerfiles\
ls
```

```
    ディレクトリ: C:\Users\luke\dockerfiles


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       2016/12/07     18:49           8855 ansible.cfg
-a----       2016/12/07     19:01            446 Dockerfile

```

## imageの作成
```Shell
docker build -t ansible-centos7-ssh .
```

## 作成されたimageの確認
```Shell
docker images -a
```

## imageのマウント
```Shell
docker run --rm -it ansible-centos7-ssh /bin/bash
```

# ファイルのコピペ
## 外部 → Docker container内
1.Namesの確認

```
PS C:\Users\luke> docker ps -a
CONTAINER ID        IMAGE                     COMMAND             CREATED             STATUS              PORTS               NAMES
c3982e09c02f        ansible/centos7-ansible   "/bin/bash"         18 minutes ago      Up 18 minutes                           mad_yonath
```

2.フィアルのコピペ

```Shell
docker cp C:\Users\luke\Downloads\ansible.cfg mad_yonath:/etc/ansible
```

## Docker container内 → 外部
```Shell
docker cp <containerId>:/file/path/within/container /host/path/target
```

### 例
1.Docker Container IDの確認
ここでは最近使った順で出力して確認します。

```
PS C:\Users\luke> docker ps -a
CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS                         PORTS               NAMES
5d55b99ee4ea        centos7_ansible       "/bin/bash"              3 days ago          Up 44 minutes                                      tender_lalande
8ede9b8a93b7        cf04d5bfcd27          "/bin/sh -c 'chmod 77"   3 days ago          Exited (1) 50 minutes ago                          pedantic_wright
429f823263c2        1146eec0ab33          "/bin/sh -c 'yum clea"   3 days ago          Exited (1) 53 minutes ago                          gigantic_khorana
2985bed2897c        1146eec0ab33          "/bin/sh -c 'yum clea"   3 days ago          Exited (1) 56 minutes ago                          desperate_banach
349fd1512649        948922cef506          "/bin/sh -c 'chmod 77"   3 days ago          Exited (1) About an hour ago                       distracted_einstein
1e303cced832        centos7               "/bin/bash"              4 days ago          Up 30 hours                                        local-ansible
a6498ae53202        centos7               "/bin/bash"              4 days ago          Up 35 hours                                        sleepy_mirzakhani
ce7a249531cd        ansible-centos7-ssh   "/bin/bash"              5 days ago          Up 42 hours                                        goofy_stonebraker
6af21c7de2d1        ansible-centos7-ssh   "/bin/bash"              5 days ago          Up 42 hours                                        berserk_thompson
51ee42eb08cb        ansible-centos7-ssh   "/bin/bash"              5 days ago          Exited (0) 2 days ago                              suspicious_joliot
a259235f3c82        5ef5711d0680          "/bin/sh -c 'yum inst"   5 days ago          Exited (0) 2 days ago                              silly_gates
```

2.コピペ
```Shell
docker cp 5d55b99ee4ea:/root/.ssh C:\Users\luke\dockerfiles
```


# Dockerのip確認
```Shell
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' sleepy_mirzakhani
```

# Dockerが終了してもcontainerは終了しない仕方
```Shell
docker run -it -d --name local-ansible  -v C:\Users\luke\git\ansible-s5-setup:/ansible-script centos7 /bin/bash
```

# Dockerのすべてのcontainerを削除
```Shell
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
```

# Dockerのすべてのimageを削除
```Shell
docker images -a
docker rmi $(docker images -q)
```

# Docker IMAGE
## CentOS/Redis
https://github.com/zokeber/docker-redis

### pull
```Shell
docker pull zokeber/redis:latest
```

### create
```Shell
docker create -it -p 6379:6379 --name container-redis zokeber/redis
```

### start
```Shell
docker start container-redis
```

### connect
#### Redis cline
```Shell
docker exec -it container-redis redis-cli
```

#### Bash
```Shell
docker run --rm -it zokeber/redis redis-cli
```

### Upgrading
```Shell
docker stop container-redis
docker pull zokeber/redis:latest
```

### Docker runの場合
```Shell
docker run --rm -it -p 6379:6379 --name container-redis zokeber/redis
```