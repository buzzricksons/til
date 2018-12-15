2017 4.21@Shibuya, Tokyo

# 発表資料
https://lp.google-mkto.com/rs/248-TPC-286/images/google_cloud_onboard_japan.pdf?mkt_tok=eyJpIjoiT0RBek5qazFPVGxtT0RjMyIsInQiOiJFM252R013S2xDZ1FOenhITWJtZDN4WjVQSU55NXVISVkwblBXMjFKZ2N0c1RYdzZJXC94R0dLUHA2ckpPM3ptQ0RnRnRUT3dhODJBeTI2TllzdzNFK1NPNnJVNHpwY1NQZG9nVGh0VGpxQytaTk9xOSt2TTlGRitSeVBrNlRcLzBJIn0%3D

# いまなぜGCPを学ぶのか？
- グーグルが社内で使用していたインプラ環境をパブリッククラウド化
- 全世界のユーザーがターゲット
- 0から全部グーグルが設計。レイア構造

# Google Cloud Platformのご紹介
## GCPを選択する理由

- 安定性、信頼性、スケーラビリティ
- Region:複数のZoneが集まっている。Region内のリソースは同じリージョンであればどれでも利用可能。
Zone:リージョン内のデータセンターがある場所

### 課金

- 1時間未満の課金単位
- 長期利用割引：1ヶ月に25%を超えた使用した仮想マシンは自動で割引が適用される。
- 課金管理者というユーザーが存在

# プロジェクト
### プロジェクトパーミッション
- オーナー
- 管理者
- 閲覧者
- 課金管理者

### G suitsとの相性が良い
- gmailアカウントをそのままプロジェクトで使える。

# GCPの操作
## 3つの方法が存在
### Cloud Console - Web(GUI)
### Cloud SDK/Cloud Shell
- Dockerイメージとして利用可能
- Cloud Shell(Debian base)経由で利用可能

### REST-based API
- GCP Consoleから利用可能
- Java, GO,Python,JavaScript, PHP, .NET,Node.js, Ruby, Objective-C, Dartをサポート
- APIs Explorerというブラウザ(ウェブサイト)のようなツール存在(GUI)

## Client Libraries
- Google Cloud Client Libraries
	- コミュニティが所有する手作りのClient LIbraries
- Google APIs Client Libraries
	- オープンソース作成
	- 様々の言語をサポート

# Google App EngineとGoogle Cloud Datastore
## Google App Engine
- スケーラブルなウェブアプリケーションや、モバイルバックエンドを構築するためのプラットフォーム(PaaS)
- App Engineがデプロイやメンテナンス、スケーラビリディを実施し、開発者はアプリケーションの開発に集中することができる。

※Google Compute EngineはIaaS

### 例
#### Snapchat
- Google App Engineで動いている。毎日7億の写真やビデオを送信している。

### App Engine Standard Environment
- Java, Python, PHP, Goなどをサポート。(SDK存在)
- クリック1つでアプリの構築、デプロイ、コンテナ化
- 標準のランタイム(Python, Java, Go, Node.js)でサンドボックスの制限なし
-カスタムランタイムはHTTPリクエストをサポートする言語であればなんでもサポート
- `スケーラブル制限がある`
- ローカカルの開発はDockerに依存

#### Flxible Environment

## Google Cloud Datastore(NoSQL)
- アプリケーションバックエンド向けに設計されたデータベース
- 数十億行のNoSQLデータストア
- スケーマレスなアクセスで、データ構造を考える必要がない
- ローカルの開発ツール
- オートスケーリングで完全管理
- ACIDトランザクションをサポート
- 毎日無料枠あり
- 何処からでもRESTfulインタフェースを通してアクセス

# Google Cloud Platform Storageのオプション
bucket名は世界でユニーク(早くcommerce21という名前でbucketを作らないと。。。)

## Google Cloud Storage
- ファイルサーバのように感じ
- ファイルシステムではない。
- 管理が簡単、容量のマネジメントは不要。
	- アップロードした分課金
- 全てのストレージクラスは同一のAPIでアクセス可能
- 4つの種類が存在
	- Multi Regional
		- リージョンをまたがったユーザーに邸レイテンシで、高QPSのコンテンツを届けるのに理想的
	- Regional
		-1つのリージョン内
	- Nearline
		- 1ヶ月あたり1回未満に良い
	- Coldine
		-1年あたり1回未満に良い
