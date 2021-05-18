# 10. ListView & RecyclerView
## 1) ListView 효율성 높이기
+ Adapter를 통해서 데이터를 표현하는 대표적인 AdapterView 중 하나가 ListView
+ 기본 ListView는 Custom Adapter를 만들지 않는다면 View를 계속 생성하기 때문에 비효율적
+ 따라서, Custom Adapter를 만들어서 getView()를 통해서 재활용 가능
+ 여기서 또 발생하는 문제는 View는 재활용해도 데이터가 바뀔때마다 findViewById()를 해야 하는데 overhead가 발생
+ 따라서, 각각의 View에 표시할 data를 미리 hold하는 ViewHolder를 만들고 setTag()를 통해서 효율성을 높인다.

## 2) RecyclerView()
+ ListView에서 효율성을 높이기 위해 Custom Adapter를 만들고 View 재활용, ViewHolder를 만들어서 사용
+ 하지만 강제성이 없다.
+ RecyclerView()는 ViewHolder 패턴에 강제성을 부여하여 반드시 ViewHolder 패턴을 사용하도록 한다.

## 3) ViewHolder와 ViewHolder 패턴
+ ViewHolder 객체는 ListView에서 사용한 방식과 같이 각각의 레이아웃의 태그 필드 안에 각 구성 요소 view를 저장하도록 하는 객체
+ 태그 필드 안에 구성 요소 view를 저장하여 ViewHolder에 각 view를 보관하기 때문에 불필요한 findViewById()를 하지 않아도 된다.
+ 이러한 ViewHolder를 사용하는 방식이 ViewHolder 패턴

## 4) 또다른 RecyclerView와 ListView의 차이
+ ListView는 세로 방향만 지원하지만 RecyclerView은 LayoutManager를 통해서 가로/세로/그리드/지그재그 방향 모두 지원
+ ListView는 목록의 개별 항목에 대한 clicklistener interface를 제공하지만 RecyclerView는 제공하지 않아 직접 listener interface를 만들어야 한다.

## 5) RecyclerView Adapter 구성
+ RecyclerVie Adapter는 RecyclerView.Adapter<VH>를 extends하고 여기서 VH는 ViewHolder를 의미
+ 의무적으로 3가지 method를 override해야 한다.
+ onCreateViewHolder, onBindViewHolder, getItemCount
1. ViewHolder onCreateViewHolder(ViewGroup parent, int viewType)
+ 새로운 ViewHolder를 create하는 곳으로 새롭게 생성해야 한다면 먼저 이 method가 호출된다.
+ 이 method에서 ViewHolder에 담을 view를 inflate하고 view를 담은 ViewHolder를 return한다.
2. void onBindViewHolder(@NonNull ViewHolder holder, int position)
+ 이곳에서는 재활용되거나 onCreateViewHolder에서 생성한 holder를 가지고 와서 데이터를 bind하는 곳이다.
+ ViewHolder holder가 내가 사용할 holder
3. int getItemCount()
+ RecyclerView를 구성하는 전체 item 수를 return하는 곳
+ 여기서 제대로된 값이 return되어야 item수와 position을 비교하여 체크하고 RecyclerView의 각 item를 생성한다.
  
## 6) 예시
1. ViewHolder
```
public class TestViewHolder extends RecyclerView.ViewHolder{
  TextView title, body;
  public TestViewHolder(@NonNull View itemView){
    super(itemView);
    title=itemView.findViewById(R.id.title);
    body=itemView.findViewById(R.id.body);
  }
  public void settingitem(Data data){
    title.setText(data.title);
    body.setText(body.body);
  }
}
```
2. RecyclerView Adapter 형태
```
public class TestRecyclerVIewAdapter extends RecyclerView.Adapter<TestViewHolder>
```
3. RecyclerView Adapter의 onCreateViewHolder
```
public TestViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType){
  View v=LayoutInflater.from(context).inflate(R.layout.resource, parent, false);
  TestViewHolder holder=new TestHolder(v);
  return holder;
}
```
4. RecyclerView Adapter의 onBindViewHolder
```
public void onBindViewHolder(@NonNull TestViewHolder holder, int position){
  holder.settingitem(data.get(position));
}
```
5. RecyclerView Adapter의 getItemCount
```
public int getItemCount(){
  return data==null?0:data.size();
}
```








