# Spring 공부

구조 src => main => java, resource

![image-20221011202735479](C:\Users\kiki2\AppData\Roaming\Typora\typora-user-images\image-20221011202735479.png)

### 1. Tomcat

Tomcat으로 8080포트에 접근

### 2. MVC 패턴

mustache를 통해 만든다. => html을 다르게 부르는것?

![image-20221011204007209](C:\Users\kiki2\AppData\Roaming\Typora\typora-user-images\image-20221011204007209.png)

컨트롤러에서 model의 정보를 받아 mustache에 넘긴다.

### 3. DTO

=> 폼데이터를 받는 객체

![image-20221011220324969](Spring 공부.assets/image-20221011220324969.png)

왼쪽부터 form에서 날린 데이터가 DTO로가서 Form데이터 형식으로 변환후 Controller로 날아감