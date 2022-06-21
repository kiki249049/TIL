SPA : single Page Application

시험공부 , vue복습, bootsrtap, css



single page Application!!

CSR

Client Side Rendering

서버에서 화면을 구성하는SSR 달리 client가 화면을 구성!



Model, View, View Model 

MVVM model이라고한다. vue는

Model

Vue에서 Model은 Javascript object이다.

Vue에서 View는 DOM이다. - Data의 변화에 따라서 바뀌는 세상이다.

ViewModel View Model은 모든 Vue instance다.

Vue.js 

데이터가 변경되면 Dom이 바뀌기 때문에

Data로직을 작성하고 DOM을 작성한다.

```js
var app = new Vue({
    el : "#app",
    data : {
           message : ""}
})
```

```js
var app4 = new Vue({
    el:"app",
    data : {
        todos : [
            {text : '복습하기'},
            {text : '밥먹기'},
        ]
    }
})
<h1 v-for="todo in todos">
    </h1>
```

vue 함수 객체내에서 화살표함수를 쓰게되면 vue instance가 아닌 window를 가르키게 되므로 안된다.

template syntax

1. interpolation

(1) Text

```html
<span>메시지 : {{ msg }}</span>
```

(2) Raw HTML

```html
<span v-html="rawHtml"></span>
```

(3) Attributes

```html
<div v-bind:id="dynamicId">
    
</div>
```



(4) JS 표현식

{{ number+1 }}

{{ text.split('').reverse().join('') }}

2. directive

v-text = "message"

v-html 

엘리먼트의 innerHTML을 업데이트 XSS 공격에 취약

임의의 사용자한테 입력받은 내용은 v-html에 절대 사용금지

### v-if 바인딩

```html
<div v-if="my-type === 'A'">
    A
</div>
<div v-else-if="my-type === 'B'">
    B
</div>
```

V-show와 v-if의 차이점

v-show는 렌더링되지만 눈에 보이지 않는 것이므로 v-if에 비해 렌더링 비용이 높다. 하지만 자주 변경되는 요소라면 한번 렌더링 된 이후 부터는 렌더링 되는지 여부만 알려주면 되기 때문에 토글비용이 낮다.

```vue
v-for = "todo in todos"
v-for = "(fruit,index) in fruits"
```

v-for 사용시 key 속성을 각 요소에 작성!!

watch : {

}

데이터가 변했을때 실행되는 함수.

filters 텍스트 형식화를 적용할 수 있는 필터.

SFC single File Components

Babel : Javascript compiler

자바스크립트의 ECMAScript 2015+ 코드를 이전버전으로 번역해주는 도구

WebPack : 모듈 간의 의존성 문제를 해결하기 위한 도구

Static Module Bundler

router-link -> link를 정의하는 공간

to='{name : ''}' or to="/"

```html
<router-link to='{name : 'home'}'>Home</router-link>
이런식으로도 name으로도 접근가능.
<router-link to='/about'>about</router-link>

<router-view></router-view>
```

router.push('name')로도 호출가능 

router.push({path: 'home'})

named route to='{name : 'home', params : {}'

router.push({name : 'user', params: {userId:'123'}})

```js
const routes=[
    {
        path:'/user/:userId'
    }
]
```

이동한 페이지에서는 $route.params.lottonum or $route.params.userId

```html
<router-link to="{name : 'lotto', params:{lottoNums:6}}"></router-link>
```

## Vuex

state management pattern + Library for vue.js

- state를 전역

컴포넌트의 공유된 상태를 추출하고 이를 전역에서 관리하도록 한다.

state 원본소스의 역할.	

내부에 있는 특정 state를 중앙에서 관리한다.

actions - mutations - state

context.commit

Actions는 비동기 mutations는 동기

new Date().getTime()

this.$store.state.todos

```vue
actions : {
	createTodo({commit},todoItem){
	commit('CREATE_TODO',todoItem)
}
},
const commit = context.commit
const { commit } = context
const {state,commit} = context
```

```js
state.todos = state.todos.map(todo => {
    if(todo === todoItem){
        return {
            ...todo,
            isComplete : !todo.isCompleted
        }else{
            return todo
        }
    }
})
```

:class = "{'asd' : 조건문.}"

```vue
import {mapState} from 'vuex'

computed : {
mapState(['todos',
])
}
import {mapGetters} from 'vuex'
computed {
	mapGetters(['GetTodosCount',
])
}
```

Plugin

createdPersistedState

now playing / search / recommend / community / signup / login

this.$router.push

$router.params.lottoNums

.env.local => key 숨기는곳!

splice(index,1)

import createPersistedState from 'vuex-persistedState'

plugins: [

​	createPersistedState

]
