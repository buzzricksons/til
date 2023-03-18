# Dependencies
`build.gradle`ファイルをデフォルトとして記述します。

### MyBatis
http://www.mybatis.org/spring-boot-starter/mybatis-spring-boot-autoconfigure/
```Text
compile('org.mybatis.spring.boot:mybatis-spring-boot-starter:1.3.1')
compile('org.mybatis:mybatis:3.4.5')
```

### Db Connection
https://github.com/brettwooldridge/HikariCP
```Text
compile('com.zaxxer:HikariCP:2.6.3')
```

### Flyway(Db migartion)
https://flywaydb.org/documentation/plugins/springboot
```Text
compile("org.flywaydb:flyway-core:4.2.0")
```
※ resources/db/migrationフォルダを追加する必要がある。

### Lombok
https://projectlombok.org/
```Text
compileOnly('org.projectlombok:lombok')
```

### Groovy
```Text
apply plugin: 'groovy'
```

### PostgreSQL
```Text
runtime('org.postgresql:postgresql')
```

### Using XML
```Text
<dependency>
    <groupId>com.fasterxml.jackson.dataformat</groupId>
    <artifactId>jackson-dataformat-xml</artifactId>
</dependency>
```


### Live Reload
```Text
runtime('org.springframework.boot:spring-boot-devtools')
```

#### 仕方(Intellij + Chrome)

1. Settings --> Build-Execution-Deployment --> Compiler --> Build Project Automaticallyをチェック
2. ctrl+shift+Aを押下しRegistryで検索 → compiler.automake.allow.when.app.running項目をenabledにする
3. IntelliJの再起動
4. ChromeにLiveReloadプラグインをインストールする。https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei
5. 4番でインストールしたプラグインをonにする

# ORM(Object Relational Mapping)
- HibernateまたはJPAのメリットとデメリット
    - メリット：SQL分を書かなくても良いためコードの量が減る。
    - デメリット：複雑なSQL分の場合、対応が難しい。
- MyBatisのメリットとデメリット
    - メリット：SQL分を書くため、複雑なSQL分でも問題なし。
    - デメリット：SQL分を書くため、コード量が増える。

## Hibernateの利用する場合

## MyBatisを利用する場合
http://www.mybatis.org/mybatis-3/ja/index.html

### Mapperの作成はGroovyを利用する
Javaはsqlをstring文字列で扱うため読みにくい。Groovyを使えば読みやすく書ける。
http://qiita.com/kazuki43zoo/items/0c6ac5acaee1201a433e

#### Java
```Text
@Mapper
public interface CityMapperJava {
    @Select("" +
            "SELECT" +
            " id, name, state, country " +
            "FROM " +
            "city " +
            "WHERE " +
            "state = #{state}" +
            "")
    City findByState(String state);
}
```

#### Groovy
```Text
@Mapper
interface CityMapperGroovy {
    @Select('''
            SELECT
                id, name, state, country
            FROM
                city
            WHERE
                state = #{state}
            ''')
    City findByState(String state);
}
```

### sqlsession
http://www.mybatis.org/spring/ja/sqlsession.html

#### sqlSessionFactoryとsqlSessionTemplateの実装
```Text
@Configuration
@EnableTransactionManagement
@MapperScan("com.example.demo.mapper")
@ComponentScan("com.example.demo")
public class SetupApplicationPersistenceConfig {
 
    @Autowired
    private DataSource dataSource;
 
    @Bean
     public DataSourceTransactionManager transactionManager() {
         return new DataSourceTransactionManager(dataSource);
     }
 
     @Bean
     public SqlSessionFactory sqlSessionFactory() throws Exception {
         SqlSessionFactoryBean sessionFactory = new SqlSessionFactoryBean();
         sessionFactory.setDataSource(dataSource);
         SqlSessionFactory factory = sessionFactory.getObject();
         return factory;
     }
 
     @Bean
     public SqlSession sqlSessionTemplate() throws Exception {
         return new SqlSessionTemplate(sqlSessionFactory());
     }
}
```

