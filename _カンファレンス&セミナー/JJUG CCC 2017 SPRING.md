
# 資料
http://d.hatena.ne.jp/chiheisen/20170520/1495278028

# JHipsterで学ぶ！Springによるサーバサイド開発手法
## JHipsterとは
- 기본적으로 인증이 준비되어있음.
	- 구글, 페북, 트위터
- 여러가지 언어 서포트
- 어플리케이션 관리 기능이 준비되어있음.
	- jvm상태
	- 어플리케이션 실행시간등등
	- 헬스체크
	- 엘라스틱서치랑 연동해서 로그 검색가능
	- 스프링 설정
	- 시스템 환경관리등
	- api탭에는 Swagger도 들어있음
	- 데이터베이스 내용도 웹상에서 확인 가능.

## Getting Start
- vagrant, docker로 인스톨 가능
	- 노드.js인스톨할 필요가 있음.
- 최초에 monolithic or micro service선택 가능
- 엔티티 생성가능
- jdl-studio 브라우저 베이스의 gui툴도 이용가능

## Learn with JHipster
- 어플리케이션 구성
	- 웹, 서비스, 도메인, 리포지토리, 세큐리티
- 로그출력
	- spinrg-boot-starter-logging에 의존
- 개발할때만 유효하게 설정하는게 가능
- 로그내용을 비동기로 logstash에 연동가능
- 인증:http, OAuth2, jwt
- 세큐리티: 스프링부트보다 간단하게 가능
- 페이징정보는  http header에 추가됨
	- RFC 5988(Link Header)
- Rest에러 처리 
	- @ControllerAdvice
- 효율적 개발
	- Spring Bood Devtools랑 연동.
- Spring Boot Actuator

# Vue.js+Spring Bootで楽しくフルスタック開発やってみた
## knockout
	- 데이터 바인딩이 가능.
	- 자바스크립틔 오브젝트를 변경하면 html에 반영됨.
	- Cordova:html로 작성 가능
	- Vanilla js

## VueでSPA
- vue-router2: 루팅
- Vuex:페이스북의 Flux를 구현
- axios:HTTP클라이언트
	- promiseが返される

```
Vue를 써서 좋았던점
학습코스트가 적다.
양방향 바인딩
애니메이션 css transition
```
- npmとwebpackの導入
	- maven이나 grandle같은 녀석
	- 추가할때는 커멘드 실행
- webpack
	- 여러가지 파일을 하나의 파일로 축약 -> build.js
	- entry, ouput, 축약(컴파일)할때의 룰 설정 가능
	- webpack dev server
		- 코드변경을 감지해서 빌드
		- 브라우저를 자동 리로드(웹소켓이 사용됨)
	- 복수의 파일로 만드는것도 가능.(일부는 하나의 파일로. 일부는 복수의 파일을 하나의 파일로등등)
- vue-cli
- 크롬확장기능
	- 바인드된 값
	- 버츄얼 돔의 상태
	- vue의 상태, 실행된 mutation

## 스프링부트와 같이 빌드
- Gradle빌드중에 같이 실행되도록 설정.

## 프레임워크/라이브러리
- Spring Boot, devtools
- Spring MVC(or JAX-RS)
- Doma(데이터베이스 엑세스.)
- Vue(+ vue-router 2, Vuex), axios
- Gradle
- npm, webpack
- Selenide

## 그외
- 이뮤터블
- 발류오브젝트
- 클래스설계 참고 패턴
	- Observer
	- Iterator
	- Visitor
- 그외
	- EsLint
	- AVA
	- TypeScript or Flow
	- yarn
	- CSS Grid layout
	- Hotreloading
		- spring-boott-devtoolsとwebpakc dev tool이용

# データ履歴管理のための点ポラルデータモデルとReladomoの紹介
RDBMSで変更履歴をどう扱うか
## Model
### スナップショットデータモデル
- 最新の情報のみ
- update_dm

### トランザクション期間データモデル
- IN(유효)/OUT(무효)
- select * from employee where IN < ?  and OUT > ?

### 有効時間データモデル
- FROM/THRU
- IN의 정보는 알수없음

### バイテンポラルデータモデル
- FROM/THRU/IN/OUT전부사용

## Reladomo
-골드만 삭스가 깃허브에 공개한 프레임워크.
-generationギャプpattern
- Finder DSL
- Reladomo Kata GitHub
- Guided Tour of Reledomo
- Join: 엔티티에 릴레이션십 정의 가능
- 인덱스는 thru/out에 붙이면 유용

# What you need to know about HotSpot and Your Code
## What is good code
- Does what it's suppose to do
- Is easy for Humans to read
- Translates well into the execution environment

## Jit compilers
- C1 - client
- C2 - server - optimizing compiler
- Tiered - combination of C1 and C2
 
## Monitoring hotspot
- -XX:+PrintCompilation
- -XX:+LogCompilation
	- requires -XX:+UnlockDiagnosticVMOptions
	- log is best viewed using JITWatch
	- -XX:+TraceClassLoading
- jClairity

# Javaで実装して学ぶOAuith 2.0!
## OAuth 2.0とは？
- RFC 6749より
- 1.0とは別物
- 認証と認可の違い
- OAuth 2.0は認可
- Scope

## OAuth 2.0の登場人物
- Resouce Owner
	- 人間
- Resource Server
	- ex:トークンが保持されているサーバー
- Client
	- アプリ
- Authorization Server
	- アクセストークンをクライアントに発行するサーバー

## OAuth 2.0認可の流れ
- 重要な3つのエンドポイント
	- 認可エンドポイント
	- トークンエンドポイント
	- リダイレクトエンドポイント
- 認証が必要な場所もいくつかある
- アクセストークン(JSON形式)が発行されたら再認証はしない
- 暗号化は必須

## サンプル
- Apache OLTU(ドキュメントが少ないなどいろいろあり、本番に使うには難しいかも？)
- OpenID Connect
- JWT
- Spring Security OAuth
	- Spring Security 5にOAuth 2.0が入る予定
- pac4j

CASAREAL

## その他のセキュリティに関する事項
- RFC 6819
- RFC 7009

# Java8プログラミングベストプラクティス&きしだが動いているかどうかIDEメモリ使用状況から義機学習で判定する
## Netbeansからメモリログ
- JMX -> InfluxDB -> Grafana
- Thread count
	- NetrBeansが使っているThread数

## Java8コーディング
- Optionalは戻り値のみ使うのがいい
- 引数・filedにOptionalを使わない
	- Optionalはserializeができないため
- orElseThorwにException::newを書かない
	- 直接原因を書くほうがいい
- finalを使いたい場合は配列を使うほうがいい