# proxy機能を利用する(with Tomcat)
1.Tomcat起動
ローカルにローカルにtomcatが用意されていない場合は、下記を利用。 ここでは、ajpポートを3009とする
```Text
command docker run --rm --name tomcat -p 3080:8080 -p 3009:8009 tomcat
```

2.httpd.conf修正
```Text
LoadModule proxy_module modules/mod_proxy.so
LoadModule proxy_ajp_module modules/mod_proxy_ajp.so
Include conf/extra/httpd-proxy.conf
```

3.extra/httpd-proxy.conf作成
```Text
ProxyPass        /           ajp://192.168.0.1:3009/
ProxyPassReverse /           ajp://192.168.0.1:3009/
```

# アクセスするURLを別のURLにRedirectする
1.httpd.confにて、rewriteモジュールを有効にする
```Text
LoadModule rewrite_module modules/mod_rewrite.so
```

2.httpd.confにて、RewriteEngine Onにする
```Text
RewriteEngine On
```

3.ルールを作成(例)
```Text
RewriteRule ^/dummy/?$ /display/dummy/ [R=permanent,L]
```

4.ログを確認をしたい場合は、ログを有効にする
```Text
# ※数値が大きいほど詳しく出る
LogLevel debug rewrite:trace8
```

5.apache再起動し、動作確認
6.ログが不要なら、コメントアウトして再起動
出力例
```
[Sat Jan 28 16:23:57.618556 2017] [rewrite:trace2] [pid 7:tid 140023525508864] mod_rewrite.c(477): [client 192.168.0.1:39396] 172.17.0.1 - - [yoda.jp/sid#7f59d54fff28][rid#7f59d53e20a0/initial] init rewrite engine with requested uri /ap/pw.html
[Sat Jan 28 16:23:57.618716 2017] [rewrite:trace3] [pid 7:tid 140023525508864] mod_rewrite.c(477): [client 192.168.0.1:39396] 172.17.0.1 - - [yoda.jp/sid#7f59d54fff28][rid#7f59d53e20a0/initial] applying pattern '^.*$' to uri '/ap/pw.html'
[Sat Jan 28 16:23:57.618746 2017] [rewrite:trace4] [pid 7:tid 140023525508864] mod_rewrite.c(477): [client 192.168.0.1:39396] 172.17.0.1 - - [yoda.jp/sid#7f59d54fff28][rid#7f59d53e20a0/initial] RewriteCond: input='/ap/pw.html' pattern='^/ap/pw.html?md=u55$' => not-matched
[Sat Jan 28 16:23:57.618766 2017] [rewrite:trace1] [pid 7:tid 140023525508864] mod_rewrite.c(477): [client 192.168.0.1:39396] 172.17.0.1 - - [yoda.jp/sid#7f59d54fff28][rid#7f59d53e20a0/initial] pass through /ap/pw.html
```

## RewriteRuleのURLをエンコーディングしない
```Text
RewriteRule ^/foo http://example.com/?q=%26 [R,L]

↓

RewriteRule ^/foo http://example.com/?q=\%26 [R,L,NE]
```

# Virtual hostでホストごとに異なるルールを設定する
1.httpd.confにて、Virtual hosts設定をincludeする
```Text
Include conf/extra/example1.conf
```

2.host1の設定を作成
- ファイル名はconf/extra/host1.example.rewrite.confとする
- ルールは必要に応じて作成

3.host2の設定を作成 
- ファイル名はconf/extra/host2.example.rewrite.confとする
- ルールは必要に応じて作成

4.extra/httpd-vhosts.confにて、RewriteOptions Inherit, Include ファイル名を指定
```
<VirtualHost *:80>
 RewriteOptions Inherit
 Include conf/extra/host1.example.rewrite.conf
 ServerName host1.example.com
# 他の設定
 </VirtualHost>
 <VirtualHost *:80>
 RewriteOptions Inherit
 Include conf/extra/host2.example.rewrite.conf
 ServerName host2.example.com
# 他の設定
</VirtualHost>
```
5.apache再起動

# LB関連設定
1.設定箇所はどこでも構いませんが、VirtualHost, Location, Directory等の中は避けてください。 ここでは、httpd.confの最後に下記を追加するとします
- 1号機Apacheのhttpd.conf
```Text
Header add Set-Cookie "sn=01; Path=/"
```

- 2号機Apacheのhttpd.conf
```Text
Header add Set-Cookie "sn=02; Path=/"
```
※LB側の設定は別途必要です

# server-statusを利用する
mod_statusモジュールを有効にして、request数などをモニタリングできるようにする。 （性能試験実施時に、zabixでモニタリングするURLでもある）
- httpd-info.conf
```Text
Require ip 219.118.163.49
```

- httpd.conf
```Text
Include conf/extra/httpd-info.conf
```

- httpd-proxy.conf
```Text
ProxyPass        /server-status !
```

# KeepAlive
https://sites.google.com/site/hcgoon/puroguramingu-jiao-shi/apache/keepalive

# アクセスが多くなる場合の臨時対応
### リアルタイムで接続数の把握
```Text
 watch 'netstat -an | grep EST | wc -l'
```

### Web同時接続リスト
```Text
netstat -nap | grep :80 | grep ESTABLISHED | wc -l
```

### その他
- httpd.confファイルの修正

```Text
KeepAlive Off
Timeout 8~10
```
