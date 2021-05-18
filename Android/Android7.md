# 7. inflate
## 1) inflate란
+ inflate라는 것은 ViewGroup, View들을 메모리에 적재하여 객체화시키는 작업을 의미
+ 모든 View들을 각각 객체화시키고 트리구조를 형성하여 메모리에 적재해야 사용자와 상호작용이 가능
+ 기본적으로 Activity의 onCreate()에서 setContentView()를 통해서 Activity를 구성하는 View들을 inflate한다.
+ 사용해본 inflate는 Activity.getLayoutInflater(), context.getSystemService(LAYOUT_INFLATER_SERVICE), LayoutInflater.from(context), View.inflate()다.
+setContentView()가 아니라면 모두 inflate된 RootView(최상위 부모 참조 변수)를 return 받는다.

## 2) Activity.getLayoutInflater()
+ Activity 상에서 inflate 할때 사용할 수 있는 방법
+ LayoutInflater를 얻고 이를 통해 inflate
```
LayoutInflater inflater=Activity.getLayoutInflater();
inflater.inflate(R.layout.resource, Container, attachtoRoot);
```

## 3) Context.getSystemService(LAYOUT_INFLATER_SERVICE)
+ Context를 얻었다면 이를 통해 systemservice를 이용한다.
+ LayoutInflater를 얻고 이를 통해 inflate
```
Context context=Activity.this;
LayoutInflater inflater=context.getSystemService(LAYOUT_INFLATER_SERVICE);
inflater.inflate(R.layout.resource, Container, attachtoRoot);
```

## 4) LayoutInflater.from(context)
+ Context를 얻고 이를 사용한다.
+ LayoutInflater를 얻고 이를 통해 inflate
+ LayoutInflater의 method인 from(Context)는 내부적으로 context.getSystemService(LAYOUT_INFLATER_SERVICE)를 호출한다.
```
Context context=Activity.this;
LayoutInflater inflater=LayoutInflater.from(context)
inflate.inflate(R.layout.resource, Container, attachtoRoot);
```

## 5) View.inflate()
+ LayoutInflater를 얻지 않고 View를 통해서 inflate한다.
+ View의 inflate method은 내부적으로 LayoutInflater.from(context)->context.getSystemService(LAYOUT_INFLATER_SERVICE)를 호출한다.
```
Context context=Activity.this;
View.inflate(context, R.layout.resource, Container, attachtoRoot);
```
