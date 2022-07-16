# Vanilla JS

### 1. const 와 let의 차이

```javascript
let a = 5;
const b = 2;
```

const는 상수고 값이 바뀔 수 없다. 

let은 나중에 바뀔 수 있는 변수일때만 사용

```javascript
let a = 5;
a = 7
console.log(a)
=> 7
```

```javascript
const a = 5;
a = 7
console.log(a)
=> error! // const는 바꿀 수 없기 떄문
```

기본적으로 const를 쓰고 나중에 가변적인 변수에서만 let을 사용한다.

### 2. boolean

```javascript
const amIFat = null;
console.log(amIFat)
// null => 메모리에 만들어졌고 값이 빈칸
let something;
console.log(something); 
// undefined => 메모리에 만들어졌지만 값이 없는것.
```

### 3. array

```javascript
const nonsense = [1,2,"hello", true]
```

### 4. object

```javascript
const playerName = "nico"
const playerPoints = 121212;
const playerHandsome = true;
const playerFat = "little bit"

// 이런식으로 적으면 매우 비효율적으로 데이터를 관리하게 된다.
const player = { 
    name : 'kanghyun', 
    points : 10, 
    isHandsome : true, 
    isFat : false
};
console.log(player);
console.log(player.name);
player.name = "nico"
// const를 썼는데 name이 바꿔지는 것은 전체를 바꾸는게 아니라 안에 있는 요소를 바꿨기 때문에 가능하다.
player.lastName = "potato";
// 데이터 추가도 가능!
```

### 5. function

```javascript
function sayHello(){
    console.log("Hello!")
}
const player = {
    name : "nico",
    sayHello: function(otherPersonName){
        console.log(`hello ${otherPersonName}!`)
    }
} 
console.log(player.name)
player.sayHello("lynn")
```

### 6. return

```javascript
const age = 96;
function calculateKrAge(ageOfForienger){
    return ageOfForeinger + 2;
}
const krAge = calculateKrAge(age);
console.log(krAge)
```

### 7. Conditional

```javascript
const age = prompt("How are you??"); // prompt는 메시지창을 띄우는 메소드, js를 잠시 멈춘다.
console.log(age);
parseInt(age);
// prompt로 나오는 글자는 기본적으로 string이기 때문에 int로 바꿔주는 메소드인 parseInt로 숫자로 바꿔준다.
// 만약 prompt에 숫자가 안들어갔다면 ?? => NaN이 나온다.
```

&& => and 

|| => or

### 8. isNaN => 숫자인지 아닌지 검증하는 함수

```javascript
const age = parseInt(prompt("How old are you??"));

console.log(isNaN(age));
if(isNaN(age)){
    console.log("Please write a number")
}else{
    console.log(age)
}
```

### 9. document

```javascript
document
// #document
console.dir(document)
// document object가 나온다.
```

document에 JS가 연결돼있다!! 접근해서 JS로 바꿀 수 있음!

### 10. getElementById

```javascript
const title = document.getElementById("title")
// id로 tag요소를 가져오는 방법!
```

### 11. console.dir

```javascript
console.dir(title)
// console.dir은 console.log보다 더 자세하게 모든 것을 보여준다.
```

### 12. querySelector(매우 중요! 되게 많이씀)

```html
 <div class="hello">
      <h1 autofocus  id="title">Grab me!</h1>  
  </div>
```

```javascript
// div안에 있는 h1 타이틀을 가져오고 싶다면
const title = document.querySelector(".hello h1");
// querySelector는 .hello처럼 class 표시를 해줘야한다.
const title = document.querySelector(".hello h1:first-child")
// 첫번째 h1만 가져오고 싶을때 사용
```

하지만 .hello h1가 여러개 있는 경우에는 가장 첫번째 것만 가져온다.

다 가져오고 싶으면 querySelectorAll을 사용!

### 13. addEventListener

```javascript
const title = document.querySelector("div.hello:first-child h1")
function changeColor(){
    if title.style.color !== "red"{
     title.style.color = "red"   
    }else{
        title.style.color = "black"
    }
}
title.addEventListener("click",changeColor)
```

### 14. mouseenter, mouseleave

mouseenter = 마우스 들어가면 발생하는 이벤트

