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

実行時間は、分、時、日、月、曜日を指定し、こちらも半角空白を空けて記録する。
時は24時間表記、曜日は0から6まで日曜日から土曜日までに対応し、さらに7はまた日曜に対応する。
数字の代わりに*を入力すると指定しないことになる。

## 例
### 1
毎月２０日の２３：５９に、シェルスクリプト/home/vagrant/work.shを実行させるには次の書式だ。

```shell
59 23 20 * * ./home/vagrant/work.sh
```

### 2
毎週金曜日の17:00に、シェルスクリプト/home/vagrant/weekly.shを実行させるには次の書式だ。

```shell
00 17 * * 5 ./home/vagrant/weekly.sh
```

### 3
/5と表記すると間隔５を表すことができる。

例えば、５分おきに、シェルスクリプト/home/vagrant/work.shを実行させるには次の書式だ。

```shell
*/5 * * * * ./home/vagrant/work.sh
```

### 4
毎日の１１時と２３時に、シェルスクリプト/home/vagrant/work.shを実行させるには次のように２行併記する。

```shell
0 11 * * * ./home/vagrant/work.sh
0 23 * * * ./home/vagrant/work.sh
```

### 5
今回は、毎日のお昼１２時に、シェルスクリプト/home/vagrant/pslog.shを実行させるため、次のような表記とする。

```shell
0 12 * * * ./home/vagrant/pslog.sh
```

保存し、コマンドプロンプトに戻るときにエラーチェックが行われ、正常であればinstalling new crontabとメッセージが表示される。