# 6. Web & HTTP
## 1) Web page
+ 우리는 노트북, 스마트폰 등을 이용해서 수많은 웹페이지에 접근한다.
+ 그러한 웹페이지는 HTML 파일, 이미지, 오디오 파일 등 수많은 object들로 구성되어 있다.
+ 각각의 object들은 그들을 구분하는 address를 가지고 있는데 그것이 URL이다.(요즘은 정형화된 인터넷 자원 식별자를 의미하는, URL의 상위 개념인 URI를 사용하기도 한다.)
+ 결론적으로 웹페이지에 볼 수 있는 것은 웹브라우저(client)가 웹서버(server)로부터 수많은 object를 받아오기 때문이고 이는 HTTP protocol을 통해서 이루어진다.

## 2) HTTP
+ HyperText Transfer Protocol의 약자
+ Application layer의 protocol 중 하나로써 웹브라우저와 웹서버가 주고받는 message의 대한 통신 규약
+ 웹브라우저는 HTTP Request를 웹서버에게 보내고 웹서버는 request에 해당하는 object들을 HTTP Response로 보낸다.
+ HTTP는 TCP protocol(Transport Layer의 protocol 중 하나로써 process사이의 통신을 위한 소켓을 만들고 HTTP에 해당하는 포트 번호는 80)를 사용
+ TCP를 사용하기 때문에 HTTP message를 주고받기 위해서는 반드시 TCP connection이 먼저 이루어져야 한다.(Transport Layer의 TCP에서 정리 예정)
+ HTTP는 stateless로써 과거 클라이언트의 request가 보관되지 않는다.
+ HTTP는 non-persistent HTTP와 persistent HTTP 두가지로 나뉜다.

## 3) Non-persistent HTTP
+ TCP connection이 형성되면 그 connection을 통해서 최대 한개의 object만이 전송되며 전송 이후 TCP connection은 닫힌다.
+ 전송되어야 할 object가 여러개라면 그 수만큼 매번 TCP connection이 형성되어야 한다.
+ message가 클라이언트에서 서버로 갔다가 다시 그에 대한 response가 올때까지의 시간을 RTT(Round Trip Time, 왕복시간)이라 한다.
+ Non-persistent HTTP의 경우 한개의 object 당 TCP connection 형성을 위한 1RTT, object를 위한 1RTT, object transmission time까지 총 2RTT+transmission time이 걸린다.
+ 각각의 object를 위해 매번 TCP connection이 형성되기 때문에 OS overhead가 발생할 수 있다.

## 4) Persistent HTTP
+ Non-persisten HTTP와 달리 한번 TCP connection이 형성되면 여러 object가 한번에 전송될 수 있다.
+ 한번 TCP connecton 형성을 위한 1RTT 이외에 모든 object를 받기 위해 1RTT 만큼의 시간만 걸린다.

[참고 자료: Computer Networking: A Top-Down Approach 7th edition]
