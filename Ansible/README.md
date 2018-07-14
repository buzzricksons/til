

# Ansibleのインストール
```Shell
# yum -y install epel-release
# yum -y install ansible
# ansible --version
```

## Ansibleがインストールできない場合
* epel-releaseのバージョンが7.8であることを確認する（updateする）
```sh
$ rpm -ivh http://ftp.riken.jp/Linux/fedora/epel/7/x86_64/e/epel-release-7-8.noarch.rpm
```

* 外部ネットワークにつながらないサーバの場合（例：DBサーバ）
ADMINサーバでインストールするためのファイルを用意し次に下記を実行
```sh
$ scp epel-release-7-8.noarch.rpm 対象サーバー:
  ```

* 上記でもインストールできない場合

    ```
    "/etc/yum.repos.d/epel.repo"の"[epel]"で"enabled=0"になっているので”enabled=1”に変更すればepelが使えそうです。
    もしくはyumのインストールでenablerepoを追加すればよいでしょう。詳細は下記を見てください。
    http://qiita.com/muniere/items/6c4923a070cbbd824f39
    ```

## pipを利用したインストール
```Shell
sudo yum install -y epel-release
sudo yum install -y gcc python-pip python-devel openssl-devel libffi-devel
sudo pip install --upgrade pip setuptools
sudo pip install ansible==2.2.0.0
```

# 直接コマンドを実行する時
* Adhocを利用
http://docs.ansible.com/ansible/intro_adhoc.html

# Ansible.cfgカスタマイジング
ansible.cfgの修正(普通は/etc/aisibleフォルダ直下にある)
```
executable = /bin/bash -l
host_key_checking = False
```

# SSH通信

### Keyの配置
下記のA,Bの中で一つを選んで実施する。
> A.keyをAnsibleを実行する別サーバーで生成する場合

* keyの生成およびコピ

    ```Javascript
    $ ssh-keygen -t rsa
    $ ssh-copy-id ID@対象サーバ(ex:ssh-copy-id s5@xxx.xxx.xxx.xx)
    ```

> B.対象サーバーで生成されたkeyを使用する場合

* Puttygenを利用
http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html

    ```
    1.Puttygenを実行する
    2.Conversions -> import keyを選択し、もらったkeyファイル(ex:id_rsaまたは〇〇.ppkなど)を選択
    3.passphraseを入力(はるやまSTの場合OSユーザs5のpassword)
    4.keyがロードされる
    5.Conversions -> Export Open SSH keyでexportする
    6.Ansibleを実行するサーバーにexportしたkeyを配置する
    7.keyの権限を600に変更(ex:chmod 600 key名)
    ```

### 下記を実行する
1.ssh-agentの実行

```Javascript
$ ssh-agent bash
$ ssh-add keyの場所(ex:ssh-add ~/.ssh/id_rsa)
```

2.Ansibleのhostsファイルに↓を追加

```Javascript
[all:vars]
private_key_file=keyの場所(ex:/root/.ssh/id_rsa)
ansible_connection=ssh
ansible_ssh_user=対象サーバーのユーザ名
ansible_ssh_pass=対象サーバーのパスワード
```

### ping確認
hostsファイルがある場所で`ansible 接続名(hostsファイルに書いてある) -m ping -i hosts`
```Javascript
ex)
$ ansible s5-admin -m ping -i hosts
192.168.1.59 | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
```

# その他
## sudo pipが認識されない場合
```Shell
sudo ln -s /usr/local/bin/pip /usr/bin/pip
```

## Ansible Directory Layout
http://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html#directory-layout
```
production # 상용서버를 위한 인벤토리 파일 
staging # 스테이징 서버를 위한 인벤토리 파일

group_vars/
group1 # 인벤토리파일에 정의된 그룹을 위한 변수 저장
group2 # ""
host_vars/
hostname1 # 인벤토리파일에 정의된 호스트용 변수 저장 hostname2 # ""

library/ # 별도 모듈을 만들었다면 이곳에 저장 (optional)
module_utils/ # 별도 모듈의 module_utils 저장소
filter_plugins/ # 별도 필터플러그인 저장소

site.yml # 메인 플레이북 파일
webservers.yml # webserver 용 플레이북
dbservers.yml # dbserver 용 플레이북

roles/
common/ # 롤 이름, 여기서는 common
tasks/ #
main.yml # tasks 작업은 이곳에 작성
handlers/ #
main.yml # 핸들러는 이 곳에 작성
templates/ # 템플릿파일 모아두는 저장소
ntp.conf.j2 # <------- .j2 로 끝나는 템플릿들
files/ # copy, script 등 모듈에서 사용하는 파일 저장소
bar.txt # <-- 파일 예제
foo.sh # <-- 파일예제
vars/ #
main.yml # <-- 이 롤에서 사용하는 변수 작성
defaults/ #
main.yml # <-- 이 롤에서 사용하 변수(낮은 우선순위)
meta/ #
main.yml # <-- 의존성있는 롤 지정
library/ # 이 롤에서 사용하는 별도로 작성한 모듈 저장
module_utils/ # 별도 모듈용 module_utils 저장
lookup_plugins/ # 플로그인 저장소 예제

webtier/ # 롤 이름, 여기서는 webtier
monitoring/ # 롤 이름, 여기서는 monitoring
fooapp/ # fooapp, 여기서는 fooapp
```

## ansible reboot and wait
https://gist.github.com/infernix/a968f23c4f4e1d6723e4

```
---
- name: Reboot a host and wait for it to return
  hosts: somehost
  remote_user: root
  tasks:
    # Send the reboot command
    - shell: shutdown -r now

    # This pause is mandatory, otherwise the existing control connection gets reused!
    - pause: seconds=30

    # Now we will run a local 'ansible -m ping' on this host until it returns.
    # This works with the existing ansible hosts inventory and so any custom ansible_ssh_hosts definitions are being used
    - local_action: shell ansible -u {{ ansible_user_id }} -m ping {{ inventory_hostname }}
      register: result
      until: result.rc == 0
      retries: 30
      delay: 10

    # And finally, execute 'uptime' when the host is back.
    - shell: uptime
```