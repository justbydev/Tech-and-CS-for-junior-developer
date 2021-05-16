# 16. UDP
## 1) UDP 란
+ UDP란 User Datagram Protocol로써 TCP와 함께 Transport layer의 protocol이다.
+ 비연결형, 신뢰성(reliability)이 없는 전송 프로토콜이다.
+ out-of-order 프로토콜이다.
+ 혼잡 제어, 흐름 제어를 하지 않는다.
+ 에러 제어의 경우 checksum을 사용한다.
+ 신뢰성(reliability)를 얻기 위해서는 application layer에서 처리해주어야 한다.
+ 비연결형이라는 것은 TCP와 같이 connection을 이룰 필요가 없다는 뜻이다.
+ DNS, Multimedia, Real time protocol등에서 사용한다.

## 2) UDP checksum
1. segment content, header를 합하여 16 bit integer를 만들고 전부 더한다.
2. 더한 결과를 one's complement하고 UDP segment header의 checksum에 저장한다.
3. 수신측에서 받은 segment의 content, header에 대한 checksum 연산을 한다.
4. 만약 header에 있는 checksum과 수신측에서 연산한 checksum이 같으면 error가 없고 다르면 error가 발생한 것이다.

## 3) UDP 장점
+ connection을 하지 않기 때문에 그에 대한 overhead가 발생하지 않는다.
+ 혼잡 제어를 하지 않기 떄문에 속도가 빠르다.
+ header size가 작다.

[참고 자료: Computer Networking: A Top-Down Approach 7th edition]
