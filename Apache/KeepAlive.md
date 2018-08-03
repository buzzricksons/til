
# KeepAlive정의
특정 한 프로세스가 특정 사용자의 지속적인 요청 작업들을 계속해서 처리하도록 함.
즉, 첫 요청 시에 열어 놓은 Port를 끊지 않고, 지정된 KeepAliveTimeout동안 idle하면 끊는다. 
KeepAliveTimeout값이 채워지기 전에 다시 요청이 온다면 다시 KeepAliveTimeout은 다시 0부터 Count를 수행한다.
최종적으로, KeepAliveTimeout 지정한 시간만큼 idle하면 그때, 해당 Port연결을 끊는다.

### 설정법
```text
KeepAlive [On/Off]
MaxKeepAliveRequest [회수]
KeepAliveTimeout [초]
```

#### 사용 예
```text
KeepAlive On
MaxKeepAliveRequest 100
KeepAliveTimeout 60
```

## 개인적인 견해
Client 수가 많을 경우, 상당히 민감하게 작용하는 부분이므로 신중히 설정하여야 한다. 
보통 단발성 요청들이 많을 경우, KeepAlive를 Off하는 것이 좋을 수도 있다.
허나, KeepAlive를 사용하면 웹브라저상에서의 체감속도는 빨라진다는것을 잊지 말자.


필자의 경우, 예전에 그림 파일들이 엑박이 뜨는 문제가 발생하여 해결하고자 사이트 지원을 나갔었는데,
이 문제는 특정 날에만 발생을 하였다. Access로그를 분석한 결과, 해당 날에 요청이 급격히 많았음을 확인하였고,
Errorlog상에서는 많은 요청들이 웹서버단에서 튕겨버림을 확인하였다.

이때, KeepAliveTimeout의 값은 60초 였으며, 서비스 성격 특성상 많은 이미지 파일들의 요청이 src="http://~ " 형식으로 되어 있어서 이 이미지 처리를 위해 매번 이미지 요청시마다 소켓이 새로 생성되었던 것이였다.


그에 따라, KeepAliveTimeout의 수치를 10초 내로 줄였다. 그러자 해당 문제는 해결 되었다.


> 출처: http://mcpaint.tistory.com/141 [MC빼인트와 함께]


# [apache] keepalive timeout 설정에 대해서..  WAS / 인프라관리 

2015. 10. 20. 0:26복사http://sim3peanut.blog.me/220513667593
 

## 1. 개요

    apache 의 keep alive 옵션을 on으로 하면 클라이언트와 apache 간의 tcp 커넥션을 keepalivetimeout 동안 유지하게 된다. keep alive timeout 설정과 관련하여 고려할 사항들을 정리하였음. 

## 2. 정의

KeepAliveTimeout
Amount of time the server will wait for subsequent requests on a persistent connection

## 3. 고려사항

​

  1) 사용자의 요청량 및 사용자수

       - 인터넷망에서 일반 사용자를 대상으로 접속자 수가 많고  요청량이 많은 웹서비스를 제공 경우,

          keep alivetime을 짧게 가져가는 것이 적절하다. (3초~5초)

      - 60초등과 같이 길게 가져갈경우에는 불필요한 tcp 세션을 유지하게 되고 웹서버의 메모리 사용량이 높아지게 되어 피크시간대에 갑자기 서비스가 안되는 등의 현상이 발생할 수 있다.



      - 폐쇄망에서 내부 사용자를 대상으로 접속자수가 적고, 요청량이 적은 웹서비스를 제공하는 경우,

         keepalivetimeout 시간을 30초~60초 길게 잡는 것이 성능상 유리하다.  



 2) 사용자의 요청간의 간격(think time)

  - 사용자가 한번 요청을 보내고, 다음번 요청을 보내는 간격을 think time이라고 한다. 이 think time과 keep alive time은 어느정도의 갭이 있어야 한다.

        

   실제 사이트에서 클라이언트 로그상으로는 웹서버로 요청을 보냈는데, 웹서버에는 요청 받은 로그가 없으며, 사용자 요청을 처리하지 못하는 문제가 1주 또는 2주간격으로 불규칙적으로 발생을 하는 경우가 있었다.

    

   원인은 keepalivetimeout 시간이 15초로 되어 있었는데, 사용자가 해당 화면에서 약 15초 정도 생각하고 요청을 보냈기 때문이었다.

클라이언트 요청 패킷이 보내질때,  웹서버에서는 커넥션을 끊는 Fin 패킷이 보내지면서, 요청패킷이 웹서버로 전달이 되지 않고,  웹서버에 로그도 남지 않았던 것이다. 이후 keepalivetime을 길게 조정하여 문제를 해결하였다. 

# [출처] [apache] keepalive timeout 설정에 대해서..|작성자 우보

## 도대체 KeepAlive란 무엇인가?

apache.org의 KeepAlive에 대해 아래와 같이 정의 되어 있다.

 The Keep-Alive extension to HTTP/1.0 and the persistent connection feature of HTTP/1.1 provide long-lived HTTP sessions which allow multiple requests to be sent over the same TCP connection. In some cases this has been shown to result in an almost 50% speedup in latency times for HTML documents with many images. To enable Keep-Alive connections, set KeepAlive On


HTTP프로토콜상 한번 접속 후 자료를 모두 전송하면 접속을 끊어 버리지만 KeepAlive On상태에서는 KeepAliveTimeOut시간 동안 접속을 끊지않고 다음 접속을 기다린다. 순수 html파일, 이미지파일 등으로만 구성된 서버(동적파일이 없는서버)에 KeepAlive On으로 설정할 경우 50%정도의 성능 향상을 보인다고 한다. 단 이와 같은 성능향상을 보일려면 서버가 바쁘지 않아야 한다. 아주 바쁜 서버 환경에서 KeepAlive On을 설정해 놓을 경우 모든 접속자 마다 연결 유지를 해 놓아야 하기 때문에 아파치 프로세스수가 기하 급수적으로 늘어나 MaxClient값을 초과하게 된다. 또한 On상태일때 접속유지 하는 프로세스들 때문에 메모리를 그 만큼 많이 사용하게 된다. 따라서 KeepAlive값은 단순히 On/Off 시킬것이 아니라 접속자, 메모리용량과 연관해서 값을 설정하여야한다.

 

공간사랑의 KeepAlive 설정

    접속자가 많지만 메모리가 충분하다 : On

    접속자가 많지만 메모리 여유가 없다 : Off

    접속자가 적고 메모리가 충분하다 : On

    접속자가 적고 메모리 여유가 없다 : Off

 

- 메모리가 충분하다는 의미는 접속자가 MaxClient값에 도달했을 경우라고 swap메모리를 사용하지 않는상태를 말한다.

[출처] KeepAlive Off [ Apache ]|작성자 공간사랑

















