# ユーザ
## グループの作成
```Javascript
groupadd yoda
```

## ユーザの作成
useradd -g グループ名 ユーザ名
```Javascript
useradd -g yoda yoda
```

## パスワードの設定
```Javascript
passwd yoda
ユーザー yoda のパスワードを変更。
新しいパスワード:
新しいパスワードを再入力してください:
passwd: 全ての認証トークンが正しく更新できました。
```

## 管理権限の付与
作成したユーザに対して管理者権限を付与する。
```Javascript
visudo
```

`root    ALL=(ALL) ALL`と書かれている下あたりに
```Javascript
yoda	ALL=(ALL)	ALL
```
を追加し保存する。

## ユーザが接続しているgroupの確認
```Javascript
groups
```

# munpack
https://centos.pkgs.org/6/repoforge-x86_64/mpack-1.6-2.el6.rf.x86_64.rpm.html

## Download the latest rpmforge-release rpm from
http://ftp.tu-chemnitz.de/pub/linux/dag/redhat/el6/en/x86_64/rpmforge/RPMS/

## Install rpmforge-release rpm:
```Shell
# rpm -Uvh rpmforge-release*rpm
```

or

```Shell
# yum install mpack
```

## 添付ファイルの解凍
### 解凍
```Shell
$ munpack メール
```

### 添付ファイルの生成
例えば上記の実行で
`=XUTF-8XBX5bed5Y+j5bqXKDMwOClfMjAxNzAyMDEuY3N2X=`というファイルが生成される。

### Reading
```
$ cat 生成されたファイル

```

# Bash
### version up

```Shell
$ brew update && brew install bash
```

### Bash color
https://misc.flogisoft.com/bash/tip_colors_and_formatting

### My Bash color
```Shell
PS1='\e[92m[\u@\h:\e[95m/\W\e[92m]\$ '
```

`/etc/bashrc`ファイルに追加する。

すぐ反映さえるためには
```Shell
$ source /etc/bashrc
```

# Change timezone
```Shell
# mv /etc/localtime /etc/localtime.backup
# ln -s /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
```

# Curl
https://curl.haxx.se/

## POST
### -d (--data)
POSTで設定される。POSTのデータは` "param1=value1&param2=value2"`の形式で渡す。
```Shell
curl -d "first_name=Bruce&last_name=Wayne&press=%20OK%20" http://posttestserver.com/post.php
```

## GET
```Shell
curl "http://111.111.111.111:8080/service.jsp?req=1234"
```

## HTTPS通信
| オプション | 内容 |
|:-------------|:-----|
| --sslv2 | SSL2.0で通信 |
| --sslv3 | SSL3.0で通信 |
| --tlsv1 | TLS1.Xで通信 |
| --tlsv1.0 | TLS1.0で通信 |
| --tlsv1.1 | TLS1.1で通信 |
| --tlsv1.2 | TLS1.2で通信 |
| -k | 危なそうな証明書でも通信してくれる |
| -v | 通信時の色々な情報を出してくれる |
| -s | 無駄な情報は省いてくれる |

# File転送
### 外からここに
```Shell
scp username@hostname:/path/to/remote/file /path/to/local/file
```

### ここから外へ
```Shell
scp /path/to/local/file username@hostname:/path/to/remote/file
```

### 外から外へ
```Shell
scp username1@hostname1:/path/to/file username2@hostname2:/path/to/other/file
```

### 複数ファイル転送
#### 外からここに
```Shell
scp ユーザー名@ホスト:/home/yoda/\{yoda201408010005.tsv,yoda201507010005.tsv,yoda201605010005.tsv\} .
```

## その他
| short | long | 説明 | 備考 |
|:-------------:|:-------------:|:-------------|:-------------|
| -k | --insecure | httpsサイトをSSL certificate検証なしで接続する | wgetの--no-check-certificateと似ている|
| -l | --head | HTTP headerのみ表示する | |
| -D | --dump-header <file> | <file>にHTTP headerを記録する | |
| -L | --location | サーバーからHTTP 301または302のレスポンスが来る場合、redirection URLに行く。<br>--max-redirsの後ろに数字でredirectionに何回行くかを指定可能。デフォルトは50 ||
| -v | --verbose | 詳細を出力する | wgetの--no-check-certificateと似ている|
| -o | --output FILE | FILEに結果を保存する(downloadしたい場合) | |
| -O | --remote-name | file保存する時、remoteのfile名で保存する。-oより便利 | |
| -s | --silent | サイレントモード。 | HTTP response codeのみ見たい場合使えば良い。|

# その他
## ファイル名にDateを使用

```Text
bash -x yoda.sh 2>&1 | tee "yoda_work_$(date +"%Y_%m_%d_%I_%M_%p").log"
```

## ポートの確認
```Text
$ netstat -ntplo
```

