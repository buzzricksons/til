# Annotation
| アノテーション | 説明 |
|:-------------|:-------------|
| @Controller |	MVCパターンのCの役割を担うコンポーネント。このアノテーションを付与したコンポーネントでは、クライアントからのリクエスト／レスポンスに関わる処理をする。 |
| @Service | ビジネスロジックを実装するコンポーネントであることを表すアノテーション。 |
| @Repository |	データの永続化に関わる処理を提供するコンポーネント。ORMなどを利用して、データのCRUD処理を実装する。 |
| @Component | 上記3つに当てはまらないコンポーネント。ユーティリティクラスなどに付与する。 |
| @Configuration | クラス宣言の前に記述します。このアノテーションは、このクラスがBeanの設定を行うものであることを示します。Bean設定クラスには常にこれをつけます。 |
| @RestController | JSONやXML等を返すWebAPI用のコントローラに付与する。 |
| @ControllerAdvice | Controllerを横断して例外をハンドリングする場合、例外ハンドリング用のクラスにこのアノテーションを付与する。ExceptionHandler系のクラスに使用。 |
| @ManagedBean | 本来はJSFが管理してるManagedBeanを表すもの。Springの@Componentを付けた時と同じ意味になると思われる。 |
| @Named | 本来はJava(EE)系でのインジェクション対象を表すもの。Springの@Componentを付けた時と同じ意味になると思われる。 |


# Live Reload
### 1.mvn import
```Text
<dependency>
    <groupid>org.springframework.boot</groupid>
    <artifactid>spring-boot-devtools</artifactid>
</dependency>
```
### 2.ChromeにLiveReloadをインストールし、有効にする
https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei

### 3.IntelliJの設定修正
1. Open the Settings --> Build-Execution-Deployment --> Compiler and enable the Make Project Automatically.
2. Then press ctrl+shift+A and search for the registry. In the registry, make the following configuration enabled.
3. Restart the IDE.


# その他
### cookie
アノテーションを利用して特定のcookieを取得する
```Java
    @RequestMapping(value="cookie", method=RequestMethod.GET)
    public String cookie(@CookieValue(value="foo", defaultValue="none") String foo, @CookieValue(value="bar", defaultValue="0") int bar) {
        System.out.println("foo cookie: " + foo);
        System.out.println("bar cookie: " + bar);
        
        return "redirect:/";
    }
```
