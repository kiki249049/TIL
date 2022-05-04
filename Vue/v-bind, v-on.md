> ## v-bind
>
> - Vue와 html요소를 묶어주는 방법이다.
>
> ```vue
> <div id="app">
> 	<img src="imageSrc" alt="">
> </div>
> ```
>
> body에 이런 image태그가 있고
>
> ```vue
>  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
>   <script>
>     const app = new Vue({
>       el: '#app',
>       data: {
>         imageSrc: 'https://picsum.photos/200/300/',
>         isRed: true,
>       }
>     })
>   </script>
> ```
>
> 아래 script에 이런 Vue instance가 있다라고 한다면
>
> ```vue
> <img v-bind:src="imageSrc" alt=""> 
> or 
> <img :src="imageSrc" alt="">
> ```
>
> 로 아래의 Vue instance와 **바인딩**을 하여 Vue instance에 있는 imageSrc data를 가져다 쓸 수 있다.

## v-on

> v-on은 그 전에 자바스크립트로 일일히 const element = document.querySelector로 지정한 후 element.addEventListener('action',function)으로 지정해 주었던걸 손쉽게 html과 Vue instance의 상호작용으로 **손쉽게 만들고 가시성**도 좋게 만들어 주는 방법이다.

가령, 이런 코드가 있다고 하자

```vue
 <div id="app">
 	<button>button</button>
 </div>
 
 <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    const app = new Vue({
      el:'#app',
      data : {
        message:'Hello Vue',
      },
      methods : {
        alertHello : function(){
          alert('hello')
        },
      }
    })
  </script>
```

여기서 주목 할건 위의 div요소

```vue
<div id="app">
 	<button>button</button>
</div>
```

를 주목하자 그 전에는 const button = document.querySelector('button')으로 지정해주고 button.addEventListener('submit',function)으로 설정 해줬던 것을 v-on을 사용하면

```vue
<div id="app">
 	<button v-on:click='alertHello'>button</button>
</div>
or
<div id="app">
 	<button @click='alertHello'>button</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    const app = new Vue({
      el:'#app',
      data : {
        message:'Hello Vue',
      },
      methods : {
        alertHello : function(){
          alert('hello')
        },
      }
    })
  </script>
```

이제는 손쉽게 **v-on이 javascript의 addEventListener역할**을 v-on:click뒤에 오는 **'alertHello'라는 것은 addEventListener에서 두번째 인자로 오는 function**의 역할을 하게 된다.