- Objectパージョニング
- Object Lifecycle Management
- データのバックアップ
	- バックアップしたデータを分析することも可能

## Google Cloud Bigtable(NoSQL)
- key, valueストアーのサービス(NoSQL)
- HBase APIを使ってアクセス
- ビックデータ、Hadoopのエコシステムとネイティヴ互換
- G MailもBigtableで動いている

### インテグレーション
- Google Cloud Dateflow
- Google Cloud Dataproc
- クラウドをベースとしたオンプレミスのHadoop(外部サービス)

## Google Cloud SQL
- RDBサービス
	- MySQLとpostgreSQL(まだbeta)をサポート
	- 容量が足りない場合、自動でDiskの容量を増えることも可能

## Google Cloud Spanner(ベータ)
- 水平スケーリング可能なRDB
- 数千台規模でのスケールも可能
- マルチリージョン対応
- s最大で99.999%の可用生

# Google Container Engine
## Container Technology
- Dockerfile
	- コンテナイメージを自動作成する

## Docker Quick Tour

## From Borg to Kubernetes
- グーグル社内ではすべてのアプリがコンテナ上で動いている。
- App EngineはBorg上で動く

### DeploymentとServiceに夜マイグロサービス管理
deploymentとserivceに分けられている
- deployment:コンテナの準備
- service:ネットワーク設定

### Deployment
#### Blue Green Deployment
リリースするバージョンができあがたらLBによる切り替え。

#### Rolling Update
切り替えではなくリリースバージョンコンテナをどんどん植えていくながら既存のバージョンは減らしていく。(同時に行われる)

## Google Container Engine

# Google Compute Engine(IaaS)
## 概要
- Liveマイグレーション機能
	- ディスクのリサイズ、インスタンスのマイグレートをダウンタイムなしで
- 自動スケーリングとインスタンスグループマネジメントのための先進のAPI
- 分単位の課金、継続利用割引

## ネットワーキング
- HTTP(s)ロードバランシング
	- 複数のCompute EngineリージョンにまたがるHTTPベースのトラフィックをバランス
	- グローバルにはトラフィックを外部IPアドレス経由で配信
- TCP/SSLとUDP(ネットワーク)のロードバランシング

## Google Clolud CDN(Content Delivery Network)
- compute engineではHTTP(s)ロードバランシングを利用

## Google Stackdriver
- 総合モニタリング、ロギング、診断

## Firebase
- realtime DB機能
- モバイルバックエンド

# Big Data ソリューション
## GCPの特徴 = データ + No-Ops
- Data makes software great.Better software, faster.
- データを入れて、SQLを書いて、クエリーボタンを押すだけ

## BigQueryはとにかく素晴らしい！
### BigQueryとは
- GoogleのクラウドベースのDWH(データウェアハウス)
- 高速に大量データを処理可能(ペタバイト級)
- 邸コスト
- フルマネージドサービス(自動アップデートなど)
- 標準SQLをサポート
- Federated Query
- `select *`はanti pattern

#### BigQueryは万能ではない
- 非構造データ
- リアルタイム処理
- 複雑なプログラム

※BigQueryの苦手な部分を解決するのがCloud Dataflow

## Cloud Dataflowはデータ処理の新しいデファクト
### Cloud Dataflowとは
- ストリーム+バッチにてデータ処理
- オープン(Apache Beam)
- Java/PythonのSDK

### Cloud Dataprocとは
- Hadoop/Sparkのマネージドサービス
- 90秒以内にクラスタを起動
- 必要な時必要なだけ
	- 低コスト(分単位の課金)
- スケーラブル

### 事例
- Spotify
	- 音楽ストリーミング

## リファレンスアーキテクチャ

# Google Machine Learning
`Youtube 猫 機械学習`で検索

## 事例
### DeepMindのWaveNetによる音声合成技術
### Google Photo
### Gmail Smart Reply
- まだ日本語版には適用されていない
- メールを読んで自動で返事を作ってくれる。
	- モバイルアプリからの返信の10%

### ディープラーニングで冷却設備の動作を改善

## GCPが提供する機械学習サービス
### APIサービス
- Cloud Vision API
	- 画像分析
- Cloud Natural Language API
- Cloud Speech API
- Cloud Video Intelligence

### Cloud Maching Learning Engine
### Cloud Datalab
### TensorFlow

## 参考サイト
[機械学習であそぼう！](https://book.mynavi.jp/manatee/series/detail/id=65670)

# Google Cloud Next '17 Recap
- 音声認識
