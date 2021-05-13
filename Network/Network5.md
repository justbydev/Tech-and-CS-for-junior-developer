# 5. Application Layer 구조
## 1) Application layer란
+ ISO/OSI 7계층에서의 최상위 계층
+ end system에 존재하는 layer로써 많은 응용 프로그램들이 상주하고 있는 계층이고 application layer를 시작으로 network에 접근할 수 있게 된다.
+ Application의 구조는 Client-Server 구조와 Peer-to-Peer(P2P) 구조 2가지가 있다.

## 2) Client-Server 구조
1. Server
+ Client와 Server로 이루어져 있다.
+ Server는 항상 host(end system)에 존재하며 영구적인 IP address를 가지고 있다.
+ Client의 request를 받아서 요구하는 데이터 등을 response로 주는 역할을 한다.

2. Client
+ Server에게 request를 보내는 대상으로써 response로 Server로부터 원하는 데이터를 받는다.
+ network에는 필요할 때마다 간헐적으로 연결되며 변동적인 IP address를 가지고 있다.
+ Client끼리는 데이터를 주고받을 수 없으며 항상 Server를 통해서만 가능하다.

3. 예시
+ 내가 현재 사용하고 있는 노트북은 client 역할을 하게 되고 특정 홈페이지에 들어가게 되면 그 홈페이지가 서버가 되어 서버에게 홈페이지에 필요한 다양한 object를 요청해서 return받게 된다.

## 3) Peer-to-Peer(P2P) 구조
+ 항상 host에 존재하는 Server가 없으며 end system은 서로 직접적으로 통신을 주고받는다.
+ 서로가 서로의 peer가 되어 서로 필요한 데이터를 제공하고 요구하는 구조(self scalability)

## 4) Process communication
+ application layer에 존재하는 end system(host)끼리 통신한다는 것은 결국 host 내의 process끼리 통신하는 것
+ 결국, 모든 것은 process가 된다.
+ 처음 통신을 시작하는 process는 client process이고 client process가 통신을 시작하기를 기다리는 process를 server process라고 한다.
+ client/server process는 앞에서 말한 client-server 구조와는 다른 것으로 peer-to-peer 구조에서도 통신을 먼저 시작하는 process는 client process, 이를 기다리는 process는 server process라고 부르는 것
+ 결국, process는 server process와 client process로 이루어져 있으며 하나의 process는 역할이 정해져 있지 않고 두 가지 역할 모두가 될 수 있다.

[참고 자료: Computer Networking: A Top-Down Approach 7th edition]
