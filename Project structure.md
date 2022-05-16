final pjt 연습해볼것

# Accounts Vue

route-accounts/login  ==> nav bar에 구현

route-accounts/Signup ==> nav bar에 구현

route-accounts/detail =>아직 구현불가.

# Movie Vue => nav bar(Home)

searchBar

index => Search 결과반환

# Community Vue => nav bar(community)

route : community/create ==> 리뷰 폼

review_index : community/review_index

# Vuex

### state

accounts : []

review : []

movie : []

### Getters

좋아요 갯수

### Mutations

accounts와 review를 바꾸는것.

### actions

비동기식으로 구성



그런데 우리는 회신을 보낼때 웹서비스니까 주로 DB데이터를 보내겠죠?

Product라는 DB모델의 모든 데이터를 회신하라고 해보겠습니다.

\-------------------------------------------------------------------------------------------------

data = Product.object.all()

return JsonResponse(data, safe=False)

\-------------------------------------------------------------------------------------------------

에러발생!

TypeError: Object of type 'QuerySet' is not JSON serializable

이런 에러가 뜹니다. DB를 조회해서 집어넣은 변수의 Type은 QuerySet이라고 하는데 JSON으로 변환이 안되나봅니다.

 

그럼 QuerySet을 list로 바꾸면 되겠죠? 아래처럼 하면 됩니다.

\-------------------------------------------------------------------------------------------------

data = Product.object.all()

data = list(data.values())

return JsonResponse(data, safe=False)

\-------------------------------------------------------------------------------------------------

이렇게 값을 뽑아서 list화 해주면 됩니다. ※ .values()를 꼭 해주세요

백엔드 프론트엔드 연동시키는법ㄴ