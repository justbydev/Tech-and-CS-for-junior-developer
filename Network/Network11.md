# 11. TCP
## 1) TCP 개요
+ TCP는 보통 IP와 함께 사용하게 되며 TCP가 주로 data의 reliable transfer를 담당한다.
+ Reliable(신뢰성 있는)하고 in-order한 데이터 전송을 지원하는 transfer control protocol이다.
+ 흐름제어(flow control), 혼잡 제어(congestion control), 오류 제어(error control)을 한다.
+ 연결 지향형 프로토콜이기 때문에 먼저 handshake 과정을 통해서 connection 설정을 먼저 한다.
+ 통신하기 전에는 3-way handshake를 하고 연결 해제시에는 4-way handshake를 한다.
+ in-order를 지향하기 때문에 데이터 전송 순서를 보장한다.
+ HTTP, SMTP, FTP 등에서는 TCP를 사용한다.
+ connection-oriented multiplexing을 한다.

## 2) TCP reliable transfer
+ TCP는 reliable한 데이터 전송을 위해서 여러 가지 방법을 사용한다.
+ TCP는 reliable data transfer를 위해서 rdt principle를 1.0에서 3.0까지 발전시키기 이르렀다.
+ TCP가 rdt principle을 위해서 SEQ, ACK, Countdown timer를 사용한다.
+ SEQ는 sequence numbers로써 전송하는 데이터의 첫번째 byte number를 의미한다.
+ ACK는 받은 데이터와 SEQ를 보고 상대방에게 받기를 예상하는 다음 byter number를 의미한다.
+ Countdown timer라는 것은 데이터를 전송 후 그에 대한 ACK를 오기까지 일정한 시간을 countdown하는 역할로써, 만약 일정 시간안에 ACK가 오지 않는다면 timeout이 되어 제대로 전송되지 않았다고 판단하여 재전송할 수 있도록 한다.

## 3) TCP reliable transfer 예시
+ Host가 A, B가 있다.
+ 먼저, A가 SEQ=92, 8 byte data를 보낸다.
+ B는 8 byte data를 받고 현재 온 SEQ가 92이기 때문에 다음에 받고자 예상하는 SEQ는 100이기 때문에 ACK=100을 A에게 보낸다.
+ A는 timeout이 되기 전에 ACK=100인 ACK 패킷을 받으면 SEQ=100과 함께 데이터를 전송한다.
+ 만약, ACK=100인 ACK 패킷이 timeout 되기 전까지 오지 않으면 다시 SEQ=92, 8 byte data을 재전송한다.

[참고 자료: Computer Networking: A Top-Down Approach 7th edition]
