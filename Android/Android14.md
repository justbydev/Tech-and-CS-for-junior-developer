# 14. Retrofit2 & Gson
## 1) Gson이란
+ HTTP 통신을 통해서 client와 server가 통신을 하는데 주고 받는 데이터 형식이 대부분 JSON 형식으로 되어 있다.
+ Google에서 만든 Gson의 경우 JSON 형식 데이터를 직접 parsing하지 안고 JAVA 객체에 담을 수 있도록 하거나 JAVA 객체를 JSON 데이터로 변환시켜주는 라이브러리

## 2) Retrofit2이란
+ OkHttp를 기반으로 더욱 간편하게 HTTP 통신을 하고 REST를 설계할 수 있도록 해주는 라이브러리
+ 즉, OkHttp 동일 Square 사에서 만든 OkHttp 라이브러리의 상위 구현체
+ 앞서 말했듯이 Okhttp를 기반으로 하고 있다.
+ 기본적으로 Gson과 함께 사용할 수 있다.
+ Retrofit2 역시 네트워크 통신을 위한 Worker thread나 Asynctask 없이 실행 가능
+ HTTP CRUD(GET, POST, DELETE, PUT)들을 정의해놓은 인터페이스를 구현하여 annotation을 이용하여 구현

## 3) 동기/비동기
+ OkHttp와 마찬가지로 동기/비동기 둘다 가능
+ 동기는 .execute() 사용
+ 비동기는 .enqueue(Callback())을 사용하며 역시 onResponse, onFailure Callback 구현

## 4) Retrofit interface
1. 기본적으로 GET, POST, DELETE, PUT 등을 @GET(request url detail)의 방식을 사용하여 표현
2. HTTP method 표시 밑에 Call<서버로부터 return 받는 데이터 담을 곳> api 이름(서버에게 보낼 것) 구조
3. @BODY JAVA 객체 이름: JAVA 객체 통째로 server에게 전송
4. @Path("pk") int pk: request url에 들어가는 변수로 예를 들어 "users/list/{pk}" 방식
5. @Field("key") String value로써 @FormUrlEncoded와 함께 사용하며 URL 상에 숨겨진 채로 전달(key=value)
6. @Query("key") String value로써 "users/list?key=value" 형식으로 보인채로 전달
7. @Headers(key) String value로써 HTTP Header에 key:value로 전달
8. @Part MultiparBody.Part image, @Part(key) String value로써 여러 가지 타입의 데이터를 한꺼번에 보낼때(주로 이미지, 파일등을 전송) 여러개를 지정하여 사용하며 @Multipart annotation과 함께 사용

## 5) 간단한 예시
1. 기본 설정(싱글톤 패턴과 함께)
```
private static Retrofit getInstance(){
  Gson gson=new GsonBuilder.setLenient().create();
  return new Retrofit.Builder()
          .baseURL(통신한 server base url)
          .client(okHTTPclient 설정했다면)
          .addConverterFactory(GsonConverterFactory.create(gson))
          .build();
}
```
2. GET
```
@GET(base url 뒤에 붙는 url detail)
Call<ArrayList<Object>> get_data();
```
3. Multipart
```
@Multipart
@POST(base url 뒤에 붙는 url detail)
Call<Void> send_data(@Part MultipartBody.Part file, @Part("filename") String filename);
```

4. Header+Path 사용
```
@GET("url detail/{pk}/")
Call<Object> login(@Header("Authorization") String header, @Path("pk") int pk);
```
