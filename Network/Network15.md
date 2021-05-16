# 15. Congestion control(혼잡 제어)
## 1) Congestion control 이란
+ 혼잡이라는 것은 너무 많은 데이터가 너무 빠르게 전송되어 네트워크에서 handle하기 어려운 상태를 말한다.
+ 라우터의 buffer가 수용하기 어려울 정도로 너무 많은 데이터가 너무 빠르게 전송되거나 한 라우터에 데이터가 몰리는 등의 현상이 발생하면 delay, loss가 발생하고 재전송이 이루어져야 한다.
+ 라우터의 buffer가 full이 되는 경우, packet loss가 발생하여 불필요한 재전송이 이루어지는 경우, 한 라우터에 데이터가 몰려 특정 link의 데이터는 전부 loss가 발생하는 등이 모두 혼잡 상황의 예시이다.
+ 이러한 네트워크의 혼잡 상황을 피하기 위하여 송신 측에서 전송하는 데이터의 양, 즉, 데이터 전송 속도를 조절하는 것을 Congestion control(혼잡 제어)라고 한다.

## 2) AIMD(Additive Increace Multiplicative Decrease)
+ Additive Increase란 전송 패킷의 loss가 발견되기 전까지(에러 탐지, timeout) window size를 1(MSS=Maximum Segment size)씩 증가시키면서 전송하는 것을 말한다.
+ Multiplicative Decrease란 패킷 loss(에러 탐지, timeout)가 발생하면 현재 window size를 절반으로 감소시키는 것을 말한다.
+ 여기서 말한 패킷 loss, 에러 탐지, timeout등은 전부 혼잡 상황이라고 볼 수 있다.
+ 이 방법을 통해서 여러 host들의 TCP fair를 이룰 수 있다.
+ 초반에는 가장 처음 공유 네트워크에 진입한 host의 window size가 크지만 시간이 흐름에 따라서 Multiplicative Decrease에 의해서 점점 window size가 비슷해지면서 평형 상태가 된다.
+ 하지만 에러가 발생, 즉, 혼잡 상태에 직면해서야 처리를 한다는 문제가 있다.

## 3) Slow Start
+ 가장 처음 window size는 1MSS 이다.
+ 전송 패킷 loss(에러 탐지, timeout)이 발생하기 전까지 현재 window size의 2배가 된다.
+ 즉, exponentially하게 window size가 증가한다.
+ 또한, window size 증가에 threshold가 있어서 증가하다가 threshold가 되면 AIMD에서 사용했던 Additive Increase를 한다.(1 MSS만큼씩 증가)
+ 혼잡 상황에 직면하게 되면 일반적으로 window size는 다시 1이 된다.
+ 또한, 혼잡 상황에 직면하게 되면 threshold는 현재 window size(감소하기 전 혼잡 상황이 되었을 떄의 window size)의 절반이 된다.
+ 혼잡 상황에 직면했을 때 결정하는 window size를 결정하는 방법은 TCP Tahoe와 TCP RENO에 따라 다르다.

## 4) TCP Fast retransmit
+ 수신측에서는 예상한 패킷이 도착하지 않는다면 순서대로 정상적으로 도착한 마지막 패킷에 대한 ACK 패킷을 전송한다.
+ 이때, 만약 송신측이 중복된 ACK 패킷을 3개 받게 되면(3 duplicate ACK) 송신측에서는 그에 해당하는 패킷에 에러가 발생했음을 인지하게 된다.
+ 따라서, timeout이 되지 않아도 즉시 재전송을 하게 되는데 이를 Fast retransmit이라고 한다.

## 4) TCP Tahoe
+ Tahoe의 경우 timeout에 의한 loss라면 window size는 다시 1이 된다.
+ 중복 ACK(3 duplicate ACK)에 의한 loss여도 window size는 다시 1이 된다.

## 5) TCP RENO
+ timeout에 의한 loss라면 window size는 다시 1이 된다.
+ 중복 ACK(3 duplicate ACK)에 의한 loss라면 현재 window size의 절반이 된다.
+ 현재 window size의 절반이 된다는 것은 threshold와 같은 값을 가지게 되는 것이고 threshold 이후는 Additive Increase를 하기 때문에 이후 1 MSS 만큼씩 증가한다.

[참고 자료: Computer Networking: A Top-Down Approach 7th edition]
