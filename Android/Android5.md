# 5. Intent & Bundle
## 1) Intent란
+ 비동기식 메시지 객체
+ 4대 컴포넌트 간의 작업 수행을 위한 정보를 전달하는 역할
+ 대표적으로 startActivity(), startService(), bindService(), broadcastIntent() 등이 있다.
+ Intent는 명시적 intent와 암시적 intent가 있다.

## 2) 명시적 intent
+ 전달한 목표가 명확한 intent로써 정보를 전달하는 대상을 명확히 지정할 때 사용
+ 실행하고자 하는 컴포넌트가 명확할 때 사용하는 방식
+ 가장 대표적인 예시가 Activity
```
Intent intent=new Intent(Now.this, Next.class);
startActivity(intent);
```
+ 위와 같이 컴포넌트를 명확하게 명시한다.

## 3) startActivity vs startActivityForResult
+ startActivity는 단순히 다른 Activity로 정보를 전달하고 새롭게 시작하는 역할
+ startActivityForResult는 호출하는 Activity에게 정보를 전달할 뿐 아니라 호출한 Activity로부터 return 값을 받는 것
+ return 값은 onActivityResult로 들어오게 된다.
+ onActivityResult에서는 requestCode, resultCode, data(Intent)를 통해서 이루어진다.

## 4) 암시적 intent
+ 특정 컴포넌트를 지정하는 것이 아니라 어떠한 작업을 수행할 것인지만 선언
+ 암시적 intent는 보통 Action과 Data라는 속성으로 구성
```
Intent intent=new Intent(Intent.ACTION_PICK)
startActivity(intent)
```
```
Intent intent=new Intent(Intent.ACTION_VIEW, Uri.parse("tel:010-0000-1111"));
startActivity(intent)
```

## 5) Bundle
+ Bundle은 여러가지 타입의 데이터를 저장하는 Map 클래스(key-value)
+ Intent에도 putExtra(key, value)를 통해서 데이터를 담을 수 있지만 정석적으로는 Bundle에 담는다.
+ Bundle이 데이터를 담는 택배라면 Intent는 이 택배를 전달하는 집배원의 역할을 하는 것이다.
```
//Sender
Intent intent=new Intent(Now.this, Next.class)
Bundle bundle=new Bundle();
bundle.putString("name", "test");
bundle.putInt("test", 123);
intent.putExtras("mybundle", bundle);
startActivity(intent);
```
```
//Receiver
Intent intent=getIntent();
Bundle bundle=intent.getExtras();
String name=bundle.getString("name");
int test=bundle.getInt("test");
```
+ 이렇게 Bundle에 넣어서 데이터를 전송하는 방법이 한번에 보내줘서 더 빠르다고 하기 때문에 이렇게 하는 것이 좋다.
