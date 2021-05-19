# 16. FCM(Firebase Cloud Messaging)
## 1) FCM이란
+ FCM이란 Firebase에서 제공해주는, 무료로 메시지를 전송할 수 있는 교차 플랫폼 메시징 솔루션
+ 한명부터 다수, 그룹으로 알림 메시지를 전송할 수 있으며 무료로 사용 가능
+ 어플리케이션은 기존 서버가 존재하는데 이 서버에서 알림 메시지 기능까지 수행하면 상당히 복잡해지는데 이를 다른 서버가 제공해 줄수 있도록 만든 것이 FCM
+ 어플리케이션(client)-FCM 서버(구글 클라우드 서버)-어플리케이션 본 서버 형태로 이루어진다.
+ 또한, 만약 FCM 서버를 사용하지 않고 어플리케이션 서버를 사용해 알림 메시지를 보낸다면 계속 서버에 접속해 있어야 한다.
+ 따라서 FCM 서버를 사용한다면 이런 문제를 해결해 줄 수 있다.
+ 알림 메시지를 전송할 대상은 FCM token을 통해서 구분하여 보내게 된다.
+ 알림 메시지의 경우 앱이 종료되거나 백그라운드에 있어서 받을 수 있어야 하기 때문에 Service를 이용한다.

## 2) FCM method
1. getToken()
+ 앱이 최초로 실행될 때(최초로 다운로드되어 설치된 경우) FCM을 위한 device token이 생성된다
+ 이 token은 생성되면 구글 클라우드 서버에 자동으로 저장된다.
+ 현재 토큰을 가져오려면 다음을 사용한다.
```
FirebaseInstanceId().getInstnace().getToken()
```
+ 만약 새롭게 생성된 device token을 어플리케이션 서버에 저장하고 싶다면 새 토큰이 생성될 때 onNewToken()이 호출되기 때문에 이를 재정의한다.

2. onMessageReceived()
+ 알림 메시지를 받았을 때 호출되는 콜백 메소드
+ 받은 메시지는 기본 지정된 형식을 사용한 메시지라면 getNotification()을, custom이라면 getData()를 통해서 알림 메시지 내의 내용을 받을 수 있다.
+ 본인은 이렇게 받은 알림 메시지를 Notification, PendingIntent와 함께 사용했다.

3. 알림 메시지 보내기
+ 내가 보내고자 하는 대상의 device token을 알아야 한다.
+ FCM도 결국 구글 클라우드 서버, 즉, 서버와의 통신이기에 HTTP 통신을 진행한다.
+ 따라서 본인은 Retrofit2을 사용했으며 FCM에 해당 어플리케이션 등록 시 받은 Authorization key, content-type을 Headers에 포함시켜 진행한다.
```
@Headers({"Authorization: key=" + "AAAAz....Sh_1U", "Content-Type:application/json"})
@POST()
CALL<>()
```
