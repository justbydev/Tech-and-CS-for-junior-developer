# 3. Fragment
## 1) Fragment란
+ 안드로이드 앱은 기본적으로 Activity로 구성되어 있고 Activity를 통해 사용자에게 UI를 제공한다.
+ 그런데 하나의 창(Activity)를 여러 개의 서로 다른 것을 보여주는 여러 창을 보여주고 싶을 때가 있다.
+ 물론, View를 여러 개 하여 보여줄 수도 있지만 복잡한 경우도 있어 이럴 때 Fragment를 사용한다.
+ 즉, Fragment는 Activity 내에서 UI 구성을 여러 개의 모듈 단위로 이루어질 수 있도록 한다.

## 2) Fragment 특징
+ Fragment는 적어도 반드시 하나의 Activity와 결합되어야 한다.
+ Fragment는 Activity와는 별개의 생명 주기를 가지고 있다.
+ 별개의 생명주기를 가지고 있지만 Activity와 반드시 결합되어 사용되기 때문에 Activity의 생명주기에 직접적인 영향을 받는다.
+ Fragment가 결합되어 있는 Activity가 일시정지되면 Fragment도 전부 일시정지되며 소멸되면 같이 소멸된다.
+ Activity와 같이 addToBackStack(null)을 통해서 back-stack에 넣을 수 있다.

## 3) Fragment 생명주기
![캡처](https://user-images.githubusercontent.com/17876424/118468260-8ceb8500-b73f-11eb-9756-121827a2cb76.PNG)

onAttach()->onCreate()->onCreateView()->onActivityCreated()->onStart()->onResume()->onPause()->onStop()->onDestroyView()->onDestroy()->onDetach()

## 4) Fragment 생명주기 역할
1. onAttach()
+ Fragment가 Activity에 붙을 때 호출
+ 아직 완전하게 생성된 것은 아님
2. onCreate()
+ Fragment가 Activity의 호출을 받아 생성되기 시작하는 시점
+ Activity에서는 onCreate()에서 UI 작업, view inflate 등의 작업을 했지만 Fragment는 할 수 없다.

3. onCreateView()
+ UI 작업, view inflate 작업을 하는 시점

4. onActivityCreated()
+ Activity에서 Fragment를 모두 생성한 후 호출
+ Activity와 Fragment가 완전히 연결되는 시점

5. onStart()
+ Activity와 마찬가지로 사용자에게 보여지기 직전에 호출

6. onResume()
+ Activity와 마찬가지로 사용자에게 보여지고 상호작용이 되기 직전에 호출

7. onPause()
+ Activity와 마찬가지로 일부 가려져 보이지 않게 되는 시점
+ 해당 Fragment의 부모 Activity가 아닌 다른 Activity가 foreground로 나오게 될 때 호출되는 것

8. onStop()
+ Activity와 마찬가지로 완전히 가려져 더 이상 보이지 않게 되는 시점

9. onDestroyView()
+ Fragment의 view들을 제거하는 시점
+ 만약 back-stack을 사용했다면 해당 Fragment로 돌아올때 onCreateView()가 호출
+ 2개 이상의 fragment를 add한 후 replace되면 기존 fragment를 onDetach()까지 끝낸 다음 새로운 Fragment를 올린다
+ 하지만 add할 때 backstack에 넣는다면 onDetach()까지 가지 않고 onDestroyView()까지만 처리된다

10. onDestroy()
+ 완전하게 Fragment가 제거하기 직전

11. onDetach()
+ 완전하게 Fragment 제거
+ Activity와의 연결도 해제

## 5) Fragment 연결 방법
+ Fragment를 연결할 Activity에서 FragmentManager를 통해서 Fragment가 관리
+ getSupportFragmentManager()를 통해서 FragmentManager 얻을 수 있다.
+ Fragment에 대한 add, replace, hide, show 등의 transaction을 FragmentManager.beginTransaction()을 통해서 추가할 수 있다.
+ 마지막에 transaction을 commit()함으로써 작동
+ 또는 xml 파일 상에서 <fragment>를 추가할 수도 있으며 name에 추가할 Fragment의 위치를 나타낸다
