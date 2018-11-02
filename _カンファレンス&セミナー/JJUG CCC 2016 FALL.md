
# Be a great engineer!〜 フォローすべきトレンド、スルーすべきトレンドをどう見抜くのか

# SIerもはじめる、わたしたちのDevOps

# 日本でも出来る！最先端のDevOpsを導入する方法

# Spring CloudでDDD的なマイクロサービスを作ってみる

# JVMのトラブル解決のためにやったこと~メモリー/スレッド

# Selenideを試行錯誤しながら実践するブラウザ自動テスト

- Web driverの設定をSelenideのconfigファイルで設定するため、Javaソースに設定を書く必要がなくなる。
- その他にものいろいろな設定ができる。
- テストケースの量が少なくなる。
- jQueryのような書き方。
- テストケースが失敗すると自動でキャプチャと失敗したhtmlが生成される。(保存する場所はconfigファイルで設定)
- headlessでテストしたい場合
- Remote Web Driver + Docker ←つまり現行のS5 Docker環境でも使える。
- Selenium server(Jenkinsまたは別のslaveサーバー) + Xvfb(仮想ディスプレイ)