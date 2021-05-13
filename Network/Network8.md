# 8. SMTP
## 1) SMTP introduction
+ Simple Mail Transfer Protocol의 약자
+ 인터넷 상의 메일을 주고 받기 위한 통신 규약
+ Application layer의 protocol 중 하나로써 TCP를 사용하고 포트 번호는 25

## 2) 전자 메일의 구성
+ 전자 메일은 user agent, mail server, SMTP로 구성되어 있다.
+ user agent는 실제 전자 메일을 전송하고 받는 대상
+ mail server는 user agent가 전송한 mail이 저장되고 그 mail을 다시 목표 user agent에게 보내는 역할을 한다.
+ mail server는 mailbox와 message queue로 구성되어 있다.
+ mailbox는 user에게 전송될 mail이 저장되는 곳이고 message queue는 다른 mail server에게 전송될 mail이 저장되는 곳
+ SMTP는 mailbox와 mailbox 사이, mail을 전송한 user agent와 mailbox 사이에서 사용

## 3) 전자 메일 전송 과정(A에서 B로 전송)
1. A 라는 user agent가 메일을 SMTP를 사용하여 mail server로 전송한다.
2. 메일은 A의 mail server의 message queue로 들어간다.
3. A mail server의 message queue의 메일은 SMTP를 사용하여 B의 mail server의 mailbox로 전송된다.
4. B의 mail server는 B라는 user agent에게 메일이 왔다고 알린다.
5. B user agent는 Mail Access Protocol(POP, IMAP 등)를 사용하여 mailbox로부터 메일을 꺼낸다.

## 4) HTTP와 SMTP의 공통점
1. 둘다 Application Layer의 protocol이자 TCP 를 사용한다.
2. Request(commands)는 ASCII text로 구성
3. Response는 status code와 phrase로 구성

## 5) HTTP와 SMTP의 차이점
1. HTTP는 pull protocol(웹 서버의 object를 꺼내온다)이고 SMPT는 push protocol(메일 서버에 집어넣는다)
2. 참고로 Mail Access Protocol은 pull protocol
3. SMTP message는 반드시 7 bit ASCII 이내로 구성
4. HTTP는 각각의 object가 각각의 response message에 담겨져 있고 SMTP는 여러 형태의 object가 함께 multipart message에 담긴다.(HTTP는 하나의 message에 하나의 object, SMTP는 하나의 message에 여러 object)

[참고 자료: Computer Networking: A Top-Down Approach 7th edition]
