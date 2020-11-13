# Enum to String
- https://www.baeldung.com/jpa-persisting-enums-in-jpa
- https://thoughts-on-java.org/jpa-21-how-to-implement-type-converter/

# JPA GeneratedValue
* AUTO(default): JPA 구현체가 자동으로 생성 전략을 결정한다.
* IDENTITY: 기본키 생성을 데이터베이스에 위임한다. 예를 들어 MySQL의 경우 AUTO_INCREMENT를 사용하여 기본키를 생성한다.
* SEQUENCE: 데이터베이스의 특별한 오브젝트 시퀀스를 사용하여 기본키를 생성한다.
* TABLE: 데이터베이스에 키 생성 전용 테이블을 하나 만들고 이를 사용하여 기본키를 생성한다.

