# 7. Cookies & Proxy server
# 1) Cookies
+ 어떤 웹페이지에 들어가면 쿠키 허용 이라는 것을 많이 볼 수 있는데 이때의 쿠키가 바로 Cookie다.
+ Cookies는 다음과 같은 4가지 component로 구성된다.
1. HTTP response message에 담기는 cookie header로써 처음 웹페이지에 들어온 사용자에게 cookie를 setting해서 보내는 것
2. HTTP request message에 담기는 cookie header로써 다시 방문한 사용자의 경우 이전에 setting된 cookie를 보내는 것
3. user의 브라우저에 의해 관리되는, host에 저장된 cookie file로써 setting된 cookie가 저장되어 있는 곳
4. 웹페이지의 back-end 데이터 베이스에 저장된 user의 cookie setting
+ 이런 4가지 component를 이용해서 cookie가 setting되어서 사용된다.
+ 요즘은 보안 문제로 인하여 사용자에게 직접 이메일과 이름을 입력받아 쿠키 허용 요청을 하여 쿠키를 저장하는 경우가 많다.

# 2) Proxy server(Web cache)
+ 웹페이지에 들어간다는 것은 웹브라우저가 웹서버로부터 여러가지 object들을 받아온다는 것을 뜻한다.
+ 또한, 여러 object들을 받아오기 위해서는 TCP connection이 이루어지고 HTTP 통신이 이루어져야 한다.
+ 하지만, 여러 번 방문했던 웹페이지에 대해서 똑같이 웹서버와 connection을 이루어 매번 object를 가지고 온다면 비효율적이다.
+ 따라서, 나온 것이 Proxy server(web cache)로써 이름에서 알 수 있듯이 방문했던 웹페이지의 object들이 cache되고 다시 방문했을 때 origin 웹서버에게 요청을 보내기 보다 먼저 proxy server와 HTTP 통신을 한다.

# 3) Proxy server 과정
1. 웹페이지에 방문하면 먼저 proxy server와 TCP connection을 형성한다.
2. Proxy server에게 HTTP request를 보낸다.
3. 만약, proxy server에 요청한 웹페이지에 해당하는 object들이 있다면 origin 웹 서버에게 HTTP request를 보내지 않고 바로 웹브라우저에게 HTTP response를 보내서 웹브라우저는 받은 object들을 사용하여 웹페이지를 띄운다.
4. 만약, proxy server에 존재하지 않는다면 proxy server는 origin 웹 서버에게 HTTP request를 보내서 필요한 object들을 받아서 cache후 그 결과를 HTTP response를 보낸다.

[참고 자료: Computer Networking: A Top-Down Approach 7th edition]
