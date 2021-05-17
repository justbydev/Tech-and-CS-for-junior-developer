# 2. Activity
## 1) Activity란
+ Activity는 안드로이드 4대 컴포넌트 중 하나
+ Activity는 앱을 사용하는 사용자에게 UI가 있는 화면을 제공해주는 앱 컴포넌트
+ Activity는 앱이 사용자와 상호소통을 할 수 있게 해주는 역할
+ 주로 AppCompatActivity를 extend 하는데 하위 버전의 안드로이드를 지원하기 위해서 사용
+ Activity는 각자의 생명 주기를 가지고 있다.
+ 여러 Activity가 호출되면 back-stack에 stack과 마찬가지로 LIFO기반으로 다루어진다.

## 2) Activity 생명주기
![캡처](https://user-images.githubusercontent.com/17876424/118461280-7b52af00-b738-11eb-977f-b3f60e2b0c2b.PNG)
onCreate()->onStart()->onResume()->onPause()->onStop()->onDestroy()

## 3) Activity 생명주기 설명
1. onCreate()
+ 처음 Activity가 처음 생성될 때 호출되는 함수
+ 최초로 한번 실행
+ setContentView()를 실행하게 되며 View들을 그리고 inflate하는 단계

2. onStart()
+ Activity가 사용자에게 보여지기 직전에 호출
+ 사용자에게 보여주기 위한 Activity의 resource 설정

3. onResume()
+ 사용자에게 보여지지만 상호작용하기 직전에 호출
+ Activity의 모든 준비를 마치고 back-stack의 최상위에 위치하게 될때 호출

4. onPause()
+ Activity가 사용자로부터 부분적으로 가려지기 시작할 때 호출
+ Activity가 foreground에 있지 않게 된다는 것을 처음 알리기 위한 역할
+ 아직 소멸되지 않은 상태

5. onStop()
+ Activity가 완전히 가려져 사용자에게 보여지지 않았을 때 호출
+ 아직 소멸되지 않은 상태

6. onRestart()
+ back-stack에 남아있지만 onStop()되어 foreground에 있지 않은 Activity를 다시 foreground가 되어 사용자에게 보여져야 할 때 호출
+ onRestart() 되면 onStart()->onResume()이 다시 이루어짐

7. onDestroy()
+ Activity가 완전히 소멸된 상태
+ 더이상 back-stack에 존재하지 않는 상태

## 4) onSavedInstanceState() & onRestoreInstanceState()
화면 전환, 메모리 부족, 백버튼으로 이한 종료, 언어 설정 변경 등 Activity가 완전 종료(강제 종료) 되었을 때 기존 데이터나 상태를 유지 및 복구하기 위해서 사용하는 method
1. onSavedInstanceState()
+ onSavedInstanceState()는 Activity가 완전히 종류된 이후 다시 호출될 때 필요한 복구 데이터나 이전 상태를 저장하기 위한 method
+ Bundle을 통해서 저장하며 onStop() 이후에 호출
+ 직접 override 해서 사용
2. onRestoreInstanceState()
+ 완전히 종류되기 전에 Bundle을 통해서 저장했던 데이터들을 다시 복구하기 위해서 사용
+ onStart() 이후에 호출
+ 직접 override 해서 사용

## 5) 상황에 따른 Activity 생명주기
1. 앱 새롭게 실행, 새로운 Activity 실행
onCreate()->onStart()->onResume()
2. 화면 회전
onPause()->onStop()->onSavedInstanceState()->onDestroy()->onCreate()->onStart()->onRestoreInstaceState()->onResume()
3. 홈 버튼
onPause()->onStop()->onSavedInstanceState()
4. 앱 종료
onPause()->onStop()->onDestroy()
5. 새로운 화면으로(Act1->Act2)
onPause(Act1)->onCreate(Act2)->onStart(Act2)->onResume(Act2)->onStop(Act1)<br>->onSavedInstanceState(Act1)
6. 뒤로 가기 버튼(Act2->Act1)<br>
onPause(Act2)->onRestart(Act1)->onStart(Act1)->onResume(Act1)->onStop(Act2)->onDestroy(Act2)
