# 4. Main Thread vs Worker Thread
## 1) Main Thread
+ 어플리케이션은 적어도 1개의 Thread를 가지고 있어야 하는데 그것이 바로 Main Thread
+ Main Thread에서는 UI 컴포넌트(View들)을 그리는 작업이 이루어지기 때문에 UI Thread라고도 부른다.(UI와 동기화/연동)
+ 프로그램이 실행되면 Process가 실행되고 이 Process는 적어도 하나의 Thread를 가져야 하는데 이것이 Main Thread
+ Process가 처음 실행될 떄 최초 시작점이 main()인데 "android.app.ActivityThread"에 main()이 구현되어 있으며 여기서 Main Thread가 실행된다.
+ 이후, Main Thread가 실행되면 "AndroidManifest.xml"의 Launcher로 지정되어 있는 Activity를 찾아서 실행하게 된다.
+ Main Thread는 자신만의 Looper, MessageQueue를 가지고 있다.

## 2) Main Thread에서 반드시 동작해야하는 함수
1. 생명주기와 관련된 method
2. 시스템 콜백 method(콜백 method는 어떤 이벤트가 발생했을 때 이미 지정되어 저장되어 호출되는 method)

## 3) ANR(Application Not Responding)
+ ANR은 Application Not Responding으로써 어플리케이션에 응답이 없어 강제 종료하는 경우 ANR이 호출된다.
+ 보통 Main Thread가 일정 시간동안 어떤 Task에 잡혀 다른 작업을 못할 때 발생
+ Main Thread에서는 여러 UI에 대한 작업을 하고 생명주기 관련 작업, 시스템 콜백 관련 작업 등 중요한 작업을 하기 때문에 ANR 발동
+ 5초 이내에 터치 이벤트에 대해서 UI 응답이 없거나 Broadcast Receiver의 onReceive()가 10초 내에 리턴되지 않을 때 ANR 발동

## 4) ANR 회피 방법
+ 시간이 많이 걸리는 작업의 경우 Main Thread가 아닌 Worker Thread에서 작업
+ AsyncTask를 이용하여 작업하고 실시간으로 UI 업데이트

## 5) Worker Thread
+ ANR 회피 방법에서도 나왔듯이 Main Thread이외의 Thread를 Worker Thread라고 한다.
+ 보통 Thread 객체나 Runnable 객체를 이용하여 생성한다.
+ Worker Thread에서는 직접 UI에 접근할 수 없다.
+ Worker Thread의 작업 결과로 UI를 업데이트 하기 위해서는 Handler를 통해서 전달(Message), Handler.post 통한 Runnable 전달,  AsyncTask 이용 등의 방법이 있다.
+ Worker Thread에는 Looper가 없기 때문에 만약 메시지를 받기 위해서는 Looper를 생성해야 한다.
