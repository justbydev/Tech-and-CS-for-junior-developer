# 6. IPC(Inter Process Communication)
## 1) IPC란
+ 하나의 end system(예를 들면 각자의 노트북)에는 수많은 process들이 있고 서로 다른 end system에도 서로 다른 process들이 있는데 이런 process 간의 통신을 IPC라고 한다.
+ process는 kernel이 제공하는 IPC에 따라 통신
+ 같은 end system 간에는 shared memory와 message passing 방법을 통해 IPC가 이루어진다.
+ 다른 end system 간에는 주로 socket을 통한 통신이 이루어지는데 이는 network에서 더 자세히 정리할 예정

## 2) Shared memory
+ Process는 각자의 독립된 메모리 영역을 가지고 있으며 서로간의 메모리 영역에 접근하지 못하도록 되어 있다.(Memory Protection)
+ 그런데 만약, 다른 Process의 데이터를 사용해야 하는 경우가 발생할 수 있다.
+ 이를 위해서 사용하는 것이 shared memory 이며 process 간 메모리 영역을 공유해서 사용할 수 있도록 해주는 것을 말한다.
+ kernel의 중재 역할 없이 바로 shared memory에 접근하여 데이터를 공유할 수 있다.

## 3) Message passing
+ shared memory가 kernel의 중재 없이 통신한다면 Message passing은 kernel의 중재를 통해 통신한다.
+ kernel의 중재를 통해서 message를 send하고 receive 하는 방법을 통해 통신
+ 이를 위해서는 Naming, Synchronization, Buffering을 고려해야 한다.
  > ### Naming
  > + send, recieve 할 process 이름을 직접 지정하는 direct
  > + mailbox를 통해서 주고받는 indirect
  > ### Synchronization
  > + blocking(Synchronous)과 non-blocking(Asynchronous)으로 나눈다.
  > + Blocking send: 상대방이 message 받을때까지 sending process가 block 되는 것
  > + Non-blocking send: message 전송 후 자신의 일을 수행하는 것
  > + Blocking receive: 원하는 message 받을 때까지 receiving process가 block 되는 것
  > + Non-blocking receive: 원하는 message가 아니여도 받을만큼만 받고 자신의 일을 수행하는 것
  > ### Buffering
  > + Message는 결국 담길 Queue가 필요하며 그 용량에 따라 나눈다.
  > + Zero capacity: 버퍼링 되지 않는 것
  > + Bounded capacity: 보낼 수 있는 message 개수 제한
  > + Unbounded capacity: 무한정(이론적으로는 그렇지만 사실 내부적으로는 항상 bound가 존재)

## 4) 익명 PIPE(Anonymous PIPE)
+ 파이프를 통해서 두개의 process를 연결할 때 하나의 process는 writing만, 다른 process는 reading만 하는 경우 사용
+ 부모와 자식 process 관계에서만 사용 가능(ancestor 관계)
+ 한쪽 방향으로만 통신 가능(읽기, 쓰기 동시 불가능)

## 5) Named PIPE(FIFO)
+ 익명 PIPE는 오직 부모-자식 관계에서만 사용가능했지만 그 제한을 제거한 PIPE가 Name PIPE
+ 양방향 통신 가능하며 부모-자식 관계가 아닌 전혀 모르는 process끼리도 통신 가능
+ 익명 PIPE와 마찬가지로 한쪽 방향으로만 통신 가능(읽기, 쓰기 동시 불가능)

## 6) Socket programming
+ 네트워크 상에서의 process간의 통신
+ 각각의 process가 생성되면 각각의 socket이 존재하는데 이 socket을 통해서 process간 message를 주고받는다.
+ 또한, socket을 통해 통신하기 위해서는 각각의 process를 위한 identifier가 필요하다.
+ identifier는 IP address와 Port number로 구성
+ 네트워크에서 더 자세히 정리할 예정

[참고자료] Operating System Principles(7th Edition) by Silberschatz et al.