mouseleave = 마우스 빠져나가면 발생하는 이벤트

```javascript
title.addEventListener("mouseenter",function)
```

### 15. window

```javascript
function handleWindowResize(){
  document.body.style.backgroundColor = "tomato";
}
title.addEventListener("click",changeColor)
title.addEventListener("mouseenter",changeEnterText)
title.addEventListener("mouseleave", changeLeaveText)

window.addEventListener("resize",handleWindowResize)
console.dir(title);
```

### 16. Clipboard event

```javascript
// ctrl+c했을때 발생하는 이벤트
window.addEventListener('copy',anyFunction)
```

### 17. Connection event

```javascript
// wifi가 연결에 따라 발생하는 이벤트
window.addEventListener("offline",offline);
window.addEventListener("online",online)
```

event를 심어주는 과정

1. element를 선택
2. addEventListener
3. 반응!! (함수를 넣는다!!)

### 18. CSS와 JS html을 통한 대화

```css
body {
  background-color: beige;
}

h1 {
  color: cornflowerblue;
}

.active {
  color : tomato;
}
```

```javascript
function changeColor(){
  title.className = "active";
}
title.addEventListener("click",changeColor)
// active는 getter이면서 setter
```

javascript를 작성할때 변수에 raw value를 넣을것!

### 19. javascript로 원하는 class만 없애기

```javascript
const title = document.querySelector("div.hello:first-child h1");
function changeColor(){
    const clickedClass = "active"
    if(title.classList.contains(clickedClass)){
        title.classList.remove(clickedClass)
    }else{
        title.className.add(clickedClass)
    }
}
```

className은 전에 있던 class를 상관안하고 모든걸 바꿔버림 따라서 classList사용

classList는 element의 classList의 접근을 허용한다는것.

### 20. toggle

```javascript
function changeColor(){
    title.classList.toggle("active")
}
// 위의 19번 함수와 같은내용
```

form은 enter로 입력되는게 디폴트!

### 21. submit

```javascript
const loginForm = document.querySelector("#login-form")

function onLogsubmitted(event){
  event.preventDefault(); // 브라우저의 기본 동작을 막아줌
  console.log("submit")
}

loginForm.addEventListener("submit", onLogsubmitted)
// Form에 submit을 해주면 안에있는 btn도 같이 click되는 효과가 일어난다!
```

### 22. localStorage

```javascript
localStorage.setItem("username", "kkh")
// 이렇게하면 localstorage에 key값 username, value에 kkh저장
localStorage.removeItem("username")
// 이렇게하면 username없어짐
localStorage.getItem("username")
// username 불러옴
```

### 23. 로그인할때 유무에 따라 요소 표시하기

```javascript
const h1 = document.querySelector("h1")
const loginForm = document.querySelector("login-form")
const HIDDEN_CLASS = "hidden"
// 일단은 html에서 h1와 loginForm은 hidden인 상태로 놔두고 하나씩 없애주는 형식!

const saveUsername = localStorage.getItem("username") // key를 username으로 저장했을시!
if(saveUsername === null){
    loginForm.classList.remove(HIDDEN_CLASS)  
    loginForm.addEventListener("submit",onSubmit)
}else{
    h1.classList.remove(HIDDEN_CLASS); 	
    h1.innerText = `Hello ` + ${username}
}
```

### 24. interval => 매 간격마다 시행해야하는 event

ex) 시계, 주식시장 그래프 등등...

```javascript

```

### 25. Date

```javascript
const date = new Date()
clock.innerText = `${date.getHours()}`
```

new Date()  => 시간을 불러오는 함수

### 26. padStart => 숫자길이가 2가 아니라면 0을 추가해주는 함수

```javascript
"1".padStart(2,"0") // 길이가 2가 아니면 0을 추가한다.
// "01"
```

padEnd는 뒤쪽에 추가하는것

```javascript
"hello".padStart(10,"x")
// "xxxxxhello"
```

### 27. Math.random() => 0~1 사이의 숫자중에 랜덤으로 돌려줌

```javascript
 const quote = document.querySelector("#quotes span:first-child")
 const author = document.querySelector("#quotes span:last-child")

 quote.innerText = quotes[Math.floor(quotes.length*Math.random())].quote
 author.innerText=quotes[Math.floor(quotes.length*Math.random())].author
```

