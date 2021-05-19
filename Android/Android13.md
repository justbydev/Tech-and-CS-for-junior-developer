# 13. Okhttp3
## 1) Okhttp3란
+ HTTP 통신을 간편하게 할 수 있도록 Square사에서 제공하는 오픈소스
+ 이를 통해서 REST 통신(GET, POST, PUT, DELETE) 를 간단하게 할 수 있다.
+ 안드로이드는 주로 client 역할을 하기 때문에 server와의 통신을 할 때 Okhttp3를 사용할 수 있다.
+ 만약, Okhttp3를 사용하지 않는다면 네트워크 통신은 Main Thread에서 할 수 없기 때문에 Worker Thread를 만들거나 AsyncTask를 통하여 통신을 해야 하지만 Okhttp3를 사용하면 간단하게 네트워크 통신을 할 수 있다.

## 2) 동기/비동기
+ Okhttp3는 동기, 비동기 방식 두가지 다 제공한다.
+ 동기식이면 .execute() 를 사용한다.
+ 비동기식이면 .enqueue()를 통해서 Callback을 구현한다.(onFailure, onResponse)

## 3) 간단한 예시
1. GET(동기)
```
OkHttpClient client=new OkHttpClient();//안드로이드 client
Request request=new Request.Builder()//server에게 보낼 request
          .addHeader("header에 추가할 key", value)
          .url(requestURL)
          .build();
          
Response response=client.newCall(requst).execute();//response에 server로부터 온 데이터 저장

String return_msg=response.body().string();
//return_msg를 parsing하거나 Gson 사용
//Gson gson=new Gson();
//Object object=gson.fromJson(return_msg, Object.class);
```

2. POST(동기)
```
OkHttpClient client=new OkHttpClient();
Request request=new Request.Builder()
          .addHeader("header에 추가할 key", value)
          .url(requestURL)
          .post(POST로 전달할 내용)
          .build();
Response response=client.newCall(request).execute();
String return_msg=response.body().string();
```
3. 비동기
+ 만약 비동기라면 execute() 대신에 .enqueue(new Callback())을 한다.
+ Callback 함수로 onFailure, onResponse
+ onResponse에 동기에서 받은 Response response가 인자로 있고 같은 방식으로 response.body().string()을 통해 확인