## Crontablのインストール
※Cent OS 7の場合
```Shell
yum install cronie
```

## alternatives jdk
```Shell
# alternatives --install /usr/bin/java java /opt/jdk1.7.0_79/bin/java 1
# alternatives --install /usr/bin/java java /opt/jdk1.8.0_45/bin/java 2
# alternatives --config java

There is 2 program that provides 'java'.

  Selection    Command
-----------------------------------------------
   1           /opt/jdk1.7.0_79/bin/java
** 2           /opt/jdk1.8.0_45/bin/java
Enter to keep the current selection[+], or type selection number:
```

## Install Maven by YUM
```Shell
sudo wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo
sudo sed -i s/\$releasever/6/g /etc/yum.repos.d/epel-apache-maven.repo
sudo yum install -y apache-maven
mvn --version```

## 起動時に特定のshを実行
https://qiita.com/mikoto/items/d0777c39b874d5abfd1e
1.実行するshの作成
例：mystart

```Shell
#!/bin/sh
# chkconfig: 4 98 20
# description: after start, run apache and tomcat
# processname: exam

/home/ec2-user/exam/apache/bin/./apachectl start
/home/ec2-user/exam/tomcat/bin/./startup.sh
```

2./etc/init.dに配置する
```Shell
$ cp mystart /etc/init.d
```

3.chkconfigに登録
```Shell
$ chkconfig --add mystart
$ chkconfig mystart on
```

4.確認
```
[ec2-user@ip-172-31-12-73 ~]$ sudo chkconfig --list | grep mystart
mystart        	0:off	1:off	2:on	3:on	4:on	5:on	6:off
```

## Install Chrome
1.linux用のchromeのrpmファイルをダウンロード
https://www.google.com/chrome/browser/desktop/index.html?brand=CHBD&gclid=EAIaIQobChMIjLGuxbj31wIVkjUrCh3s2gsBEAAYASAAEgLPRfD_BwE
2.yumにてインストールする
```Shell
yum install ./google-chrome-stable_current_x86_64.rpm
```

## rpm
### -i オプション（install の略）
パッケージをインストールする

### -v オプション（verbose の略）
詳細なログを表示させる

### -h オプション（hash mark の略）
進捗状況を表示させる

### -U
既に入っているパッケージをアップデートする場合使う。このオプションを使うとパッケージが既に入っている場合にはアップデートし、入っていない場合には新規にインストールするため、
実際にはアップデートでも新規インストールでも使うことが多い。

```Shell
# rpm -Uvh http://repo.webtatic.com/yum/centos/5/latest.rpm
```

### 例
```Shell
# rpm -ivh http://repo.webtatic.com/yum/centos/5/latest.rpm
warning: /var/tmp/rpm-xfer.JhDMCy: Header V3 DSA signature: NOKEY, key ID cf4c4ff9
Preparing...                ########################################### [100%]
   1:webtatic-release       ########################################### [100%]
```

## JDK設定
```Shell
 export JAVA_HOME=/root/sample-selenide-web-test/jdk1.8.0_151
 export PATH=$PATH:$JAVA_HOME
```

ssh config
```Shell
#For Mac OS Sierra
AddKeysToAgent yes
UseKeychain yes
HostKeyAlgorithms +ssh-dss

Host *
    ForwardAgent yes

Host loginp
    HostName xxx.xxxx.xxx
    User yoda
```

## SSH public key add to Remote server
```Shell
ssh-copy-id user@remote_server
```

or

```Shell
cat ~/.ssh/id_rsa.pub | (ssh user@host "cat >> ~/.ssh/authorized_keys")
```

## grep to file
```Shell
grep -n "YOUR SEARCH STRING" * > output
```

## csvファイルの行数確認
```Shell
wc -l < ファイル名.tsv
```

# Regex検索
```Shell
rpm -qa | grep '\bcurl'" -h aaa.co.jp
```

# SSH
## 新しいSSHキーの作成
- 現在使用している鍵の暗号強度の確認
```Shell
$ ssh-keygen -l -f ~/.ssh/id_rsa.pub
4096 SHA256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx your_email@example.com (RSA)
```

- 新しいSSHキーの作成
1.-Cのコメント部分を入れ替えて、以下のコマンドを実行
```Shell
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

2.SSH Keysの保存先を聞かれているので、特に気にしなければそのままEnterを入力
```Shell
Enter file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]
```

3.パスフレーズの入力を求められるので、入力
```Shell
Enter passphrase (empty for no passphrase): [Type a passphrase]
# Enter same passphrase again: [Type passphrase again]
```

## Check SSH port
```Shell
$ sudo grep Port /etc/ssh/sshd_config
```

#zip
## zip with pw
```
zip -er [ZIP 파일의 경로와 이름] [압축 대상의 경로와 이름]

ex) zip -er ~/Downloads/file.zip ~/Downloads/file.png
```