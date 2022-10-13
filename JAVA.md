# JAVA

```java
List<string>listA = new ArrayList(); // list 선언 => 리스트는 인터페이스
ArrayList<string>ArrayList = new ArrayList<>(); // ArrayList 선언 => ArrayList는 클래스
```



## **1. List**

리스트는 배열의 한계 때문에 만들어진 자료형.

프로그래밍 중 크기를 알 수 없는 경우가 더 많다.

List는 메모리가 허용하는 한 '계속해서 추가'할 수 있도록 만든 자료형 클래스이다.

 

 

**(1) 추가**

List<String> listA = new ArrayList();

 

listA.add("김삿갓");

listA.add("홍아리");

listA.add(new String("홍길동"));

listA.add(1,"1번째 요소값"); => 인덱스 1에 1번째 요소값이 들어가고

!데이터들이 하나씩 밀리게 된다.!

 

**(2) 조회**

하나씩 값을 조회하고 싶으면 get(index);

데이터를 전부 출력하고 싶다면 Iterator와 for문 사용.

 

String element0 = listA.get(0).toString();

 

Iterator 전체 조회

Iterator iterator = listA.iterator();

while(iterator.hasNext()){

  String element = (String) iterator.next();

}

 

for loop 통한 전체 조회

for(Object object: listA){

  String element =(String) object;

}

 

**(3)값 삭제**

listA.remove(0);

listA.remove("홍길동");

 

**(4)값이 있는지 확인하는 방법**

listA.contains("홍길동");

true면 있음, false면 아님.

 

**(5)해당 위치 앞에 값을 집어 넣고 싶을 때**

int index= listA.indexOf("홍길동");

listA.add(index,"홍길동 앞에 값 추가");

 

 

## **2. ArrayList**

배열처럼 고정된 크기를 가지는 것이 아니라 메모리가 허용하는 한 자동으로

ArrayList **크기는 동적으로 변경**된다.

 

**(1) 선언**

ArrayList<integer> arrayList = new ArrayList<>();

 

**(2) 데이터 추가**

arrayList.add(0);

arrayList.add(1);

 

for(int i: arrayList)

{

  System.out.println("값 :"+i);

}

 

arrayList.add(1,10) => list와 똑같이 인덱스 1에 데이터가 들어나고 뒤에 element 들은 자동으로 밀림.

 

**(3) addAll**

메소드를 통해 ArrayList에 ArrayList를 추가할 수 있다.

 

arrayList2 => 또 다른 arrayList 생성

 

arrayList.addAll(arrayList2); => arrayList에 arrayList2가 삽입.

add랑 동일하게 뒤에 삽입됨

 

**(4) 데이터 제거**

arrayList.remove(1); => 원하는 인덱스 데이터 삭제.

ArrayList는 자동으로 size가 조절된다.

 

**(5) ArrayList로부터 특정 데이터 가져오기**

List<Integer> list = arrayList.subList(1,3);

=> arrayList로부터 index 범위 1~3에 해당하는 element들을 List 형태로 반환받는다.

★범위가 1~3까지 지정이 되었지만 toIndex앞까지에 해당하는 element까지만 반환.

 

Index       0 1 2 3 4

arrayList(값)   1 2 3 4 5

 

2,3 값만 가져온다는 뜻!!(index 1~2만 가져온다)★

 