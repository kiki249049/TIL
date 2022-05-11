# Vuex

오늘은 vue의 데이터관리를 효율적으로 하게 해주는 vuex에 대해서 배웠다. Vue를 처음배울때 props와 emits을 하는것은 좋았지만 구조가 복잡해지면 저~~~기 아래서 맨 위에까지 올린다고하면 emits을 도대체 몇번을 해야하는걸까...? 라는 생각을 하곤하였다. 걱정도 잠시, **vuex를 사용하면 마치 클라우드처럼 데이터를 저장하고있는 vuex라는 공간에서 데이터를 뽑아쓸 수가 있게 되었다**!

이제 Vuex에 대해서 본격적으로 알아보자.

먼저 프로젝트 생성후 다음 명령어를 쳐서 vuex파일을 만들자.

```bash
$ vue add vuex
```

그렇게 되면 src폴더 밑에 store폴더가 생성되게 되고 **그 아래 index.js**파일이 생성될것이다. 처음 만들때는 다음과 같은 구조를 띄고있다.

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
  },
  getters: {
  }, // 이 영역은 원래 없는것인데 추가해주었다.
  mutations: {
  },
  actions: {
  },
  modules: {
  }
})

```

다음과 같이 vuex를 담당하는 index.js파일은 4가지 영역으로 살펴볼 수 있다.

## Vuex의 영역

### 1. state

: 중앙에서 관리하는 모든 상태정보를 말한다. 즉 우리가 저장하고 싶어하는 데이터를 가지고 있는 영역을 말한다.

### 2. mutations

: state영역을 변경할 수 있는 유일한 방법이다. 오직 mutations에 있는 함수들만 state의 정보를 변경할 수 있으며 다른 함수들은 직접적으로 state에 접근해서 state내용을 변경하면 안된다.

### 3. actions

: vuex안에서 재미있게 다시 mutations을 호출해주는 역할을 하는 재미있는 부분이다. 마치 state를 접근하는게 매우 중요한 부분이라 보호케이스로 핸드폰을 한번 더 감싸는 그런역할을 하는 부분이다.

### 4. Getters

: Getters는 state에 있는 정보를 바탕으로 따로 로직을 돌려 가공하여 return값을 반환해주는 역할을 하는 함수들을 모아 놓은 곳이다. 예를 들면 state안에 할일 리스트인 todos=['밥먹기','공부하기','운동하기']가 있다라고 한다면 할일의 갯수인 todos의 length를 return해주는 함수같은 것을 모아놓는 부분이다.(**computed랑 비슷한 개념이라 보면 될 것같다.**) 



## Vue component에서 Vuex요소를 사용하는 방법

Vuex에 여러 함수를 만들었으면 이제 그것을 Vue컴포넌트에서 사용해야 의미가 있을 것이다.

예를 들어 Vuex가 이런식으로 만들어져 있다고하자

```js
import Vue from 'vue'
import Vuex from 'vuex'
import createPersistedState from 'vuex-persistedstate'

Vue.use(Vuex)

export default new Vuex.Store({
  plugins: [
    createPersistedState(),
  ],
  state: {
    todos : [
    ]
  },
  getters: {
  },
  mutations: {
    CREATE_TODO(state, todoItem){
      state.todos.push(todoItem)
    },
    DELETE_TODO(state, todoItem){
      const index = state.todos.indexOf(todoItem)
      state.todos.splice(index,1)
    },
  },
  actions: {
    createTodo(context, todoItem){
      context.commit('CREATE_TODO',todoItem)
    },
    deleteTodo(context, todoItem){
      context.commit('DELETE_TODO',todoItem)
    },
  },
  modules: {
  }
})

```

위 코드에 부연설명을 붙이자면 actions에서 context.commit메서드를 이용해 위의 mutations의 함수를 때려 실행시키는 방식이다. 작동 예시를 들기 위해 이런 Vue컴포넌트가 있다고 하자.

```vue
<template>
  <div>
    <input type="text" v-model.trim="todoTitle" @keyup.enter="createTodo">
    <button @click="createTodo">할일 추가!</button>
  </div>
</template>

<script>
export default {
  name : "TodoForm",
  data(){
    return {
      todoTitle:''
    }
  },
  methods : {
    createTodo(){
      const todoItem = {
        title : this.todoTitle,
        isCompleted : false,
        data : new Date().getTime()
      }
      if(todoItem.title) {
        this.$store.dispatch('createTodo',todoItem)
      }
      this.todoTitle =''
    }
  }
}
</script>

<style>

</style>
```

코드를 살펴보면 v-model로 todoTitle이 이어져 있고 input에 todoTitle을 쓰고 엔터를 누르거나 아래의 버튼을 누르면 v-on으로 methods의 createTodo가 실행되는 방식이다.

아래의 createTodo함수를 자세히 살펴보면 우리가 주목해야 할 부분은 바로 이곳이다.

```js
if(todoItem.title) {
        this.$store.dispatch('createTodo',todoItem)
      }
```

코드를 보면 대충 감이 오겠지만 dispatch라는 method는 vuex에 접근을하게 해주는 메소드이다. 쉽게 말하자면 todoItem이라는 Object를 생성하여 vuex에 있는 createTodo actions에 전달하겠다는 뜻이다. 그렇게 되면 위의 createTodo를 인자와 함께 때려주게 되고 그대로 Mutations의 CREATE_TODO를 때려주어 state.todos에 저장이 되게 되는 메커니즘을 이용한것이다.



이렇게 Vuex로 클라우드식으로 데이터를 저장하게 되면 데이터관리와 유지보수, 접근이 좀 더 쉬워진다는 장점이있다. 프로젝트 구성이 복잡해질수록 VueX의 파워는 엄청날 것이다!