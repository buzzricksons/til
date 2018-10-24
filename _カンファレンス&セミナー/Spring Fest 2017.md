Spring Fest 2017@両国, 2017.11.24 KFC Hall

# 資料
http://typewriter.hatenablog.jp/entry/2017/11/25/101306

# What's New in Spring?
- 스프링 웹플럭스로 만들면 디폴트가 네티로 만들어짐
- 리턴값을 Mono로 바꿔도 기존의 소스결과는 동일
- Reactive Spring
    - More for scalability and stability than for speed

# Introduction to Spring WebFlux
https://blog.ik.am
- Tomcat는 1리퀘스트당 1쓰레드. 디폴트는 200쓰레드
- Servlet Stack -> Reactive Staack
- The goal of Spring WebFlux is to offer Spring developers a non-blocking event-loop style programming model similar to node.js
-zip: 스트림처리를 순서에 의해 실행할 필요가 있을때 사용
- flatMap: 스트림 데이터를 핸들링 해서 새로운 데이터를 만들때 사용
    - ※map메소드랑 혼동되지 않도록 주의
- WebFlux를 도입해도 기존의 소스를 수정할 필요는 없음.(기존 그대로 움직임.) 
- Accept헤더를 이용.(Content Negotiation)
    - Accept: text/event-stream등 3가지. BackPressure를 사용할 수 있는건 2가지
    - curl -v -H "Accept: application/stream+json" localhost:8080
- Reactive Web Client
- Schedulers.elastic()
- Thymeleaf 3.0 reactive support
    - full mode
    - chunked mode
     - data-driven mode: 데이터가 준비된것부터 웹페이지 순차적으로 렌더링

# Wagby R8とSpringの関係

# SpringとData RESTを利用したAPIの設計と、作り直しまでの道のり
- lombok클래스:@Getter, @Setter, @Entity
- Controller라든지 restmapper등이 필요 없음.자동으로 뒷쪽에서 구현됨
- Spring Data REST
    - Entity랑 Repository두개를 구현하면 Endpoint가 생성됨.
    - post/get/put/patch/delete가 전부 생성됨
    - request/response포맷을 통일된 HATEOAS로 만들어줌.
    - 전부 톱레벨의 엔드포인트가 되어버림.(단계구조로 만들어지지 않음.)
    	- 커스텀 엔드포인트를 만드는걸로 대응가능.

# ドメイン駆動設計のためのSpringの上手な使い方
- 도메인주도설계의 기본활동
    - 개발자가 도메인을 학습
	- 계속적인 학습
	- 학습한것으르 코드로 표현
    - 모델이랑 구현을 일치시키기
	- isolating-the-domain
	- Spring의 프로그래밍 모델: focus on your specific domain model implement with plain Objects
    - 심도있는 모델을 탐구
	- if문 보다는 폴리시를 작성
    - 거대하고 복잡함에 맞서기
- Spring Boot
- Spring Integration
- Spring Batch
- Spring Security
- どんな状況でも改善はできる
- どんたときでも「あなた」から改善をはじめられる
- どんたときでも「今日」から改善をはじめられる

# 2017年のLINEのマイクロサービスを支えるSpring

# The Road to Serverless: Spring Cloud Function
- Functions->Apps->Containers->Virtual Machines
- FaaS -> PaaS -> CaaS -> IaaS
- Event driven
- Dynamic resource utilization
- 메세지 단위의 과금 Billing per message
- 프로토타입으로 만든걸 혼방용으로 쓸때 빨리 전개가 가능.
- CNCF WG Whitepaper
- Service Block @kennybastani
- Get out of the business of infrastructure and automation(a.k.a "undifferentiated heavy lifting") and integration spaghetti
- Serverless Provider
    - aws lambda  자바서포트
    - google cloud function
    - Azure Function자바서포트
    - IBM openwhisk자바서포트
    - Oracle Fn자바서포트
    - Riff자바서포트
    - OpenFaas
    - Fisson
    - Kubernetess
- maven: spring-cloud-function-web
    - spring cloud version
    - reactor version
- Spring boot Thin Launcher

# Spring BootとSpring Cloudで始めるマイクロサービス
- Not everyone needs agility and scalability
- 守破離
- @RunWith(SpringRunner.class), @SpringBootTest
- Spring Cloud Eureka
    - pom에 dependency 추가
    - @EnalbeEurekaServer
- Spring AMQP or Spring cloud stream
- RabbitMQ -> Kafka로 변경하는데 소스변경은 필요없음





