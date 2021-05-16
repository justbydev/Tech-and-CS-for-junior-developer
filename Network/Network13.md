# 13. Error control(오류 제어)
## 1) 오류 제어
+ TCP는 데이터 전송 과정에서 발생하는 오류에 대해서 제어한다.
+ 오류가 발생하면 TCP에서는 오류가 생긴 패킷에 대해서 재전송한다.
+ TCP가 오류를 파악하는 방법은 크게 두가지로 나눈다.
+ 첫번째는 중복 ACK된 받는 경우인데 이 경우는 TCP는 in-order 방식인데 중간에 in-order하지 않게 전송되는 경우 중간에 빠지게 되는 패킷이 발생하게 된다.
+ 이렇게 빠지게 되면 빠진 데이터에 대해서 중복적인 ACK를 보내게 되고 송신측은 이를 파악하여 재전송하게 된다.
![캡처](https://user-images.githubusercontent.com/17876424/118386939-f1cab080-b655-11eb-9c22-ba97e239341c.PNG)
+ 두번째는 timer에 의한 재전송으로 일정 시간 내에 ACK가 오지 않고 timeout 되면 전송하는 과정에서 제대로 전송되지 않았다고 판단하여 재전송한다.
+ 또한, 수신측은 제대로 받았지만 ACK 패킷이 중간 유실되는 경우에도 timeout 되어 재전송하게 된다.
![캡처](https://user-images.githubusercontent.com/17876424/118386995-79b0ba80-b656-11eb-9950-7d77b2a7698e.PNG)
+ 오류를 제어하는 방식은 크게 Stop and wait, Go-Back-N(GBN), Selective Repeat이 있다.

## 2) Sliding window
+ 앞서, 송신측, 수신측은 한번에 데이터를 보낼 수 있는 양을 window size로 나타냈으며 rcwd 값에 따라서 window 사이즈를 동적으로 변화시킨다고 했다.
+ 이런 window는 전체 보낼 데이터 byte가 있을 때 옆으로 sliding하면서 작동된다.
+ window에 들어온 데이터들은 한번에 전송 가능한 데이터이며 만약 window의 데이터 중 일부가 ACK 패킷을 받는다면 옆으로 sliding하여 새로운 데이터를 window 범위에 속하게 한다.
## 3) Stop and wait
+ Stop and wait는 송신측이 한번 데이터를 보내고 수신측으로부터 제대로 받았다는 ACK 패킷을 받을까지 기다리다가 다음 데이터를 보내는 방식
+ 만약, timer가 정한 시간 안에 ACK 패킷을 받지 못한다면 재전송한다.
+ 하지만 이 방식은 한번에 하나의 데이터만을 전송하기 때문에 Window size 고려가 필요없게 되며 Sliding window 사용이 필요없어진다.

## 4) Go-Back-N(GBN)
+ Window에 포함된 데이터를 연속적으로 전송하다가 그 중 에러가 발생한 데이터가 있다면 그 데이터 이후부터 다시 재전송하는 방법이다.
+ Window 당 하나의 timer가 설치되며 만약 timer가 설치된 데이터가 timeout 되기 전에 ACK 패킷을 받았다면 window에 포함된, 전송했는데 아직 ACK 패킷을 받지 못한 데이터 중 가장 오래된 데이터에 다시 timer를 설치하고 countdown을 다시 시작한다.
+ 수신측에서는 오직 expected byte number, 즉, in-order에 따라서 다음에 올 데이터 byte number만을 중요시한다.
+ 따라서, 만약, in-order대로 오지 않는다면 그 이후 데이터에 대해서는 전부 폐기처리한다.
+ ACK에 대해서는 in-order대로 정상적으로 온 데이터 중 가장 최근 데이터에 대한 ACK 패킷을 보낸다.
+ 따라서, 만약, in-order대로 오지 않는다면 그 이후는 무시하고 정상적으로 전송된 가장 최근 데이터 ACK 패킷을 중복 전송하게 된다.
+ 에러가 발생한 데이터 이후의 데이터는 제대로 전송했지만 수신측에서 전부 폐기하고 다시 오류가 발생한 데이터로 되돌아가 그 이후부터 전부 재전송하기 때문에 Go-Back-N이라고 부른다.

## 5) Selective Repeat
+ Go-Back-N에서 에러가 발생하면 전부 폐기하고 재전송하기에 이런 비효율성을 해결하기 위해서 나온 방식
+ Selective Repeat이라는 이름에서 알 수 있듯이 에러난 데이터에 대해서만 재전송하는 방식이다.
+ 만약, in-order대로 오지 않았다면 수신측에서는 그 이후 데이터를 전부 buffering한다.
+ ACK 패킷도 일단 에러난 데이터에 대해 무시하고 맞는 ACK 패킷을 전송한다.
+ Go-Back-N에서는 Window당 하나의 timer를 설치했지만 Selective Repeat에서는 모든 데이터에 대해서 개별적인 timer를 가지고 있다.
+ 에러난 데이터에 대해서는 ACK 패킷을 받지 못하므로 timeout되며 이에 대해서만 재전송하게 된다.
+ 재전송되어 수신측이 에러난 데이터에 대해 제대로 받게 되면 다시 받은 데이터부터 buffering되어 있는 데이터들을 재정렬하여 상위 계층에 전송하게 된다.
+ 즉, Go-Back-N에서의 불필요한 재전송이 사라졌지만 재정렬이라는 과정이 추가되었다.

[참고 자료: Computer Networking: A Top-Down Approach 7th edition]
