
# 日本語
JJUG CCC 2017 Fall

## 資料
http://d.hatena.ne.jp/chiheisen/20171119/1511042292

## Selenide or Geb?
- JSTQB

### Selenide
- Javaで作られたSeleniumラッパー
- IDEとの親和性が良い(自動完成など)
- Ajaxの非同期処理に対する機能が良い
- Enterprise サポート開始
- ローカル環境での実行は問題ないがJenkinsでは失敗する場合がある。(安定化が大変かも)
    - 環境依存問題(ステージング環境とローカル環境のネットワーク速度差など)のせいでwaitがうまく動かない場合がある。
- 開発環境ではphantomjs(headless)を使うのが良いかも
    - Sauce labsを使えばクラウド環境でのマルチブラウザ対応が楽かも。。。
- JUnit5対応

### Geb
- ジェブと呼ぶ
- Groovyで作られたSeleniumラッパー
- DSLを利用したjQueryのようなセレクターを提供
- waitが使いやすい。
- 細かく画面要素のコントロールが可能
- IDEサポートが弱い
- Groovy,Gradleなど初心者には壁が高いかも
- Spockが使える

## APACHE CAMEL + HAWTIO + SPRING BOOTによるモダンなインテグレーションマイクロサービス
- Enterprise Integration Patterns
- Camel in action 2
- JCUG
    - Japan camel user group

### インテグレーションマイクロサービス
- Smart endpoints and dumb pipes

### Apache Camelとは
- 軽量化インテグレーションフレームワーク
    - camel-core.jarがわずか 4.8M
- 直感的なルーティングDSL
- Enterprise Integration Patterns
- 280個以上の接続コンポネントサポート(aws, azure, cassandra, facebookなど)
- マイクロサービスサポート(Cloud Ready)
    - Spring Boot/WildFly Swarm/Netflix Hystrix
- eclipse用のguiプラグインが存在する
- Camel test用サポートクラスが存在する

#### Camelでできること
1.HTTP/RESTで取得したリクエストをツイッターにリツイートする
- Java DSL言語で作成する
- RouteBuilderを継承してconfigure()メソッドをオーバーライドする
- ScalaのなどのALT JAVA言語も利用可能
- Spring xml DSLでも書ける

2.SOAPで取得したリクエストをKafkaに転送
3.Active MQにより取得したJMSメッセージ内容対応

### インテグレーションマイクロサービスの作り方
- CAMEL X SPRING BOOT
    - Camelコンポネントスターターをpom.xmlに追加する
    - @Componentを付けてCamelルートを定義

### hawitoによるモニタリング
- マイクロサービスを監視
    - jvmの監視はjmxを使うのが一般的
- webベースのjmx監視ツール(Angularjs 1.x + jolokia)
- spring boot用のdependencyが存在する
- Camelのサポートが充実(作業の流れがgui化されているなど)

## DDD x CQRS - 更新系と参照系で異なるORMを併用して上手くいった話
- CQRSを独自で利用可能
- Command Query Responsibility Segregation
- Greg Youg
- Read, Writeを分ける
    - dataモデルを分ける(既存にReadのモデルを追加するのが楽)
    	- 複数のORMマッパーを利用.(書きはHibernate, 読みはjOOQなど)
    - dataストアを分ける(例えば読みモデルはelastic searchなどを利用)
- jOOQ

## 劇的改善 CI 4時間から5分へ~私がやった10のこと~
- Google SET
- クラス単位のテスト
    - rdbに接続するのはレポジトリレベルのみ
- Not @SpringBootTest, but @WebMvcTest
- ServiceテストではDIは利用しない
- @MyBatisTest(1.3以上の場合)
- 要らないテストは削除する
- 時間がかかりすぎるテストは修正する
- Jenkins -> Oracle仕組みの既存CIをawsに移行(ec2->node->Amaon RDS(Schema))
    - テストの並列実行
- テストサイズの導入(Googleが提唱)
    - JUnitの@Category, maven-surefire-pluginのgroupsで実行する
	- mvn -P Small
	- mvn -P Medium
- プルリクエストフィードバック: Lint(lint-review), CodeCov, SonarQube, Dangerを利用

## DockerではじめるJava EEアプリケーション開発
- build、 deploy環境、dbを１つのdocker composeファイルで実行
- docker fileの作成
- docker compose.yml
- Swarm, kubertness

## 「書ける」から「できる」になれる！〜Javaメモリ節約ノウハウ話〜
- stw(Stop the world), oom(Out of Memory error)
- primitiveではなく基本形を使うのがメモリの使用率が低い
- BitSet
- Runtime.totalMemory(), Runtime.freeMemory()

## Spring BootとKafkaでCQRS
- https://cacoo.com/ja
- 実践DDD
- ドメインイベント
- イベントソーシング Event Sourcing(既存のStatus Sourcingより進歩した方法)
- CQRSはEvent Sourcingへ至る前の段階
- CQRS/Event Sourcingをすべてに適用はしない(効率面で考えたら時間・費用が高いのため)
- Kafka
    - 分散ストリーミングプラットフォーム

# 한국어
JJUG CCC 2017 Fall

## 資料
http://d.hatena.ne.jp/chiheisen/20171119/1511042292

## Selenide or Geb?
- JSTQB

