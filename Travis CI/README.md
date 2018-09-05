## はじめに
ファイル名は`.travis.yml`

## Gradle設定ファイル
```
language: java
jdk: oraclejdk8

before_install:
 - chmod +x gradlew

before_cache:
  - rm -f  $HOME/.gradle/caches/modules-2/modules-2.lock
  - rm -fr $HOME/.gradle/caches/*/plugin-resolution/

cache:
  directories:
    - $HOME/.gradle/caches/
    - $HOME/.gradle/wrapper/

notifications:  slack: Token
```
## Maven設定ファイル
```
language: java
jdk: oraclejdk8

sudo: false

env:
  - MAVEN_VERSION=3.3.9
install:
  - "mvn -N io.takari:maven:wrapper -Dmaven=${MAVEN_VERSION}"
  - "./mvnw --show-version --errors --batch-mode test-compile dependency:go-offline"
script: "./mvnw --show-version --errors --batch-mode -Prun-its clean verify"

cache:
    directories:
    - $HOME/.m2

notifications:  slack: Token
```

## Headless Chromeのbuild設定
https://sites.google.com/site/hcgoon/puroguramingu-jiao-shi/selenium/selenide#TOC-Travis-CI-