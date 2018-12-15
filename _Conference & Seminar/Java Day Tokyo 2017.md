
![](https://lh3.google.com/u/1/d/0B2Yxg0Epe-6_N3pfejlUZG45d2M=w1920-h950-iv1)
Java Day Tokyo 2017
2017.05.17.水
https://twitter.com/javadaytokyo
http://www.oracle.co.jp/events/javaday/2017/

# 基調講演

## ２番目の発表
- Javaがdockerと一緒に使えることになる
- Java 9
    - 122 new feature
    - Module System
    - jShell
    - Encapsulate Internal APIs
    - security強化
    - Ahead of Time Compilation(AOT)
    
### Beyond Java 9
http://openjdk.java.net
- Project Valhalla
    - Value Types
    - Specialized Generics
    - Var Handles
- Project Panama
    - Foreign Function Interface
    - Date Layout Control
    - Arrays 2.0

## 3番目の発表
Mazda自動車がJava使っている理由
- 長い期間安定的に使える言語のため
- 下位交換性が良い

### Strategy Patternから関数形プログラミングに変えていく

## 4番目の発表
- jShell

## 5番目の発表
- サイクルのデータ処理にJavaを利用
    - データを集計し、クラウド環境に転送して分析。

## 6番目の発表
- Java EE 8

# Java 9 and Beyond
- Modules will define a module - info.java file
- security強化
- jlink(ツール)
- Ahead of Time Java Compiler
    - static
    - dynamic
- jShell
- G1 GCがデフォルトGarbage Collectorへ

## Java SE Advanced
- flight recorder
- advanced management console

# Modular Development with JDK 9
## Programming in The Large
- 今まではパッケージが異なる場合、他のパッケージのクラスを使うためにはpublicにするしかなかった。
    - Java 9のモジュール化によってpublicの中でもっとscopeを設定することが可能になった。( public no longer means accessible to everyone)
- モジュールの再利用によってもっと効率的に活用が可能になる。

## Migrating To Modules
- jdeps
- Automatic modules
    - ex: opens com.myapp.domain to jackson.databind;

## The Modular JDK
- 既存のアプリケーションへの導入は慎重にする必要がある。
- rt.jarがなくなる。現在rt.jarを使っているのかを確認する必要がある。

# Servlet 4.0で始めるHTTP/2
## Servlet振り返り
Servletとは
- サーバサイドで動作するJava
- Controllerとしての役割

## Servlet 4.0概要
- Server Push
    - `PushBuilder pushBuilder = request.newPushBuilder();`

## Servlet 4.0 Server Push API
- RFC7540:予約リクエストは`キャッシュ可能`かつ`安全`なメソッドで定義

## Server Push 利用時のネットワーク状況

## Server Push ユースケース

# Java EE開発者のための、今から取り組むMicroservices開発
- war -> 実行可能なjarへの変更
- ログは外のシステムに写して分析

# Spring Framework 5.0によるReactive Web Application
## sync, blocking, async, non-blocking
- Async & Non-Blocking
- Tomcat NIO connector
- Non-blocking and event-loop(Netty)
    - appleで使っている。一秒あたり3テラ？ペタ？バイトを処理する。65万台のサーバーで動いている。
- 数少ないスレッドで大量の処理をする。
- マイクロサービスは多いサーバーと大量のデータ処理が必要ため既存のブロッキング処理では耐えられない。
- 多いクライアントから数少ないサーバーに接続される時、対応しやすい。
- scalabilityとstabilityを上げることを目指してSpringに導入された。
- Flux
- Mono

## Spring 5.0
- WebFlux
- WebClient
- Router Functions
- 現在のJDBCはブロッキングのためリアクティブプログラミングができない。(JDK 10でノンブロッキングをサポートする可能性あり。)
    - Spring apiではJDBCをノンブロッキングのように使えるメソッドが存在する。