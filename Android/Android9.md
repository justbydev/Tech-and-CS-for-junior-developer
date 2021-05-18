# 9. Adapter
## 1) Adapter란
+ 어플리케이션을 보면 위아래/좌우로 스크롤하면 새로운 항목들이 계속 나오는 화면을 볼 수 있는데 이런 형태의 개발을 위해 사용하는 것이 Adapter
+ Adapter는 하나의 object로써 사용자에게 보여지는 View와 View에 올리는 Data를 연결하는 Bridge 역할을 한다.
+ 즉, 사용자에게 보여주고자 하는 데이터 원본을 받아서 관리하고 View(여기서는 AdapterView)가 출력할 수 있는 형태로 데이터를 제공하는 중간 객체 역할을 한다.
+ Adapter랑 연결된 원본 데이터가 변경되면 notifyDataSetChanged() method를 호출하여 데이터 변경을 알리고 다시 그린다.

## 2) AdapterView
+ AdapterView는 ViewGroup을 상속받으며 내부에 수많은 View를 담아서 사용자에게 보여지는 부분이다.
+ 데이터를 직접 AdapterView에 담지 않고 앞에서 말한 Adapter를 통해서 담는다.
+ ListView, RecylerView 등이 대표적인 AdapterView다.
+ Adapter에 먼저 데이터를 담고 View.setAdapter()를 통해서 Adapter를 연결한다.

## 3) Custom Adapter
+ 기본적인 Adapter(ArrayAdapter, SimpleAdapter 등)을 사용할 수 있지만 만약 담아야 하는 데이터의 수가 많아지게 되면 메모리 누수 및 부족 현상으로 앱이 강제 종료될 수 있다.
+ 스크롤 형식으로 같은 형태의 View를 보여주기 때문에 화면에 한번에 보여지는 최대 view 개수만을 새롭게 만든다.
+ 이후, 스크롤 해서 다시 보여지게 되는 View들은 기존 생성했던 View를 재활용하여 담기는 데이터만 바꿔서 사용한다.
+ 데이터를 관리하는 역할은 Adapter이기 때문에 Custom Adapter를 만들고 이때 기본적으로 BaseAdapter를 extends 한다.
+ Custom Adapter에서 재활용할 때 getView()를 통해서 이루어진다.

```
public View getView(int position, View convertView, ViewGroup parent){
  TextView text;
  if(convertView==null){
    LayoutInflater inflater=LayoutInflater.from(context);
    convertView=inflater.inflate(R.layout.resource, parent, false);
  }
  text=convertView.findViewById(R.id.id);
  text.setText(data.get(position));
  return convertView;
}
```
