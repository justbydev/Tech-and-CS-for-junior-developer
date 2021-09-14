# 8. ContentProvider
## 1) ContentProvider란
+ 안드로이드 4대 컴포넌트 중 하나
+ 안드로이드 시스템에서 각각의 앱은 각각의 DB를 가지고 있는데 해당 앱의 DB는 해당 앱만 접근가능하다.
+ 따라서, 다른 앱의 DB에 접근할 수 있도록 제공해주는 역할이 바로 ContentProvider
+ 여기서 다른 앱이란 연락처, 갤러리, 음악 등 안드로이드가 가지고 있는 기본 앱도 포함된다.

## 2) ContentResolver
+ ContentProvider가 Provider를 제공하는 다른 앱의 DB에 접근하려 한다면 접근하여 그 결과를 받아 반환해주는 역할을 하는 것이 ContentResolver
+ ContentProvider가 접근하기 위해서는 ContentResolver를 사용해야 한다.
+ ContentResolver는 geContentResolver() 를 통해서 얻을 수 있다. 
+ ContentResolver는 SQL 기반으로 CRUD query를 제공한다.

## 3) URI
+ Uniform Resource Indicator로써 정형화된 여러 파일들의 식별자를 의미
+ ContentProvider가 DB에 접근하여 ContentResolver를 통해 받아올 때는 그 DB(여러 파일들)의 URI를 받아오게 된다.
+ 이 URI를 통해서 DB에 접근하는데 외부 앱 역시 이 URI를 해석하여 필요한 DB query 작업을 하고 return값을 돌려준다.
```
<provider android:name=".TestProvider"
          android:authorities="com.test.contentprovidertest.TestProvider"
          android:exported="true">
```
위의 코드는 데이터를 제공할 곳의 AndroidManifest.xml에 provider를 추가한 코드입니다.
```
  Cursor cursor=getContentResolver().query(
    Uri.parse("content://com.test.contentprovidertest.TestProvider"),null,null,null,null);
```
위의 코드는 provider를 선언한 앱에서 authorities로 지정한 것을 Uri를 통해서 접근하도록 contentresolver를 사용하는 코드입니다.

## 4) Cursor
+ Cursor는 DB에서 각 행을 참조하는 역할을 한다.
+ Cursor를 행 단위로 움직임으로써 DB에서 필요한 값을 받아오게 된다.
