JJUG CCC 2019 Spring 2019.5.18

# 開発リーダー1年目。メンバーのスキルアップのためにやっていること
## 輪読会
* 1.リーダブルコード
* 2.レガシーソフトウェア改善ガイド
* 週に一回行う
* 二冊平行していく
## ランチ会
## 夕会&雑談
## チームの外へ
* 毎週LT大会開催
* 他のチームにも輪読会を提案
## マネージャーになると
マネジメントキャリアパスの本

# ランチセッション
* Eclipse che

# Hadoop 13:30セッション
* `_`は使わない方がいい。従来にjdkで使われる可能性がある

# SI大規模 IBM
## テスト
* ITAのテストはCI上で正常系のみ実施する
* テスト自動生成
* テストコードとテストデータの分離
## テスト環境
* mvn compile -> mvn test → mvn clean package, skpitestをtrueした状態でbuild
## まとめ
* Port Bindingが大変 → ochestration tool導入で解決できる
* コンテナおよびサービス起動が確認できない→ochestration toolを導入すれば確認できるはず

# Line発表
* ScalaはAkkaを使うため
* Spring WebFluxを使ってstreaming apiを実現(relatime性が必要のため)

# Functional Spring Cookbook
* Functional style -> Simple
* Simple is not easy
* WebFluxとの違いはTomcatなのかNettyなのか































