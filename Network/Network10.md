# 10. Multiplexing
## 1) Multiplexing, Demultiplexing
+ Transport Layer에는 TCP, UDP protocol 두가지가 있으며 Application layer는 반드시 둘 중 하나의 transport layer를 사용해야 한다.
+ Application layer의 process 끼리 주고받는 데이터는 소켓을 통해서 주고받게 되는데 process의 수는 엄청 많고 따라서, 데이터를 주고받고자 하는 process와 연결이 잘 되어야 한다.
+ 각각의 process는 각자의 socket을 가지고 있다.
+ Process를 구분하기 위한 identifer로써 IP address와 Port number를 사용한다.
+ Multiplexing이란 전달하고자 하는 데이터가 제대로된 process에게 전달되기 위해서 IP address, port number 등을 주고 받는 데이터의 header information에 encapsulate 하는 것
+ Demultiplexing이란 맞는 process에게 전달하기 위해 header information에 담긴 IP address, port number를 해석하는 것
+ Multiplexing은 sender에서 사용하며 Demultiplexing을 receiver에서 사용한다.

## 2) Connectionless demultiplexing
+ Connectionless demultiplexing은 UDP에서 사용하는 demultiplexing
+ UDP는 header에 담긴 destination IP address, port number 두가지 정보를 이용하여 맞는 socket에게 전달한다.
+ 같은 socket에게 전달되는 데이터는 같은 source IP address, port number를 가질 수도 있다.

## 3) Connection-oriented demultiplexing
+ Connection-oriented demultiplexing은 TCP에서 사용하는 demultiplexing
+ TCP는 header에 담긴 destination IP address, port number 뿐 아니라 source IP address, port number까지 총 4가지의 정보를 이용하여 맞는 socket에게 전달한다.

[참고 자료: Computer Networking: A Top-Down Approach 7th edition]
