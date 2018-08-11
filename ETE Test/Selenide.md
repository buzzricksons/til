# import
### Maven
```
<!-- https://mvnrepository.com/artifact/com.codeborne/selenide -->
<dependency>
    <groupId>com.codeborne</groupId>
    <artifactId>selenide</artifactId>
    <version>4.8</version>
</dependency>
```

### Gradle
```
dependencies {
    testCompile('com.codeborne:selenide:4.11.1')
}
```

# Elementコントロール
### inputタグ
```Java
$("input[type=textarea]").setValue("Hello World!");
$("input[type=button]").click();
$("input[type=textarea]").getText();
```
# 一般
## Configuration
- browser
```Java
//Chromeの場合
System.setProperty("selenide.browser", "Chrome");
```

- Screenshot
```Java
//gitレポジトリ/test-result/reportsに保存される
System.setProperty("selenide.reportsFolder", "test-result/reports");
```

- Headless: Xvfbは不要になる
```Java
System.setProperty("selenide.headless", headless);
```
※mvn実行の場合`$ mvn test -Dchromeoptions.args=headless` または `$ mvn test -Dselenide.headless=true`

## 実行
```Shell
clean test -Dchromeoptions.args="--headless --disable-gpu"
```

### その他
#### Seleniumの場合headless
```
ChromeOptions chromeOptions = new ChromeOptions();
chromeOptions.addArguments("--headless");
WebDriver Driver = new ChromeDriver(chromeOptions);
```

### Basic authentification
```text
driver.get("http://username:password@www.domain.com");
```

## Browser
### vm optionの場合
```Shell
-Dbrowser=chrome
```

### Javaクラスに記述する場合
```Java
System.setProperty("selenide.browser", "Chrome");
```

## Error
### UrlCheckerエラー
```
java.lang.IllegalAccessError: tried to access method com.google.common.util.concurrent.SimpleTimeLimiter.<init>(Ljava/util/concurrent/ExecutorService;)V from class org.openqa.selenium.net.UrlChecker
```
のエラーが出る場合`pom.xml`に下記を追加する。
```Shell
        <dependency>
            <groupId>com.google.guava</groupId>
            <artifactId>guava</artifactId>
            <version>22.0</version>
        </dependency>
```

## Travis CIを利用する場合
- .travis.yml

```yml
language: java
jdk: oraclejdk8

sudo: false

addons:
  chrome: stable

env:
  - MAVEN_VERSION=3.3.9

dist: trusty
addons:
  chrome: stable

install:
  - "mvn -N io.takari:maven:wrapper -Dmaven=${MAVEN_VERSION}"
  - "./mvnw --show-version --errors --batch-mode test-compile dependency:go-offline"
script:
  - "./mvnw --show-version --errors --batch-mode -Prun-its clean verify -Dchromeoptions.args=headless"

cache:
    directories:
    - $HOME/.m2

notifications:
  slack: buzzricksons:5Ohg3Wubu3gbfa8l0zBumtrX
```

# Linux
下記のものをインストールする
- maven
- jdk 1.8以上