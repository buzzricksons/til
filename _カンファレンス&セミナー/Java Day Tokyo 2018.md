# はじめに
- ホームページ：http://www.oracle.co.jp/events/javaday/2018/?source=JPMK171120P00102-OW:O:H:-
- 資料：http://www.oracle.com/technetwork/jp/ondemand/online2018-javaday-4489556-ja.html

## Container Nativeアプリケーション開発とアーキテクチャの勘所
http://otndnld.oracle.co.jp/ondemand/javaday2018/TEC-2

- Kubernetesの導入＝ Microservicesの実現ではない
- 「Designing Distributed Systems」
    - https://azure.microsoft.com/mediahandler/files/resourcefiles/baf44271-3870-454f-868c-23d48e7672cb/Designing_Distributed_Systems.pdf
- Containerのベストプラクティスを適用して、Cloud NativeなOSSの効果を最大化すべし
- ContainerとPodの考え方、Containerベースのデザインパターン設計のヒントになる
- Containerベースで考える場合のCI/CD
    - Microservicesにおける開発プロセスの課題
        - 複数サービスをく合わせたテスト
        - 継続的インテグレーション/デリバリー
        - 様々なデプロイ方法への対応
    - Containerベースの開発の場合の追加要件
        - 成果物をContainerとして作成
        - Containerベースの実行環境(=Kubernetes)へのデプロイ
        - ローカルで動作確認もContainerでできればなお良い

## Running Java applications on Docker: practical tips and valuable insights
http://otndnld.oracle.co.jp/ondemand/javaday2018/TEC-3





## Java in Serverless Land
http://otndnld.oracle.co.jp/ondemand/javaday2018/TEC-4

- http://fnproject.io/
    - an Open Source FaaS platform
    - Fully open (Apache 2.0) with commercial backing from Oracle
    - Run anywhere - Datacenter/labtop/rPi
    - Functions are containers
    - Fn Java


## Performance tuning with poor tools and cheap drink
http://otndnld.oracle.co.jp/ondemand/javaday2018/JSE-7



