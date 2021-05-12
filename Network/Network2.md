# 2. Network core
## 1) Network core란
+ 수많은 computing device로 구성된 network를 Internet이라고 하는데 Internet 구성 요소 중에서 switch, router로 구성되어 있는 부분은 packet switches라고 한다.
+ 이런 packet switches들로 구성되어 end system을 network에 접근할 수 있도록 하는 것을 network core라고 한다.
+ network core는 수많은 router, switch로 구성되어 있는데 이들끼리 통신하는 방법은 packet switching, circuit switching 2가지가 있다.

## 2) Packet Switching
+ end system에서 온 message를 작은 data chunk 단위인 packet으로 break하여 link를 통해서 전송하는 기법
+ store and forward 방식을 사용하는데 packet을 구성하는 모든 bit가 전부 router에 도착해야 다음 link로 전송되는 것을 말하며 모든 packet이 도착하기 전까지 router의 buffer에 store된다.
+ pacekt이 전송되는 link capacity에 따라서 router에 도착한 packet이 바로 link로 전송될 수 없는 경우도 있기 때문에 delay, loss 발생 가능

## 3) Circuit Switching
+ Packet switching이 link capacity에 따라서, 현재 traffic에 따라서 전송되는 packet이 다르고 delay, loss가 발생할 수도 있던 반면 circuit switching의 경우 link가 특정 resource에게 할당되어 그 resource만이 전송되는 방식
+ link가 reserved 되기 때문에 delay, loss가 발생하지 않는다.
+ link를 나누는 기준에 따라 frequency에 의해 나누는 FDM(Frequency Division Multiplexing), TDM(Time Division Multiplexing)으로 구분한다.
+ 비록 delay, loss가 발생하지는 않지만 만약 reserved된 link로 전송되는 resource가 없다면 idle 상태가 된다.
+ 따라서, packet switching의 경우가 같은 시간안데 더 많은 사용자가 network에 접근할 수 있다.

## 4) Routing & Forwarding
+ Network core의 가장 중요한 두가지 기능이 바로 Routing, Forwarding
+ Routing은 message의 시작점인 source에서 도착점인 destination까지 packet이 가는 route를 결정하는 것
+ Forwarding은 packet이 router에 들어오면 source, destination 정보에 따라서 packet이 나갈 output link를 결정하는 것
+ Routing은 전체 네트워크에서 source에서 destination까지의 경로를 찾는 것이고 Forwarding은 하나의 router에서 input으로 들어온 packet이 나갈 output link를 결정하는 것
+ 간단한 실생활 예시로 한국->터키->프랑스로 간다고 하면 이 전체 비행 경로를 구하는 것이 Routing이고 터키 항공에서 내려서 프랑스행 비행기를 타기 위해 어떤 gate로 가야하는지를 결정하는 것이 Forwarding
+ 후에 Routing, Forwarding은 Network layer에서 더 자세히 볼 예정

[참고 자료: Computer Networking: A Top-Down Approach 7th edition]
