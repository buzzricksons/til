elastic on tour
2019年5月30日のTokyo Elastic {ON} ツアーイベント

# 基調講演
* Search is an experience applicable to many things.
* 検索はいろいろなものに適用可能
* kubernatisの状況もelastic searchで見ることができる
* APM
	* Java, .netなどのサポートが可能
* Uptime
	* クラスタ管理
	* ga化
* Elastic Enterprise Search(beta)
	* google drive, dropbox, githubなどのエンタプライズサービスの検索
* Map検索
	* ddosの攻撃経路の可視化など

# Elastic Stackの進化
* Elastic Stack
	* Beats
		* Elasticsearchへのデータ転送
	* Logstash 
		* Beatsより複雑な対応が必要な場合
* Weak-ANDアルゴリズム
	* 検索速度改善
* BKD Tree
	* BKD Geoshape
* Changes API
	* データのストリーム化
	* 自分が知りたいデータだけ検索したい要望に対して
* shirinkを利用してshadeの数を減らす
* 一元的なBetasの管理機能
	* Kibana上でBeatsの設定が可能
* Kibana Spaceで複数のプロジェクト表示が可能に


# ロギング、メトリック、APM：The Operations Trifecta
* Logging Modules
* Log File Import → 機械学習
* Metrics : 測定値



# Elastic Stackを使ったエンドツーエンドのセキュリティ分析
* Beatsはクライアントのため、サーバー全部インストールする必要あり
* LogStashはクライアントではないためサーバーにインストールする必要あり
* ECSはガイドラインのドキュメント
* データのエンリッチ
	* データの検索ではなく投入のタイミングで設定
* ebayは1秒で250万ログ


# Canvasで作成するリアルタイムなインフォグラフィック
* データの表示方をカスタマイジング



# アーキテクチャーのベストプラクティスと”落とし穴”
* クラスタが2 nodeはだめ。最小限3(Master)  nodeが必要
* 専用Nodesか？非専用Nodesか？
* Shardsは１つ当たり15~50GBのサイズが良い
* Shards数は20GB以下/1GB heap


# 機械学習ディープダイブ


# Elasticを利用したリコーグループのIT基盤の見える化


# 水環境の持続を支えるプラットフォーム Water Business Cloudにおける活用と今後展開



























