# 11. Context
## 1) Context란
+ 안드로이드 개발을 하다보면 Context를 많이 사용한다.(Toast, Intent, SharedReference 등 상당히 많은 곳)
+ Context는 어플리케이션이나 어플리케이션 컴포넌트와 관련된 다양한 정보를 담고있는 인터페이스를 말한다.
+ 어떤 Activity, application인지 구별할 수 있는 정보가 Context

## 2) Context 역할
+ 안드로이드에서 어플리케이션 정보를 관리하는 것은 시스템이 아닌 ActivityManagerService라는 일종의 또다른 어플리케이션
+ 어플리케이션 정보를 얻기 위해서는 ActivityManagerService에 접근해야 하며 이는 Context를 통해 가능하다
+ Context는 어플리케이션, Activity와 관련된 정보에 접근하거나 시스템 레벨의 함수 호출시 사용
+ Context가 있어야 각종 컴포넌트(Activity, Service, BroadCast)를 발생시킬수도 있고 resource 접근도 가능

## 3) Context 생성
+ Context는 기본적으로 어플리케이션이 생성되면 생성된다
+ 또한, 어플리케이션의 컴포넌트가 생성될 때도 각각 생성된다

## 4) Context 종류
+ Context 종류는 ApplicationContext, ActivityContext가 있다.
+ ApplicationContext는 Application 생명 주기와 관련되어 있다.
+ ActivityContext는 Activity 생명 주기와 관련되어 있어 Activity가 소멸되면 Context도 소멸된다.
+ Activity는 Context를 상속받기 때문에 this를 통해서 ActivityContext를 얻을 수 있다.
+ Application도 Context를 상속받는다.

## 5) 참조
+ https://shnoble.tistory.com/57
+ https://devwooks.tistory.com/13