#### 動的なSQLの生成
```Text
@Update("<script>
  update CITY
    <set>
      <if test="name != null">name=#{name},</if>
      <if test="state != null">state=#{state},</if>
      <if test="country != null">country=#{country},</if>
    </set>
  where id=#{id}
</script>")
```

#### カラムとオブジェクトのfield名が異なる場合
```Text
@Results({
        @Result(property = "regDm", column = "reg_dm"),
        @Result(property = "updDm", column = "upd_dm")
})
@Select("select * from tsfsmeta where fullpath = #{fullpath} order by reg_dm")
List<SFSMeta> getListByFullPath(@Param("fullpath")String fullPath);
```
## JPAの場合

# AOP

# Batch

# H2 Database(ローカル環境開発用)
### application.properties設定
```Text
spring.datasource.driverClassName=org.h2.Driver
spring.h2.console.enabled=true
spring.datasource.url=jdbc:h2:C:/workspace/boot-practice/ChatPractice/db/db;MODE=PostgreSQL
spring.jpa.hibernate.ddl-auto=update
```

### またはapplication.yml設定
```Text
#H2 Database
spring:
  datasource:
    url: jdbc:h2:mem:example-app;DB_CLOSE_DELAY=-1;DB_CLOSE_ON_EXIT=FALSE
    platform: h2
    username: sa
    password:
  h2:
    console:
    enabled: true
```

### 接続
http://localhost:8080/h2-console

| Key | Value |
|:-|-|
| Driver Class | org.h2.Driver |
| JDBC URL | jdbc:h2:mem:example-app;DB_CLOSE_DELAY=-1;DB_CLOSE_ON_EXIT=FALSE |
| Password ||
| User Name | sa |

# テスト
```Java
/**
 * Initialization class for all test classes.
 *
 * @author HyungCheol Kim
 * @see resources/application.yml
 *
 */
@SpringBootTest
@SpringBootConfiguration
@RunWith(SpringJUnit4ClassRunner.class)
public class AbstractTests {
    private static boolean initialized = false;

    @Value("${setting.browser}")
    String browser;

    @Value("${setting.screenshot-folder}")
    String screenshotFolder;

    /**
     * Initialize before test. This method executed only once.
     *
     * @see com.codeborne.selenide.Configuration
     */
    @Before
    public void initialize() {
        if (initialized) {
            return;
        }

        LocalDateTime now = LocalDateTime.now();
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyyMMddHHmmss");

        System.setProperty("selenide.browser", browser);
        System.setProperty("selenide.reportsFolder", screenshotFolder + now.format(formatter));

        this.initialized = true;
    }
}
```


# Etc
## 複数のTomcatの同時起動
こちらでは3台のTomcatを同時起動する場合の例です。(ポート番号：8880, 8881, 8882)

### 実装クラス
```Java
@Configuration
public class EmbeddedTomcatConfiguration {

    @Value("${server.additionalPorts}")
    private String additionalPorts;

    @Bean
    public EmbeddedServletContainerFactory servletContainer() {
        TomcatEmbeddedServletContainerFactory tomcat = new TomcatEmbeddedServletContainerFactory();
        Connector[] additionalConnectors = this.additionalConnector();
        if (additionalConnectors != null && additionalConnectors.length > 0) {
            tomcat.addAdditionalTomcatConnectors(additionalConnectors);
        }
        return tomcat;
    }

    private Connector[] additionalConnector() {
        if (StringUtils.isEmpty(this.additionalPorts)) {
            return null;
        }
        String[] ports = this.additionalPorts.split(",");
        List<Connector> result = new ArrayList<>();
        for (String port : ports) {
            Connector connector = new Connector("org.apache.coyote.http11.Http11NioProtocol");
            connector.setScheme("http");
            connector.setPort(Integer.valueOf(port));
            result.add(connector);
        }
        return result.toArray(new Connector[]{});
    }
}
```

### Applicationクラス
```Java
@SpringBootApplication
@Import({EmbeddedTomcatConfiguration.class})
public class LukeApplication {

    public static void main(String[] args) {
        SpringApplication.run(LukeApplication.class, args);
    }
}
```

### build.gradle
```Text
compile("org.springframework.boot:spring-boot-starter-tomcat")
```

