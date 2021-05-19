# 17. Manifest file
## 1) Manifest file이란
+ 어플리케이션에 관한 정보를 입력하는 xml 형태 파일
+ 별도의 설정을 하지 않는다면 src/main에 위치해야 한다.
+ 패키지 이름, 앱 이름, 앱 설명, 아이콘, 컴포넌트, 권한, 앱에 필요한 하드웨어, 소프트웨어 특징 기술

## 2) 앱 정보
+ 기본적으로 상위에 기술한다.
+ 패키지 이름, 앱 이름, 아이콘 등을 기술
```
<application>
```
  
## 3) 컴포넌트
+ 4대 컴포넌트를 지정하고 앱 실행시 가장 먼저 실행되는 LAUNCHER도 표시한다.
```
<activity>: Activity
<service>: Service
<provider>: Content Provider
<receiver>: Broadcast Receiver
```

## 4) 권한
+ 여러가지 권한 역시 기술
```
<uses-permission android:name="android.permission.CAMERA" />
```
+ 위의 예시는 카메라 권한 설정

## 5) 앱에 필요한 하드웨어, 소프트웨어 특징 기술
+ 앱을 다운로드 받을 때 기기에 해당 하드위어나 소프트웨어가 있어야 한다는 것을 기술
```
<uses-feature android:name="android.hardware.camera2" android:required="true"/>
```
+ 위의 예시는 카메라 앱 필수를 표시
