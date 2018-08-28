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
## cookie
アノテーションを利用して特定のcookieを取得する
```Java
    @RequestMapping(value="cookie", method=RequestMethod.GET)
    public String cookie(@CookieValue(value="foo", defaultValue="none") String foo, @CookieValue(value="bar", defaultValue="0") int bar) {
        System.out.println("foo cookie: " + foo);
        System.out.println("bar cookie: " + bar);
        
        return "redirect:/";
    }
```

## DAOとService
- 一般的なSpringの処理流れ：- URL call -> Controller -> Service -> ServiceImpl -> Dao -> DaoImpl -> Service -> View

```
MVC 패턴에서 Service Model 의 역할

MVC 패턴의 핵심은 View는 자신이 요청할 Controller만 알고있으면 되고, Controller는 화면에서 넘어오는 매개변수들을 이용해 Service 객체를 호출하는 역할을 한다. Service 는 불필요하게 Http 통신을 위한 HttpServlet을 상속 받을 필요도 없는 순수한 자바 객체로 구성된다(그렇기에 Service 에 request나 response와 같은 객체를 매개변수로 받아선 안된다. 그걸 사용해야하는 작업은 컨트롤러에서 해야한다.). 그렇기에 자신을 어떤 컨트롤러가 호출하든 상관없이 필요한 매개변수만 준다면 자신의 비즈니스로직을 처리하게된다. 즉 모듈화를 통해 어디서든 재사용이 가능한 클래스파일이라는 뜻이다. 단순 Web 기반이 아니라 추후 native app 으로 view단이 변경되더라도 Service는 view에 종속적인 코드가 없기때문에 그대로 재사용 할 수 있어야 한다. 그리고 추가적인 요청사항이 들어오면 기존 소스를 수정하는게 아니라 기존 service 인터페이스를 구현한 다른 클래스를 구현해 그 객체를 사용하게끔 하는것이다. OCP에 입각한 변화에는 닫혀있고 확장에는 열려있는 구조로 만들어야한다는 것이다.



결론

그렇기 때문에 Service를 인터페이스로 구성했던것이 아닐까 생각한다. 비즈니스 로직을 처리하는 모델은 요청사항에 따라 언제든 변할수있는 부분이었고 변화에 대응하기위해 확장을 염두하여 인터페이스로 구성했던것이다. 그런데 어디서부터 잘못된건지 Service를 인터페이스로 만들었던건 관례로 굳어지게 되었는데 개발은 transaction script 형식으로 진행하다보니 관례는 관례대로 남고 애초에 그렇게 하고자했던 이유는 사라져버리게 된것이다. 그래서 내가 내린 결론은 한 메서드에서 모든 역할을 다하는 이런 절차지향적 코딩에서는 사실 Service를 굳이 인터페이스로 할필요는 없다는 것이다. 물론 '그러니까 인터페이스 만들지말자' 보다는 애초에 인터페이스를 만들었던 이유를 잘 살리는게 바람직하지 않을까 생각하고, 나같은 궁금증을 가졌던 사람들에게 조금이나마 도움이 되는 글이었으면 좋겠다.


출처: http://multifrontgarden.tistory.com/97 [우리집앞마당]
```

### DAO
`データの呼び出し`：単一のデータアクセスと更新処理(CRUD)。

### Service
`データの加工`：複数のDAOを呼び出し、ユーザーの要求に従って加工(ビジネスロジック)する。つまりトランザクション単位である。