round는 반올림해주는 함수!

Ceil 올림

floor 내림

### 28. image삽입 createElement사용

```javascript
const bgImg = document.createElement("img")
document.body.appendChild(bgImg)
```

### 29. addEventListener "submit"있음!!

form tag에서 엔터로 보내는거 포함!

### 30. todo

```javascript
const todoForm = document.getElementById("todo-form")
const todoList = document.getElementById("todo-list")
const todoInput = todoForm.querySelector("input")

function handleTodoSubmit(event){
  event.preventDefault()
  const newTodo = todoInput.value
  const li = document.createElement("li")
  li.innerText = newTodo
  todoList.appendChild(li)
  todoInput.value = ''
}
todoForm.addEventListener("submit", handleTodoSubmit)
```

### 31. addTodo

```javascript
function paintTodo(newTodo){
  const li = document.createElement("li")
  const span = document.createElement("span");
  li.appendChild(span)
  span.innerText = newTodo
  todoList.appendChild(li)
}
```

### 32. Delete Todo

```javascript
function deleteTodo(event){
  const li = event.target.parentElement
  li.remove();
}
```



### 33. JSON.stringfy

```javascript
localstorage.setItem("todos",JSON.stringify(todos))
// 이렇게하면 todos리스트가 문자열로 저장!
```



### 34.JSON.parse

```javascript
const saveToDos = localStorage.getItem(TODOS_KEY)
console.log(saveToDos) // string
if(saveToDos !== null){
  const parsedTodos = JSON.parse(saveToDos)
  console.log(parsedTodos) // array
}
```



### 35. forEach

```javascript
function sayHello(item){
    console.log("this is the turn of", item)
}

if (saveTodos !== null){
    const parsedTodos = JSON.parse(saveTodos)
    console.log(parsedTodos)
    parsedTodos.forEach(sayHello)
}
// forEach는 굳이 들어갈 el를 명시해주지 않더라도 자동으로 sayHello에 원소로 들어가게 된다.
```



### 36. Date.now()

```javascript
//id값을 부여할때 쓰이는 함수
Date.now()
```



### 37. filter

```javascript
// 무언가를 삭제할때 유용하게 쓰이는 함수
function sexyFilter(newTodoObject){
    return newTodoObject.id !== li.id
}
[1.2.3.4].filter(sexyFilter)
// true값을 반환하는 값만 남기고 다 없앰
```

```javascript
function saveTodos(){
  localStorage.setItem("todos", JSON.stringify(todos))
}

function deleteTodo(event){
  const li = event.target.parentElement
  // li.id는 str이니 parseInt로 숫자로 바꿔주기!
  todos = todos.filter(todo => todo.id !== parseInt(li.id) )
  console.log(todos) 
  saveTodos()
  li.remove();
}

```



### 38. for in, for of

```javascript
const todos = [2,5,4,4,233,2,21]
for(key in todos){
    console.log(key)
}
// 0,1,2,3,4,5,6
for(value of todos){
    console.log(value)
}
// 2,5,4,4,233,2,21
```



### 39. geolocation

```javascript
// geolocation.getCurrenrPosition함수는 2개의 인자가 필요한데
// 첫번째는 문제가 없을때 실행되는 함수, 두번째는 에러가 났을때 실행되는 함수

function getSuccess(position){
  const lat = position.coords.latitude
  const long = position.coords.longitude
  console.log("U live in", lat,long)
}

function getFail(){
  alert("Can't find You!!")
}

navigator.geolocation.getCurrentPosition(getSuccess, getFail)
```



### 40. fetch 매우중요!!

```javascript
function getSuccess(position){
  const lat = position.coords.latitude
  const long = position.coords.longitude
  const url = `https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${long}&appid=${API_KEY}&units=metric`
  // fetch로 불러오고 계속 then으로 정보를 가져오는 식!
  fetch(url)
  .then(response => response.json())
  .then(data => {
    const weather = document.querySelector("#weather span:first-child")
    const city = document.querySelector("#weather span:last-child")
    weather.innerText = data.weather[0].main
    city.innerText = data.name
  })
}
```

