# 1. Internet이란
## 1) Internet이란
+ Internet이란 수많은 computing device들이 서로 얽혀서 구성한 network를 말한다.
+ Internet은 end system, communication link, packet switches로 구성되어 있다.
+ end system은 host라고도 불리며 사람들이 사용하는 수많은 기기 장치들을 말한다.
+ communication link는 network를 연결해주는 역할을 한다.
+ packet switches는 switch, router로 구성되는 구조로써 수많은 end system은 packet switch를 통해서 서로 통신을 하고 데이터를 주고받게 된다.

## 2) network core
+ 앞서 packet switches와 communication link를 설명했는데 수많은 packet switches들과 communication link로 구성되어 있는 것을 network core라고 한다.
+ 결국, 우리가 사용하는 수많은 기기들(노트북, 스마트폰, 네트워크 통신을 필요로 하는 수많은 기기들)이 서로 통신을 하고 데이터를 주고받을 수 있는 것은 network core가 있기 때문이다.
+ 즉, network core는 network를 구성하고 있으며 우리는 이렇게 구성된 network를 이용하여 수많은 서비스들을 사용할 수 있게 된다.

## 3) protocol
+ end system은 서로 통신을 하게 되는데 이를 위해 서로 message를 주고 받게 된다.
+ OS에서 같은 end system 내의 process끼리 IPC를 통해서 통신을 했다면 서로 다른 end system에는 서로 다른 process가 존재하고 이런 process끼리 통신하기 위해서 network를 통해서 message를 주고 받게 된다.
+ 이런 message를 주고 받기 위해서는 message의 format, order, request/response type, action 등을 규정할 수 있는 통신 규약이 필요한데 그것이 바로 protocol
+ end system의 process에서 message를 보내면 network를 통과하여 다른 end system의 process로 전달되는데 이런 network는 여러 계층의 layer로 구성되어 있고 각각의 layer에서 사용하는 protocol은 다르다.
+ 각 layer의 protocol들이 규정한 통신 규약에 따라서 process끼리 message를 주고받는다.

[참고 자료: Computer Networking: A Top-Down Approach 7th edition]
