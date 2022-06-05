# Test Annotation
| annotaion       | description             | Bean scope                        | memo| 
| --------------- | ----------------------- | --------------------------------- | --------------- |
| @SpringBootTest | 전체 테스트 어노테이션  | app에 주입된 Bean 전체            || 
| @WebMvcTest     | Controller Layer 테스트 | MVC관련 Bean(Controller, Service) | ※Slice Test |
| @DataJpaTest    | Jpa(DB I/O) 테스트      | JPA관련 Bean (Entity Manager)     | ※Slice Test |
| @RestClientTest | Rest API 테스트         | RestTemplate등 일부 Bean          | |
| @JsonTest       | Json 데이터 테스트      | Json 관련 일부 Bean               | |

