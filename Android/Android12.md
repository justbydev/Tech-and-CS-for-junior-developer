# 12. HTTP 통신과 REST
## 1) 외부 DB
+ 안드로이드는 외부 DB에 직접 접근할 수 없어서 중간에 웹 서버의 중계 필요
+ 안드로이드-웹서버-외부 DB
+ 웹서버와의 통신이 필요한데 통신 방식은 크게 HTTP 통신과 Socket 통신 2가지가 있다.
## 2) HTTP 통신
+ HTTP는 server-client 구조를 가지고 있다.
+ HTTP 통신은 client의 요청이 있을 때 connection이 형성되면서 server가 응답하여 요청한 정보를 전송하고 연결을 바로 끊는 방식
+ server는 client에게 요청을 할 수 없는 단방향적 통신
+ 안드로이드에서는 HTTPURLConnection과 더불어 AsyncTask, OKhttp3, Volley, Retrofit2 등을 통해 가능하다.

## 3) Socket 통신
+ server와 client가 socket을 열고 특정 포트를 통해서 연결하여 실시간으로 통신
+ HTTP 통신에서는 client만이 server에게 요청을 보낼 수 있었지만 Socket 통신에서는 server도 client에게 요청 전송 가능
+ 양방향 통신이며 연결을 유지한다.
+ 실시간 채팅, 스트리밍과 같은 경우 Socket 통신을 한다.
+ 안드로이드에서는 ServerSocket을 사용하거나 Socket.io 라이브러리가 있다.

## 4) REST
+ REST는 HTTP 통신을 보다 간편하게 해줄 수 있도록 지원하는 소프트웨어 아케틱처
+ 웹 서버를 통해서 가지고 올 수 있는 자원들은 HTTP URI(웹 자원의 정형화된 식별자) 형태로 표현되어 있다.
+ REST라는 것은 HTTP 프로토콜의 인프라를 그대로 사용하면서 웹 상의 자원들을 HTTP URI로 명시하고 HTTP method(GET, POST, PUT, DELETE)를 통해서 해당 자원들에 대한 CRUD operation을 적용하는 것을 말한다.
+ HTTP이기 때문에 client가 server에게 요청하여 자원을 받는 것이고 자원의 상태를 Representation이라고 한다.
+ REST에서의 Representation은 주로 XML, JSON 형태로 되어 있다.
+ 또한 이를 이용한 API를 REST API라고 한다.
+ 여러 오픈 API들도 현재는 REST 방식을 사용하고 있다.

## 5) 참고자료
https://velog.io/@wlsdud2194/HTTP-REST-API-%EB%9E%80
