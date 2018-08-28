# Sessionの仕組み
1.まずClientの最初のRequestでWeb ContainerはユニックなSession IDを生成し、これをResponseと共にClientに返す。これはWeb Containerにより生成された臨時Sessionである。
2.Web ContainerがRequestの元が識別できるようにClientは各Requestと共にSession IDを再度送信する。
3.Web ContainerはこのIDと一致するSession IDを探し、RequestにSessionをつなぐ。


1.먼저 Client의 첫 번쨰 Request에서 Web Container는 고유 Session ID를 생성하고 이를 Response와 함께 Client에게 돌려준다. 이는 Web Container에 의해 생성된 임시 Session이다.
2.Web Container가 요청의 출처를 식별할 수 있도록, Client는 각 요청과 함께 Session ID를 다시 전송한다.
3.Web Container는 이 ID와 일치하는 Session ID를 찾고, Request에 Session을 연결한다.

# Session Clustering
### Tomcat(or Jboss) session clustering
- https://tomcat.apache.org/tomcat-7.0-doc/cluster-howto.html
- http://take0415.blog.me/221023934579

### Memcached session manager
http://hskimsky.tistory.com/3

### Sticky Session
https://aws.amazon.com/ko/blogs/aws/new-elastic-load-balancing-feature-sticky-sessions/

### 暗号化されたCookieを利用

# JWT/JSON Web Token
<iframe src="//slides.com/sanghaklee/jwt/embed" width="720" height="420" scrolling="no" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
http://sanghaklee.tistory.com/47


