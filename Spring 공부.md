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



### 4. Controller에서 DTO와 entity로 바꿔주는 기능을 담당

DTO에서는 Entity로 바꾸는 toEntity 메소드도 포함!

ArticleRepository Package에서는 Entity를 CRUD할 수 있는 CrudRepository 상속받아 사용 



### 5. 저장된 데이터를 조회하기

![image-20221012233814965](Spring 공부.assets/image-20221012233814965.png)

h2.Database에 접근허용

```sql
INSERT INTO ARTICLE(id,title,content) VALUES(3,'gfdsg','12314');
```

### 6. Lombok

- 코드를 간소화 시켜주는 메소드

![image-20221012235947061](Spring 공부.assets/image-20221012235947061.png)

이랬던 코드가

Lombok Annotation을 쓰면

![image-20221013000022124](Spring 공부.assets/image-20221013000022124.png) 

이렇게 생성자와 toString메소드를 생략할 수 있다.

### 데이터 조회

![image-20221013194652776](Spring 공부.assets/image-20221013194652776.png)

### Repository에서 ArrayList로 받게하기

![image-20221013201338788](Spring 공부.assets/image-20221013201338788.png)

![image-20221013201351406](Spring 공부.assets/image-20221013201351406.png)

그 후 Controller에서 List로 받는다.

# 스프링부트 흐름

1. 컨트롤러 생성(RestController Annotation)

2. 서비스 인터페이스 생성(필요 x)

3. 서비스 impl 클래스 생성 후 인터페이스 implements로 상속(Service Annotation)

4. 서비스 Entity생성 (2,3번에서 쓰일 것.)

   ```java
   @Entity
   @Getter
   @Setter
   @NoArgsConstructor
   @DynamicInsert
   @DynamicUpdate
   @Table
   // Entity Annotation리스트!
   
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Integer idx;
   // pk 설정 어노테이션
   
    @ManyToOne
    @JoinColumn(name="user_idx")
    private UserEntity userIdx;
   // fk 설정 어노테이션
   ```

5. Entity에 접근할 Repository생성

```java
import org.springframework.data.jpa.repository.JpaRepository;

// Entity가 들어가야함
public interface ArticleRepository extends JpaRepository<ArticleEntity, Integer> {
    
}
```

6. 컨트롤러 api 생성

```java
kakaoCallBack(HttpServletRequest request) // HttpServletRequest request 토큰 받는 부분.
```

6. Dto 생성
7. 서비스 쓰게 만들기 in Controller

```java
    private FarmmunityService farmmunityService;

    @Autowired
    FarmmunityController(FarmmunityService farmmunityService){
        this.farmmunityService = farmmunityService;
    }
```

