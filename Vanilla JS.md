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

