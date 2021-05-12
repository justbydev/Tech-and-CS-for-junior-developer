# 3. Delay
## 1) Delay란
+ Packet switching에서 Packet은 link를 통해서 router끼리 주고받게 되는데 link capacity 혹은 transmission rate(bandwidth)에 따라서 전송되는 속도가 다르게 된다.
+ 또한, router로 packet이 들어오는 속도에 비해 router에서 link로 나가는 속도가 느린 경우도 발생한다.
+ 이러한 경우, packet의 모든 bit가 router에 도착했어도 바로 link로 전송되지 못하고 buffer에 queueing 된다.
+ 이런 상황에서 delay가 발생하게 되고 buffer도 유한 크기를 가지고 있기 때문에 packet loss가 발생하기도 한다.
+ Delay는 Processing Delay, Queueing Delay, Transmission Delay, Propagation Delay의 4가지가 있고 4가지를 합해서 그 router의 delay라고 한다.

## 2) Processing Delay
+ Router로 들어온 bit error를 check하고 output link를 결정하는 걸리는 시간으로 매우 작아서 신경쓰지 않아도 된다.

## 3) Queueing Delay
+ Packet이 output link로 전송되기 위해서 buffer에 queueing되어 있는 시간
+ output link의 congestion이 심하게 되면 buffer도 꽉 차게 되고 결국 loss가 발생할 수 있어 심각한 delay다.
+ 만약, queue가 empty이고 전송되는 packet도 없다면 0

## 4) Transmission Delay
+ Packet의 모든 bit가 output link에 들어가는데 걸리는 시간
+ Packet의 길이를 L, output link의 bandwidth를 R이라고 한다면 L/R로 계산

## 5) Propagation Delay
+ Packet의 하나의 bit가 output link를 통해서 다음 router까지 걸리는 시간
+ output link의 길이를 d, propagation speed(하나의 bit의 속도)를 s라고 한다면 d/s로 계산

## 6) 총 Delay
+ 총 Delay=Processing Delay+Queueing Delay+Transmission Delay+Propagation Delay

## 7) Transmission Delay vs Propagation Delay
+ Transmission Delay는 packet의 모든 bit가 output link에 진입할 때까지 걸리는 시간이고 Propagation Delay는 진입한 이후 하나의 bit가 다음 router까지 가는데 걸리는 시간

[참고 자료: Computer Networking: A Top-Down Approach 7th edition]