### application.yml
```Text
server:
  port: ${appPort:8880}
  additionalPorts: 8881,8882
```

## Spring SecurityのせいでH2 Consoleが見えない場合
```Java
@Configuration
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

  @Override
  protected void configure(HttpSecurity http) throws Exception {
    http.headers().frameOptions().disable();
  }
}
```

## build成果物をwarにpackaging
https://www.mkyong.com/spring-boot/spring-boot-deploy-war-file-to-tomcat/

## @Value
https://qiita.com/rubytomato@github/items/d86039eca031ac1ed511

### Multiple variable 1

- Java
```Java
@Value("#{'${my.list.of.strings}'.split(',')}") 
private List<String> myList;
```

- properties
```text
my.list.of.strings=ABC,CDE,EFG
```

### Multiple variable 2
- Java
```Java
@Value("${hoge.fuga}")
private Map<String, String> fuga;
```

- properties
```text
hoge.fuga.key1 = val1
hoge.fuga.key2 = val2
```

# Spring Batch
https://dayone.me/1Sm6zrv

## Disablel Spring Batch Auto Start
https://stackoverflow.com/questions/22318907/how-to-stop-spring-batch-scheduled-jobs-from-running-at-first-time-when-executin

# [Spring] 스프링(Spring) @Qualifier, @Named, @Primary 의존객체 선택
https://engkimbs.tistory.com/683


# springboot외부 jar추가방법
https://joshua90.tistory.com/entry/springboot-%EC%99%B8%EB%B6%80-jar-%EC%B6%94%EA%B0%80-%EB%B0%A9%EB%B2%95

```
[springboot 외부 jar 추가 방법]

springboot app 을 실행하는 방법으로 주로 가이드 되고 있는 방법은  전체 app을 jar or war 로 패키징해서 java -jar 옵션으로 실행 하는 방법이다.

보통의 경우 여기에 application.properties 를 분리해야 설정 파일을 개발 / 운영으로 분리하는 것으로 충분하겠지만
뭐 생각대로 되지 않는 일이 한 두개는 아니겠지.

외부 jar 파일을 포함해서 배포를 해야 하는 일이 발생했다. 

1. 내부 repo 서버에 등록하고 pom.xml 에 추가한다.
2. local dir 에 추가하고 pom.xml 추가한다.
3. java runtime 실행 시 classpath 를 추가 한다.
   
* 여기서 runtime 추가 하는 방법을 기술한다. 
원래는 가장 쉬어 보여 시작했는데 생각 보다 쉽지 않았음.

ref) https://www.baeldung.com/spring-boot-main-class

1. 먼제 jar 파일로 패키징 한다.
2. 메인 jar 파일은 java -cp 옵션으로 패스를 걸어준다.
3. 추가 jar 파일 패스는 -Dloader.path= 옵션으로 걸어 준다.

ex) java -cp bootApp.jar -Dloader.main=org.baeldung.DemoApplication -Dloader.path=add.jar org.springframework.boot.loader.PropertiesLauncher
```

# Print all properties
```
@SpringBootApplication
@EnableJpaAuditing
public class DummyApplication {

	private static final Logger LOGGER = LoggerFactory.getLogger(PropertyLogger.class);

	@EventListener
	public void handleContextRefresh(ContextRefreshedEvent event) {
		final Environment env = event.getApplicationContext().getEnvironment();
		LOGGER.info("====== Luke Environment and configuration ======");
		LOGGER.info("Active profiles: {}", Arrays.toString(env.getActiveProfiles()));
		final MutablePropertySources sources = ((AbstractEnvironment) env).getPropertySources();
		StreamSupport.stream(sources.spliterator(), false)
			.filter(ps -> ps instanceof EnumerablePropertySource)
			.map(ps -> ((EnumerablePropertySource) ps).getPropertyNames())
			.flatMap(Arrays::stream)
			.distinct()
			.filter(prop -> !(prop.contains("credentials") || prop.contains("password")))
			.forEach(prop -> LOGGER.info("{}: {}", prop, env.getProperty(prop)));
		LOGGER.info("===========================================");
	}

	public static void main(String[] args) {
		SpringApplication.run(DummyApplication.class, args);
	}

}
```

