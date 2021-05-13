# 9. DNS(Domain Name System)
## 1) 도메인 이름과 IP 주소
+ 인터넷 상의 host(process)들은 그들을 구분해주는 식별자로 IP address를 사용(포트 번호도 함께 사용)
+ 사람들이 웹페이지에 접근할 때는 숫자가 아닌 www.페이지이름.com 이런식의 도메인 이름을 사용(URL은 그 웹페이지를 구성하는 각각의 object들을 자세하게 구분해주는 식별자, www.페이지이름.com/test.jpg)
+ 따라서, 사람이 사용하는 도메인 이름과 인터넷이 사용하는 IP address 사이의 mapping이 이루어져야 한다.

## 2) DNS(Domain Name System)
+ 위에서 언급했듯이 도메인 이름과 IP address 사이의 mapping이 필요한 mapping을 해주는 것이 바로 DNS, Domain Name System
+ DNS 역시 application layer protocol
+ DNS는 계층 구조를 가지고 있다.
+ Root DNS Server-com/org/co.kr/edu 등등의 DNS server-www.naver.com, www.daum.net, www.google.com 등의 DNS server의 계층 구조
+ 위의 계층 구조의 각 이름은 Root DNS Server-Top-level DNS server(TLD)-Authoritative DNS server
+ 또한, DNS에는 계층 구조에 들어가지 않고 각각의 host가 가지고 있는 Local DNS server가 있다.

## 3) Local DNS server
+ 어떤 웹페이지를 들어가든 먼저 Local DNS server에 접근하게 된다.
+ Local DNS server에는 도메인 이름-IP address mapping이 cache되어 있고 만약 cache되어 있지 않다면 Root DNS Server에게 요청하여 IP address를 받아오는 역할을 한다.

## 4) IP address 받아오는 과정
1. 사용자는 특정 웹페이지를 도메인 이름을 통하여 접속한다.
2. 그러면 host는 local DNS server에 접근하여 해당 웹페이지의 IP address가 cache되어 있는지 본다.
3. 만약 cache되어 있다면 IP address를 받아온다.
4. 만약 cache되어 있지 않다면 local DNS server는 Root DNS server에 접근한다.
5. 이때, iterated query 방식과 recursive query 방식 2가지가 있다.
6. a) iterated query 방식인 경우 local DNS server가 차례대로 Root DNS server, TLD server, authoritative DNS server에게 요청하여 IP address를 받아서 host에게 전달<br>b) recursive query 방식인 경우 Root DNS server에게 요청하면 Root DNS server가 TLD server에게 요청, 다시 TLD server가 authoritative server에게 요청하여 차례대로 response하여 최종 IP address를 Root DNS server가 local DNS server에게 전달
7. 최종적으로 cache되어 있다면 3번까지, 그렇지 않다면 4~6번 과정을 거쳐서 도메인 이름에 해당하는 IP address를 받아온다.
8. 이렇게 IP address를 받았다면 이를 바탕으로 TCP connection, HTTP request를 보내서 IP address에 해당하는 웹서버로부터 object들을 받아와서 웹페이지를 띄우게 된다.

[참고 자료: Computer Networking: A Top-Down Approach 7th edition]
