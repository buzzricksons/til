# 명명규칙
※출처: https://purumae.tistory.com/200

## common
* 소문자를 사용한다.
* 단어를 임의로 축약하지 않는다.
    * register_date (O) / reg_date (X)
* 가능하면 약어의 사용을 피한다.
    * 약어를 사용해야 하는 경우, 약어 역시 소문자를 사용한다.
* 동사는 능동태를 사용한다.
    * register_date (O) / registered_date (X)

## TABLE
* 복수형을 사용한다.
* 이름을 구성하는 각각의 단어를 underscore 로 연결하는 snake case 를 사용한다.
* 교차 테이블 (many-to-many) 의 이름에 사용할 수 있는 직관적인 단어가 있다면 해당 단어를 사용한다.
    * 적절한 단어가 없다면 relationship을 맺고 있는 각 테이블의 이름을 "_and_" 또는 "_has_" 로 연결한다.
* 예
    * articles, movies : 복수형
    * vip_members : 약어도 예외 없이 소문자 & 단어의 연결에 underbar를 사용
    * articles_and_movies : 교차 테이블을 "_and_" 로 연결

## COLUMN
* auto increment 속성의 PK를 대리키로 사용하는 경우, "테이블 이름의 단수형"_id 의 규칙으로 명명한다.
* 이름을 구성하는 각각의 단어를 underscore 로 연결하는 snake case 를 사용한다.
* foreign key 컬럼은 부모 테이블의 primary key 컬럼 이름을 그대로 사용한다.
    * self 참조인 경우, primary key 컬럼 이름 앞에 적절한 접두어를 사용한다.
    * 같은 primary key 컬럼을 자식 테이블에서 2번 이상 참조하는 경우, primary key 컬럼 이름 앞에 적절한 접두어를 사용한다.
* boolean 유형의 컬럼이면 "_flag" 접미어를 사용한다.
* date, datetime 유형의 컬럼이면 "_date" 접미어를 사용한다.
* 예
    * article_id, movie_id : "테이블 이름의 단수형" + "_id"
    * complete_flag : boolean 유형의 컬럼
    * issue_date : 날짜 유형의 컬럼

## INDEX
* 이름을 구성하는 각각의 단어를 hyphen 으로 연결하는 snake case 를 사용한다.
* 접두어
    * unique index : uix
    * spatial index : six
    * index : nix
* "접두어"-"테이블 이름"-"컬럼 이름"-"컬럼 이름"
* 예
    * uix-accounts-login_email

## FOREIGN KEY
* 이름을 구성하는 각각의 단어를 hyphen 으로 연결하는 snake case 를 사용한다.
* "fk"-"부모 테이블 이름"-"자식 테이블 이름"
    * 같은 부모-자식 테이블에 2개 이상의 foreign key가 있는 경우, numbering합니다.
* 예
    * fk-movies-articles : article 테이블이 movie 테이블을 참조
    * fk-admins-notices-1 / fk-admins-notices-2 : notices 테이블이 admins 테이블을 2회 이상 참조하여 numbering

## VIEW
* 접두어 "v"를 사용한다.
* 기타 규칙은 TABLE과 동일
* 예
    * v_privileges

## FUNCTION
* 접두어 "usf"를 사용한다.
* 이름을 구성하는 각각의 단어를 underscore 로 연결하는 snake case 를 사용한다.
* 예
    * usf_random_key

## TRIGGER\
* 이름을 구성하는 각각의 단어를 underscore 로 연결하는 snake case 를 사용한다.
* 접두어
    * tra : AFTER 트리거
    * trb : BEFORE 트리거
* "접두어"_"테이블 이름"_"트리거 이벤트"
* 예
    * tga_movies_ins : AFTER INSERT 트리거
    * tga_movies_upd : AFTER UPDATE 트리거
    * tgb_movies_del : BEFORE DELETE 트리거