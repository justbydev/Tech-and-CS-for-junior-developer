# 15. Service
## 1) Service란
+ 안드로이드 4개 컴포넌트 중 하나
+ 화면 없이 백그라운드에서 실행되는 단위를 Service라고 한다.
+ Service 추가시 AndroidManifest.xml에 "service"로 추가해 주어야 한다.
+ Service는 Activity가 종료되어도 계속 실행되며 앱이 종료되어도 백그라운드에서 계속 실행된다.
+ Service는 항상 실행되어 있을 수 있도록 비정상 종료되는 경우에도 시스템에 의해 자동으로 재시작한다.
+ Service도 생명주기를 가지고 있다.
+ Service는 Foreground, Background, Bind 의 세가지가 있다.

## 2) Service 생명주기
![캡처](https://user-images.githubusercontent.com/17876424/118761270-153c6800-b8af-11eb-87b8-0bbf6b1b6438.PNG)
1. onCreate()
+ 처음 Service를 생성할 때 호출
+ 이후, 한번 생성된 Service를 계속 사용할 때는 호출되지 않는다.
2. onStartCommand()
+ 한번 생성된 Service를 앱의 여러 컴포넌트에서 실행할 때 호출
+ intent를 통해 전달된 데이터를 받을 수 있는 곳
+ Service를 실행하면 onStartCommand()에서 백그라운드 작업을 실행
+ onStartCommand()는 3가지 return type을 가진다.
  + START_STICKY: 강제 종료되면 재시작하며 intent 값은 null로 초기화
  + START_NOT_STICKY: 강제 종료되면 재시작하지 않음
  + START_REDELIVER_INTENT: 강제 종료되면 재시작하며 intent 값 유지
3. onDestroy()
+ Service를 소멸할 때 호출
4. onBind()
+ BindService 사용시 호출

## 3) 세가지 Service
1. ForegroundService
+ 사용자에게 보이는 서비스를 제공하며 반드시 알람 표시를 해야 한다.
+ Oreo 버전 이후부터는 startForegroundService(Intent)를 통해서 시작
+ ForegroundService에서는 반드시 Notification을 통해 알람 표시를 하고 startForeground(ID, Notification builder)를 호출해야 한다.

2. BackgroundService
+ 사용자에게 보이지 않고 백그라운드에서 실행하는 service
+ startService(Intent)를 통해서 실행
+ Intent를 통해서 Activity에게 데이터를 전달할 수도 있다.

3. BindService
+ server-client 구조를 가져서 Activity와 통신을 주고 받는 service
+ service를 호출한 대상이 client가 되며 service가 서버가 되는 형태
+ service에게 어떤 작업을 요청하고 요청 처리 후 결과값을 반환하는 구조
+ 하나의 service에 여러 Activity가 binding 될 수 있다.
+ BindService의 경우 bind된 Activity가 종료되면 service도 자동으로 destroy되면서 소멸된다.

## 4) Thread와의 차이
+ Thread를 생성하는 경우 MainThread가 아닌 백그라운드에서 실행되는 WorkerThread
+ Service의 경우 MainThread에서 실행되는 것
