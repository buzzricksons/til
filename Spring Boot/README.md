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


# その他
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