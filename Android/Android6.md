# 6. PendingIntent
## 1) PendingIntent란
+ PendingIntent는 바로 행동하거나 직접 행동하지 않고 다른 컴포넌트에게 위임처리를 하는 기능
+ 당장 해당 작업을 다른 컴포넌트에게 요청하는 것이 아니라 특정 시점에 자신이 아닌 다른 컴포넌트에게 해당 작업을 요청하는 것
+ 대표적으로 Notification을 클릭하거나 위젯 클릭시 작업이 수행되도록 하기 위해 PendingIntent를 사용한다.
+ getActivity, getBroadcast, getService 를 통해서 후행 작업을 표시
## 2) 예시
```
Intent intent=new Intent(Now.this, Next.class)
PendingIntent pendingIntent=PendingIntent.getActivity(this, 0, intent, PendingIntent.FLAG);
~
~
~
new NotificationCompat.Builder().setContentIntent(pendingIntent)
```
+ 위와 같이 하면 Notification을 클릭하게 되면 pendingIntent가 실행되는데 getActivity를 통해 담은 intent가 실행된다.
