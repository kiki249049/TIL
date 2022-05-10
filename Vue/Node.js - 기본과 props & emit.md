# Node.js - 기본과 props & emit

오늘은 말로만 듣던 Node.js를 배워보았다. 그 중 node.js에서 기본이 되는 부모와 자식간의 데이터를 주고 받는 방식인 props와 emit을 만들어 보았다.



먼저 node.js로 props와 emit을 구현하기 전에 프로젝트를 시작하는 법을 알아보자.

그 전에 몇가지 용어 정리가 필요한데

> Vue CLI : Vue.js 개발을 위한 표준도구, 프로젝트 구성을 도와주는 역할을 한다.
>
> node.js : 자바스크립트를 브라우저가 아닌 환경에서도 구동할 수 있도록 하는 자바스크립트 런타임 환경
>
> npm(Node Package Manage) : python에서 pip가 있다면 node.js에서는 npm이 그 역할을 담당한다. pip와 마찬가지로 의존성 패키지를 관리한다.

### Vue CLI 시작 준비순서

```bash
$ npm install -g @vue/cli # vue cli설치

$ vue create my-first-app # app 생성
> Default([Vue 2] babel, eslint) # 이것 선택.
$ cd my-first-app # app폴더에 들어가
$ npm run serve # 서버 작동!
```

#### babel

프로젝트를 시작하고 파일들을 보면 babel이라고 써진 파일을 볼수 있을 것이다. 이 파일은 Javascript컴파일러로 자바스크립트의 최신스타일 코드를 이전버전으로 번역/변환해 주는 도구라고 생각하면 된다.

예를들어

```javascript
// babel Input
[1,2,3].map((n)=> n+1); // 현재 스타일인 arrow function을
// babel Output
[1,2,3].map(function(n){
    return n+1;
}) // 예전 스타일 코드인 기본함수스타일 코드로 Babel이 변경해준다.
```



### Props & emit

Vue app은 자연스럽게 중첩된 컴포넌트 트리로 구성된다. 컴포넌트간의 부모-자식 관계가 구성되면 이들 사이에 필연적으로 의사소통이 필요하다! 그 의사소통을 구현한 것이 바로 props&emit이 되겠다.

> 부모는 자식에게 데이터를 전달(Pass Props)하며, 자식은 자신에게 일어난 일을 부모에게 알린다.(Emit event)
>
> Props는 아래로, events는 위로
>
> 부모는 **props를 통해 자식에게 데이터를 전달**하고, 자식은 **events를 통해 부모에게 메시지를 emit**함

이것을 코드로 구현해 보자

```bash
$ vue add router # vscode 터미널에서 라우터를 추가
```

라우터를 추가하게 되면 옆에 views라는 디렉토리가 생성되면서 안에 AboutView.vue와 HomeView.vue 2개의 vue파일이 생성된 것을 볼 수있다.

여기서 가장 중요하게 봐야할것은 위계질서 관계인데

가장위에 App.Vue라는 가장큰 틀이 있고 그 아래 AboutView.vue와 HomeView.vue가 같은 레벨에 있고 AboutView.vue 아래 Helloworld.vue가 있는 구조이다.

요약하면 App.Vue 안에 AboutView,HomeView 또 HomeView안에 Helloworldvue가있다.

먼저 HomeView.vue와 Helloworld.vue의 상호작용을 좀 더 쉽게 알아보기위해 Homeview.vue와 Helloworld.vue를 다음과 같이 만들었다.

**HomeView.vue**

```vue
<template>
  <div class="home">
    <h1>부모의 영역</h1>
    <p>{{ onlyParent }}</p>
    <p> 자식으로부터 온 데이터: {{ fromChild }}</p>

    <hr>
    <h1>자식의 영역</h1>
    <!-- 3. 실제로 쓰기 -->
    <!-- (1) 직접내리기 + (2) 부모가 소유한 데이터 동적 (:) 넘기기 + (3) 숫자넘기기 + (4) 커스텀 이벤트 부착 -->
    <HelloWorld msg="직접 내린 data" :to-child-data='toChildData' :num='1' @child-input-change="parentGetChange"/>
  </div>
</template>

<script>
// @ is an alias to /src -> @ 까지만 써도 src/ 시작과 동일합니다.
// 1. 가져오기
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'HomeView',
  // 2. 등록하기
  components: {
    HelloWorld
  },
  // data {} -> 이렇게 쓰면 안되고, 데이터는 '함수'여야 합니다!
  data() {
    return {
      onlyParent: '부모에게만 있는 데이터',
      toChildData: '자식에게 내려가는 데이터',
      // 자식에게 받은 데이터를 담아줄 변수 초기화
      fromChild: '',
    }
  },
  methods: {
    // 인자는 여기서 받아줍니다.
    parentGetChange(inputData) {
      this.fromChild = inputData
    }
  }
}
</script>

```

**Helloworld.vue**

```vue
<template>
<!-- div로 한번은 감싸줘야 합니다. -->
  <div class="hello">
    <!-- props 받아서 바로 활용할 수 있습니다. -->
    <h3>{{ msg }}</h3>
    <h3>{{ toChildData }}</h3>
    <!-- p태그는 reset.css 없이는 마진을 조금 줘서 레이아웃상 이점때문에 사용하였습니다. -->
    <p>
      <!-- 해당 버튼에는 함수가 연결되어 있는데, num이 Number type으로 잘 내려왔는지 확인하는 버튼입니다. -->
      <button @click='checkClick'>내려왔나 확인해보자</button>
    </p>
    <!-- 하려고 하는 것: input -> child 정보 바인딩 -> emit 하려고! -->
    <p>
      <label for="childInput">자식에서 입력 : </label>
      <!-- v-model 까지는 입력시 아래 데이터에 바인딩 -->
      <!-- keyup.enter 하는 순간 뒤의 함수 트리거! -->
      <input type="text" id="childInput" v-model="childData" @keyup.enter="childInput">
    </p>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
    toChildData: String,
    num: Number,
  },
  // 데이터는 리턴으로!
  data() {
    return {
      childData: '',
    }
  },
  methods: {
    // 그냥 타입 체크용 메서드
    checkClick() {
      console.log(typeof this.num)
    },
    // emit 담당하는 메서드 -> 커스텀 이벤트는 js 영역이지만 케밥 케이스
    childInput() {
      // payload는 여러개를 넘길 수 있으나 이런 경우 obj로 찍어서 넘기는게 낫습니다.
      this.$emit('child-input-change', this.childData)
    }
  }
}
</script>

<!-- scoped 속성이 있는 경우 이 vue 파일 안에서만 유효합니다. -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

```

여기서 주의 깊게 봐야할건 Helloworld의 props부분과 methods안에 childInput의 this.$emit부분인데

props부분은 Helloworld의 상위 vue인 Homeview에서 온 정보들을 받는 부분이라고 보면된다. Homeview에서 Helloworld로 props를 내려주는 부분은 Homeview의 templates안에 있는 HelloWorld tag를 보면 되겠다.

주의할것은 :v-bind로 props로 내려보낼때 **html에선 to-child-data처럼 kebab-case**로 써주고 자식vue에서 **props를 받을떄는 toChildData처럼 camelcase로 받아야한다는 것**이다.

그리고 자식 Vue에서 emit을하여 부모에서 받을때는 @인 v-on으로 받고 안에 데이터를 가지고 다시 emit으로 올라오기때문에 parentGetChange(inputData)같이 emit으로 올라올때 때려준 함수를 inputData같은 임의인자를 설정해줌으로써 자식에게서 올라온 데이터를 사용할 수 있다.