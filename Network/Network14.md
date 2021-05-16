# 14. TCP Handshake
## 1) TCP Handshake란
+ TCP는 연결지향 프로토콜로써, 데이터 통신 이전에 먼저 클라이언트와 서버 사이의 connection이 이루어져야 하는데 이 과정이 handshake다.
+ 연결이 이루어질 때에는 3-way handshake를 사용하고 연결 해제를 할 때에는 4-way handshake를 사용한다.
+ 연결을 요청할 때 보내는 패킷을 SYN(Synchornize Sequence Number) 패킷이라고 한다.
+ SYN 패킷에 대한 연결 요청 수락 응담은 ACK(Acknowledgement) 패킷이라고 한다.
+ 연결 해제를 요청할 때 보내는 패킷을 FIN(Finish) 패킷이라고 한다.

## 2) 2-way가 아닌 3-way를 사용하는 이유
+ TCP는 양방향성 연결이다.
+ 클라이언트는 서버에게 자신의 존재를 알리고 현재 활성화되어 있음을 알린다.
+ 이와 마찬가지로 서버도 클라이언트에게 자신의 존재를 알리고 현재 활성화되어 있음을 알려야 한다.
+ 이처럼 양측에서 서로의 존재를 인식하고 서로가 데이터 통신을 할 수 있는 상태임을 알리기 위하여 3-way를 사용한다.

## 3) 3-way handshake 과정(연결)
1. 클라이언트는 서버에 접속을 요청하는 SYN 패킷을 SYNbit과 SEQ을 담아서 보낸다.
2. 서버는 클라이언트 요청에 대한 수락 응답으로 ACK 패킷을 ACKbit과 SEQ에 대한 ACK number를 보내고 이와 함께 서버도 클라이언트에게 포트를 열어달라는 SYN 패킷을 SYNbit과 SEQ을 담아서 보낸다.
3. 클라이언트도 서버 요청에 대한 수락 응답으로 ACK 패킷을 ACKbit과 SEQ에 대한 ACK number를 보냄으로써 연결이 성립된다.
![캡처](https://user-images.githubusercontent.com/17876424/118387626-63a4f900-b65a-11eb-9624-e48c0372c812.PNG)

## 4) 4-way handshake 과정(연결 해제)
1. 클라이언트는 서버에게 연결을 해제하고자 FIN 패킷을 FINbit과 SEQ를 담아서 보낸다.
2. 서버는 클라이언트의 요청에 대한 수락 응답으로 ACK 패킷을 ACKbit과 SEQ에 대한 ACK number를 담아서 보낸다
3. 서버는 우선 자신이 처리해야 할 작업들이 끝날때까지 기다린다.
4. 모든 작업이 끝났다면 서버는 클라이언트에게 연결을 해제하고자 FIN 패킷을 FINbit과 SEQ를 담아서 보낸다.
5. 클라이언트는 서버의 요청에 대한 수락 응답으로 ACK 패킷을 ACKbit과 SEQ에 대한 ACK number를 담아서 보낸다.
6. 서버가 ACK 패킷을 받으면 소켓 연결을 닫는다.
7. 클라이언트는 서버로부터 아직 받지 못한 데이터가 있을 수 있으니 조금 더 wait 했다가 연결을 종료한다.
![캡처](https://user-images.githubusercontent.com/17876424/118387736-107f7600-b65b-11eb-8c97-a0324354fe85.PNG)

[참고 자료: Computer Networking: A Top-Down Approach 7th edition]
