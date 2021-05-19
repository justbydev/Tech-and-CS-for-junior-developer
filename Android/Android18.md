# 18. Thread/Handler/Loop
## 1) Thread란
+ Process가 메모리에 적재된, 실행중인 프로그램이라면 Thread란 독립된 하나의 코드 실행 흐름을 말한다.
+ 하나의 Process는 여러 개이 Thread로 구성될 수 있다.
+ 안드로이드에서는 Main Thread(UI Thread)가 기본적으로 있으며 새롭게 생성해서 사용하는 Worker Thread가 있다.

## 2) Handler와 Loop
+ Handler와 Loop를 설명하기 위해 일반적인 시스템 관점으로 기술한다.
+ 참고로 안드로이드에서는 Main Thread가 생성되면 기본적으로 Looper, Message Queue가 있다.
+ Worker Thread가 다른 Thread로부터 이벤트나 메시지를 받기 위해서는 Looper를 생성해야 한다.
1. 사용자로부터, 혹은 다른 Process, Thread로부터 어떤 이벤트가 발생한다.
2. 시스템 혹은 운영체제가 이벤트를 인식하고 이벤트의 내용이 담긴 Event Message가 Message Queue에 들어간다.
3. 응용 프로그램이 이벤트가 발생하여 Event Message가 들어올 때까지 무한정으로 대기할 수 없기 때문에 Loop를 실행한다.
4. Loop는 Message Queue에 Message가 들어왔는지 주기적으로 체크한다.
5. 만약 Message Queue에 Message가 들어오면 이 Mesage를 처리해야 하는데 이를 적절히 처리하고 분석해주는 역할을 하는 것이 Handler이다.
6. Handler가 Message를 확인하여 미리 등록되어 있는 Callback function 중에서 Message 내용을 처리할 수 있는 Callback function을 처리하게 된다.
+ 위와 같은 과정이 이루어지게 된다.
+ 안드로이드에서는 Handler가 Message를 처리하게 된다.
+ 안드로이드에서는 Handler, Looper를 생성하여 사용할 수 있다.
+ Handler, Looper, Message, MessageQueue 모두 android.os 패키지 안에 있다.

## 3) Thread 생성 방법
+ Thread 생성 방법은 크게 두가지다.
1. Thread 객체 사용
```
class NewThread extends Thread{
      @Override
      public void run(){
      
      }
}
```
```
NewThread thread=new NewThread();
thread.start();
```
2. Runnable 인터페이스 사용
```
class NewRunnable implements Runnable{
      @Override
      public void run(){
      
      }
}
```
```
NewRunnable runnable=new NewRunnable;
Thread thread=new Thread(runnable);
thread.start();
```

## 4) Handler 사용
+ 위에서 Thread를 생성했지만 이 Thread는 Worker Thread이기 때문에 직접 UI 업데이트를 할 수 없다.
+ 따라서 Handler를 사용한다.
+ Handler에게 Message를 보내서 Message Queue에 넣고 Loop가 Message를 해석함으로써 실행하거나 Runnable 인터페이스와 Handler.post()를 사용한다.
+ 또한, Main Thread와 Worker Thread 뿐 아니라 Thread 간의 통신에서도 사용하며 위에서 설명한 매커니즘을 사용한다.
1. Message 객체 사용
+ 수신 측 Thread에서 Handler를 생성한다.(때로는 수신 측 Thread에서 송신 측 Thread를 생성하기도 한다.)
+ 송신 측 Thread에서는 수신 측에서 생성한 Handler를 사용한다.
+ 수신 측 Thread에서 생성한 Handler로부터 obtainMessage()를 통해서 Message 객체를 만든다.
+ Message에서 수신측으로 보낼 내용을 담는다.
+ 이후 sendMesage(Message 객체)를 통해서 Message를 전송하면 Message Queue에 담기게 된다.
+ 이를 Looper가 확인하게 되고 Message가 온 것을 알면 Handler에게 알린다.
+ Handler의 handleMessage(Message)에 전달되고 Message를 처리하게 된다.
```
//수신 측 Thread
Handler handler=new Handler(){
    @Override
    public void handleMessage(Message msg){
    //Message 처리
    }
}
```
```
//송신 측 Threaad
Message message=handler.obtainMessage();
//message에 원하는 내용 담기
handler.sendMessage(message);
```
2. Handler.post() 사용
+ 위의 Message 사용의 경우 매번 Mesage 내용을 담고 다시 받아서 해석해야 하는 번거로움이 있다.
+ 이때 Handler.post()와 Runnable 인터페이스를 사용한다.
+ Runnable 인터페이스에는 run() method만 존재하는데 이는 실행 코드 작성을 위한 것이다.(Thread 생성을 위한 것이라고 착각하면 안된다.)
+ 수신 측 Thread에서 Handler를 생성한다.
+ 송신 측 Thread에서 Runnable 인터페이스를 생성하고 run() method에 실행 코드를 작성한다.
+ 실행 코드에서는 UI 업데이트도 가능하다.
+ 수신 측 Thread에서 만든 handler를 이용하여 handler.post(송신 측에서 만든 Runnable)를 실행한다.
+ 이후, 실행 코드가 담긴 Mesasge가 Message Queue에 들어가고 Looper가 확인하여 Handler에게 전달한다.
+ Handler는 Runnable에 담긴 실행 코드를 실행한다.
```
//수신 측 Thread
Handler handler=new Handler();
```
```
//송신 측 Thread
Runnable runnable=new Runnable(){
    @Override
    public void run(){
    //실행 코드 작성
    }
}
handler.post(runnable);
```

## 5) Looper 사용
+ Handler는 사실 Looper에 의존적으로 Looper가 MessageQueue에 Message가 왔다느 것을 알려줘야 Handler가 처리한다.
+ Main Thread는 Looper를 기본적으로 가지고 있지만 Worker Thread는 그렇지 않다.
+ 하나의 Looper는 하나의 Thread만을 담당하기 떄문에 Worker Thread가 Message를 받기 위해서는 Looper를 생성해 줘야 한다.
+ Looper 사용을 위해서는 Handler 생성 전에 Looper를 생성해야 한다.
+ 또는 Looper를 기본적으로 가지고 있는 HandlerThread를 사용할 수도 있다.
1. Looper 생성
```
class NewThread extends Thread{//Message 받을 WorkerThread
    Handler handler;
    @Override
    public void run(){
      Looper.prepare();
      handler=new Handler(){
        @Override
        public void handleMessage(Message msg){
        
        }
      };
      Looper.loop();
  }
  ```
2. HandlerThread 생성
```
//이 코드는 송신 측 Thread에서 작성된 것
//수신 측 Thread는 HandlerThread
HandlerThread thread=new HandlerThread("name");
thread.start();

Handler handler=new Handler(thread.getLooper());
//이 handler는 HandlerThread의 handler

handler.post(new Runnable(){
    @Override
    public void run(){
    //수신 측으로 전송될 실행 코드 작성
    }
}
//결국 위의 Handler에서 보았듯이 수신 측의 Handler를 만들고
//수신 측의 Handler를 송신 측 Thread에서 사용하여 Hander.post(Runnable)를 한 것
```


