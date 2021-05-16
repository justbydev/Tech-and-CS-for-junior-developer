# 11. TCP
+ TCP는 보통 IP와 함께 사용하게 되며 TCP가 주로 data의 reliable transfer를 담당한다.
+ Reliable(신뢰성 있는)하고 in-order한 데이터 전송을 지원하는 transfer control protocol이다.
+ 흐름제어(flow control), 혼잡 제어(congestion control), 오류 제어(error control)을 한다.
+ 연결 지향형 프로토콜이기 때문에 먼저 handshake 과정을 통해서 connection 설정을 먼저 한다.
+ 통신하기 전에는 3-way handshake를 하고 연결 해제시에는 4-way handshake를 한다.
+ in-order를 지향하기 때문에 데이터 전송 순서를 보장한다.
+ HTTP, SMTP, FTP 등에서는 TCP를 사용한다.
+ connection-oriented multiplexing을 한다.

[참고 자료: Computer Networking: A Top-Down Approach 7th edition]