### Selenide
- IDE에 의한 친화성(자동완성등)이 좋다.
- Ajax등의 비동기 처리에 대한 대응이 좋다.
- Enterprise Support개시
- 로컬과 달리 Jenkins 에서 실패하는 경우가 있음.(안정시키기가 좀 힘들수도...)
    - 환경의존 문제(스테이징 환경과 로컬환경의 네트워크 속도등)가 있어 wait가 제대로 작동안함
- 개발환경에서는 phantomjs(headless)를 이용
    - Sauce labs를 이용하면 클라우드 환경에서 멀티 브라우저 대응이 쉬울수도...
- JUnit5대응

### Geb
- Groovy로 만들어지 셀레늄랩퍼
- DSL을 이용한 jQuery느낌의 셀렉터를 제공.
- wait가 사용하기 쉽다.
- 좀 더 섬세하게 화면요소의 콘트롤이가능
- IDE서포트가 취약하다.
- Groovy,Gradle등 학습코스트가 높다.
- Spock를 사용할 수 잇다.

## APACHE CAMEL + HAWTIO + SPRING BOOTによるモダンなインテグレーションマイクロサービス
- Enterprise Integration Patterns
- Camel in action 2
- JCUG
    - Japan camel user group

### インテグレーションマイクロサービス
- Smart endpoints and dumb pipes

### Apache Camelとは
- 경량화 인테그레이션 프레임워크.
    - camel-core.jar 4.8M
- 직관적인 루팅DSL
- Enterprise Integration Patterns
- 280이상의 접속 컴포넌트지원(aws, azure, cassandra, facebook등)
- 마이크로 서비스 서포트(Cloud Ready)
	- Spring Boot/WildFly Swarm/Netflix Hystrix
- 이클립스용 gui플러그인이 존재
- Camel test용 서포트 클래스가 존재

#### Camel로 할수 있는것
1.HTTP/REST 로 취득한 리퀘스트를 트위터에 리트윗
- 자바 DSL언어로 작성
- RouteBuilder를 계승해서  configure()메소드를 오버라이드
- 스칼라등의 ALT JAVA언어에도 가능
- Spring xml DSL에도 기술가능

2.SOAP로 취득한 리퀘스트를 Kafka에 날림
3.Active MQ로 부터 취득한 JMS메세지내용 대응

### インテグレーションマイクロサービスの作り方
- CAMEL X SPRING BOOT
    - Camel컴포넌트 스타터를 pom.xml에 추가
    - @Component를 붙여서 Camel루트를 정의

### hawitoによるモニタリング
- 마이크로 서비스 감시.
    - jvm의 감시는 jmx가 일반적
- web베이스로 되있는 jmx감시툴(Angularjs 1.x + jolokia)
- spring boot용 dependency	가 존재
- Camel의 서포트가 충실(작업의 흐름이 그래픽화되있는 등)

## DDD x CQRS - 更新系と参照系で異なるORMを併用して上手くいった話
- CQRS는 단독으로도 이용가능
- Command Query Responsibility Segregation
- Greg Youg
- 읽기, 쓰기를 별도로 분리
    - data모델을 분리(읽기모델을 추가하는게 편함.)
    	- 복수의 ORM맵퍼사용.(쓰기는 하이버네이트, 읽기는  jOOQ등)
    - data스토어를 분리(예를 들어 읽기모델은 엘라스틱 서치 같은것을 이용)
- jOOQ

## 劇的改善 CI 4時間から5分へ~私がやった10のこと~
- 구글 SET
- 클래스 단위의 테스트로.
    - rdb에 접속하는 건 리포지토리 레벨만
- Not @SpringBootTest, but @WebMvcTest
- Service테스트에는 DI를 사용하지 않는다.
- @MyBatisTest(1.3이상일경우)
- 불필요한 테스트 삭제
- 시간이 많이 걸리는 테스트 수정
- 젠킨스->오라클 형태의 기존 CI를 aws에 이행.(ec2->node->Amaon RDS(Schema))
    - 테스트의 병렬실행
- 테스트 사이즈의 도입(구글이 제창)
    - JUnit의 @Category, maven-surefire-plugin의 groups로 실행
	- mvn -P Small
	- mvn -P Medium
- 풀리퀘스트 피드백: Lint(lint-review), CodeCov, SonarQube, Danger을 이용

## DockerではじめるJava EEアプリケーション開発
- 빌드,디플로이환경,디비를 하나의 도커 compose파일로 실행
- 도커파일 작성
- 도커컴포우즈.yml
- Swarm, kubertness

## 「書ける」から「できる」になれる！〜Javaメモリ節約ノウハウ話〜
- stw(Stop the world), oom(Out of Memory error)
- 프리미티브가 아니라 기본형을 사용하는 것이 메모리 사용량이 적다
- BitSet
- Runtime.totalMemory(), Runtime.freeMemory()

## Spring BootとKafkaでCQRS
- https://cacoo.com/ja
- 실전 도메인 주도설계책(일본어)
- 도메인 이벤트
- 이벤트소싱 Event Sourcing(기존의 스테터스 소싱보다 진보한 방법)
- CQRS는 Event Sourcing에 가는 전단계
- CQRS/Event Sourcing를 전체에 적용하지는 않는다.(효용면에서 시간/비용이 많이 걸리기때문)
- Kafka
    - 분산스트리밍 플랫폼