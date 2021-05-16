# 12. Flow control(흐름 제어)
## 1) Flow control이란
+ 송신측과 수신측 사이의 데이터 처리 속도를 조절하여 송신측이 전송하는 데이터량이 수신측이 받을 수 있는 데이터량을 넘지 않도록 하는 조절
+ Window size(윈도우 크기)라는 말을 사용하는데 이는 수신 측이 자신이 처리할 수 있는 데이터의 양을 의미한다.
+ Window는 결국 데이터가 보관될 수 있는 buffer를 의미한다.
+ 수신측에서 설정한 window size만큼 송신측이 전송할 수 있는 데이터량을 동적으로 조절하며 송신측 window size는 수신측과 동일하다.

## 2) Flow control 방법
+ 수신측은 송신측으로부터 데이터를 제대로 받았음과 다음 기대하는 byte number를 알리기 위해서 ACK 패킷을 전송한다.
+ 이때, 수신측은 현재 자신이 받을 수 있는 buffer size, 즉, rwnd(receive window size)를 header에 담아 송신측에 전송한다.
+ 송신측은 rwnd 값을 이용하여 flow control을 한다.

[참고 자료: Computer Networking: A Top-Down Approach 7th edition]
