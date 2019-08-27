# Command
### Start at background
https://www.elastic.co/guide/en/elasticsearch/reference/current/starting-elasticsearch.html

```
$ ./elasticsearch -d -p pid
```

# Type
### text
- [Elasticsearch] 문자열 Data Type과 Analyze: http://asuraiv.blogspot.com/2017/08/elasticsearch-data-type-analyze.html

# Query
- ElasticSearch 에서 term, match, match_phrase 쿼리에 대한 이해: https://findstar.pe.kr/2018/01/19/understanding-query-on-elasticsearch/



# Etc
### Token filter
https://jjeong.tistory.com/1358

```
Keyword 필드의 Value 는 Token filter 적용이 되지 않습니다.

대소문자 구분에 주의 해서 사용 하셔야 합니다.
```

# 성능관련
- https://m.blog.naver.com/PostView.nhn?blogId=freepsw&logNo=221217517275&proxyReferer=https%3A%2F%2Fwww.google.com%2F
- https://wishgone.tistory.com/entry/elasticsearch-indexing-Performance-Tips-%EC%97%98%EB%9D%BC%EC%8A%A4%ED%8B%B1%EC%84%9C%EC%B9%98
- https://wedul.site/613
- ElasticSearch 인덱싱 성능 최적화: https://brunch.co.kr/@alden/37

# Java High Level Client
When Spring Boot
```
    <properties>
        <java.version>1.8</java.version>
        <elasticsearch.version>7.3.0</elasticsearch.version>
    </properties>

    <dependency>
        <groupId>org.elasticsearch.client</groupId>
        <artifactId>elasticsearch-rest-high-level-client</artifactId>
        <version>7.3.0</version>
    </dependency>
    <dependency>
         <groupId>org.elasticsearch</groupId>
         <artifactId>elasticsearch</artifactId>
    </dependency>
```