# Hikari
- [SpringBoot] hikariCP + PostgreSQL + mybatis 연동하기 (1)
    - https://tlatmsrud.tistory.com/71
- [Spring] DB커넥션풀과 Hikari CP 알아보기
    - https://velog.io/@miot2j/Spring-DB커넥션풀과-Hikari-CP-알아보기
- Hikari CP / Spring boot 설정
    - https://girinprogram93.tistory.com/46
- https://velog.io/@miot2j/Spring-DB%EC%BB%A4%EB%84%A5%EC%85%98%ED%92%80%EA%B3%BC-Hikari-CP-%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0

# Multiple datasource
- Spring Boot 1개에 DB 2개 연결?
    - https://wooki92.tistory.com/m/12
- Spring JPA Multiple Databases 설정
    - https://2dongdong.tistory.com/33
- Spring Boot JPA - multiple database 설정.
    - https://mudchobo.github.io/posts/spring-boot-jpa-multiple-database
- [SPRINGBOOT] 멀티 데이터베이스(DB) 설정하기 JPA 편
    - https://minaminaworld.tistory.com/219
- [springboot] jpa 2개이상 DB사용(querydsl 설정 포함)
    - https://lemontia.tistory.com/967
- SPRING JPA 다중DB 접속
    - https://eternalteach.tistory.com/67
- lombokで@RequiredArgsConstructorに@Qualifierを渡したいときのlombok.config
    - https://qiita.com/hrkt/items/e7c67c4d4de53bcb613b

## 트랜잭션 바인딩
- Spring 다중 데이터소스 설정 및 트랜잭션 동기화
    - https://yousrain.tistory.com/50
- Springboot + JPA + JTA (Atomikos) + MySQL 을 이용한 멀티 데이터베이스
    - https://www.4te.co.kr/894

## investigated article
Spring JPA - Multiple Databases
- https://www.baeldung.com/spring-data-jpa-multiple-databases
- https://www.baeldung.com/spring-boot-configure-multiple-datasources
- https://javatodev.com/multiple-datasources-with-spring-boot-data-jpa/

Hibernate doc(setting)
- https://docs.jboss.org/hibernate/orm/5.2/userguide/html_single/appendices/Configurations.html

Spring Boot 2 Multiple Datasources initialize schema
- https://stackoverflow.com/questions/51146269/spring-boot-2-multiple-datasources-initialize-schema

remove lombok alert for @Qualifier when using @RequiredArgsConstructor
- https://qiita.com/hrkt/items/e7c67c4d4de53bcb613b
- https://stackoverflow.com/questions/38549657/is-it-possible-to-add-qualifiers-in-requiredargsconstructoronconstructor

DataSourceが複数ある場合にSpring Testの@Sqlを使う場合の落とし穴
- https://qiita.com/suke_masa/items/1461166badd9f94abcb2

SpringBoot error: Registered driver with driverClassName=oracle.jdbc.driver.OracleDriver was not found, trying direct instantiation
- https://stackoverflow.com/questions/52014595/springboot-error-registered-driver-with-driverclassname-oracle-jdbc-driver-orac

spring.jpa.hibernate.ddl-auto issue
- https://stackoverflow.com/questions/28275448/multiple-data-source-and-schema-creation-in-spring-boot
- https://stackoverflow.com/questions/23494157/what-is-exact-behavior-of-hibernate-hbm2ddl-auto-update-in-hibernate

# JWT
- Spring boot jwt token 사용하기
    - https://charlie-choi.tistory.com/211
- Spring boot환경에서 JWT 사용하기
    - https://alwayspr.tistory.com/8
- 스프링 부트에서 JWT(Json Web Token) 구현
    - https://hyojun123.github.io/2018/07/17/JWT2/
- spring jjwt 설명 및 예제
    - https://idlecomputer.tistory.com/242
- Spring Boot Security + JWT Hello World Example
    - https://medium.com/swlh/spring-boot-security-jwt-hello-world-example-b479e457664c
- 



