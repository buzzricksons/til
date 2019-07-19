JJUG CCC 2019 Spring 2019.5.18

# 開発リーダー1年目。メンバーのスキルアップのためにやっていること
## 輪読会
* 1.[リーダブルコード](https://www.amazon.co.jp/リーダブルコード-―より良いコードを書くためのシンプルで実践的なテクニック-Theory-practice-Boswell/dp/4873115655/ref=sr_1_1?__mk_ja_JP=カタカナ&keywords=リーダブルコード&qid=1563417665&s=gateway&sr=8-1)
* 2.[レガシーソフトウェア改善ガイド](https://www.amazon.co.jp/レガシーソフトウェア改善ガイド-Object-Oriented-Selection-クリス・バーチャル/dp/4798145149/ref=sr_1_1?__mk_ja_JP=カタカナ&keywords=レガシーソフトウェア改善ガイド&qid=1563417691&s=gateway&sr=8-1)
* 週に一回行う
* 二冊平行していく
## ランチ会
* 開発に関する話はしない

## 夕会&雑談
## チームの外へ
* 毎週LT大会開催
* 他のチームにも輪読会を提案
## マネージャーになると
マネジメントキャリアパスの本

# ランチセッション
* [Eclipse che](https://www.eclipse.org/che/)
    * ソースコードの共有・レビュー・確認をURLで
    * 開発からdeployまで一元化

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































