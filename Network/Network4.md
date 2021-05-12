# 4. ISO/OSI 7계층 모델
## 1) 계층을 나눈 이유
+ 계층(layer)마다 역할을 지정하여 modularization을 실행
+ 한 계층의 변화나 이상이 다른 계층에 영향을 주지않는 transparent 가능
+ 유지 보수에도 유용

## 2) 구성
### Physical-Link-Network-Transport-Session-Presentation-Application

## 3) Internet protocol layer
### Physical-Link-Network-Transport-Application

## 4) Physical
+ 오직 bit가 전송되는 물리적 역할을 하는 layer
+ 허브, 케이블, 리피터 등
+ Bit 단위

## 5) Link
+ Mac address를 통해서 통신
+ Physical layer와의 안전한 데이터 송수신 담당
+ 브릿지, 스위치
+ Frame 단위

## 6) Network
+ Routing과 Forwarding이 이루어지는 곳
+ IP, Routing protocol
+ 라우터
+ Datagram 단위

## 7) Transport
+ Process와 Process 사이의 통신이 이루어지도록 하는 곳
+ Process마다 socket이 있고 socket을 통해서 통신하기 위해 필요한 요소 중 Port number를 할당하는 곳
+ TCP, UDP
+ Segment 단위

## 8) Application
+ 여러가지 응용 process과 직접 연결되어 있는 layer
+ Application layer를 통해 여러 서비스를 제공받음
+ HTTP, SMTP, FTP, DNS
+ Message 단위

[참고 자료: Computer Networking: A Top-Down Approach 7th edition]
