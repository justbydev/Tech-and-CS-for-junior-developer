# 19. BroadCastReceiver
## 1) BroadCastReceiver란
+ 안드로이드의 4대 컴포넌트 중 하나
+ 시스템으로부터, 혹은 다른 앱으로부터 메시지를 받거나 보낼 수 있는 기능을 하는 컴포넌트
+ 충전기 연결 여부, SMS 문자 여부, 사용 언어 변경 등에 대한 메시지
+ 즉, 어떤 이벤트가 발생했을 때 안드로이드 시스템에서 인지하고 receiver가 등록된 앱에 알리는 것
+ 정적 Receiver와 동적 Receiver로 분류

## 2) 정적 Receiver
+ 한번 등록하면 해제할 수 없다.
+ Manifest에 receiver를 등록하는 방법으로 정적 Receiver를 등록할 수 있다.
+ 앱이 설치되면 자동으로 등록된다.
+ 정적 Receiver를 사용하면 앱이 실행중이지 않은 상태에서도 메시지를 받을 수 있다.
+ 앱이 실행중이지 않아도 작동을 해서 시스템에 overhead가 발생할 수 있어서 오레오(API 26) 이상부터는 예외들을 빼고는 정적 Receiver를 사용하지 못하도록 제한하게 되었다.
1. 정적 Receiver 등록
```
<receiver
    android:name=".broadcastreceiver.TestReceiver"
    android:enabled="true"
    android:exported="true">
        <intent-filter>  
                <action android:name="android.intent.action.ACTION_POWER_CONNECTED"/>
        </intent-filter>
</receiver>
```
2. TestReceiver class
```
public class TestReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        String action = intent.getAction();
        Toast.makeText(context, "받은 Action-> ", Toast.LENGTH_SHORT).show();
    }
}
```
+ onReceive에서 Receiver를 받게 된다.
3. Receiver 전송하기
```
Intent intent=new Intent(Intent.ACTION_POWER_CONNECTED);
sendBroadcast(intent);
```

## 3) 동적 Receiver
+ Activity가 create되어서 등록될 때만 가능하다
+ 즉, Activity의 context가 유효할 때만 가능하며 Destroy되면 Receiver도 같이 소멸된다.
+ Manifest에 등록할 때 intent filter를 사용한 것처럼 Receiver를 등록하기 위해서는 IntentFilter를 사용한다.
1. 동적 Receiver 등록
```
@Override
protected void onResume() {
    super.onResume();
    //BroadCastReceiver 에 Action 등록
    testReceiver = new TestReceiver();
    IntentFilter intentFilter = new IntentFilter();
    intentFilter.addAction(Intent.ACTION_POWER_CONNECTED);
    intentFilter.addAction(Intent.ACTION_POWER_DISCONNECTED);
    Context.registerReceiver(intentReceiver,intentFilter);
}
```
+ 위와 같이 register하면 TestReceiver의 onReceive에서 수신받습니다.

2. 동적 Receiver 해제
```
@Override
protected void onStop() {
    super.onStop();
    unregisterReceiver(testReceiver);
}
```

참고자료<br>
https://limkydev.tistory.com/49
