브라우저의 전역객체는 window

todoList.filter(function(todo)...)



```javascript
console.log(typeof undefined)
=> undefined
console.log(typeof null)
=> object
```

DOM

- 문서 조작

key로 접근 가능

window는 최상위 객체 작성시 생략가능.

document head,body등과 수많은 다른 요소들을 포함



let -> 재할당 예정인 변수에 사용가능

const -> 재할당 불가(값을 바꿀수가 없음.)

둘다 변수 재선언은 불가능, 블록스코프

var - 재할당, 재선언 다 가능 근데 hoisting때문에 let과 const 사용권장. 이것은 함수 스코프

hoisting 변수 선언 이전에 변수를 참조할 수 있는 현상.

```javascript
if ( 5 > 4 ) {
  var secret = '12345';
}

secret; // 12345


function a() {
  var secret2 = '12345';
}

secret2 ;  // secret2 is not defined
```

```javascript
if( 5 > 4 ) {
  let secret = '12345';
  const secret2 = '12345';
}

secret;  // secret is not defined
sercret2;  // secret2 is not defined
```



원시타입 : 숫자 , 문자열 , bool, undefined ,null(타입이 object)

참조타입 : array, function => object타입의 자료형

근데 null의 타입은 object

템플릿 리터럴 백틱(`) + ${expression}표현식가능.

undefined는 그냥 자바스크립트가 자동으로 할당해주는 값

null은 의도적으로 개발자가 할당 해 주는 값.

** number = 0,-0,NaN 항상 거짓

string = '' 거짓

object는 거짓이 없습니다. (null 제외.)

undefined과 null은 참값이 없어요.

동등비교 연산자 ==

```javascript
const a = 1004
const b = "1004"
console.log(a==b) // true... 자동으로 형변환을 시켜주고 비교를 하기 때문.

const c = 1
const d = true
console.log(c==d) // true

console.log(a+b) // 10041004
console.log(c+d) // 2

```

삼항 연산자

```javascript
console.log(true ? 1:2) // 1
console.log(false ? 1:2) // 2
```

switch 문 

```javascript
switch(expression){
    case 'first value' :{
        // do something
        [break]
    }
    case 'second value' :{
        // do something
        break
    }
    default : {
        // do something
    }
}
```

break문이 없는 경우 break문을 만나거나 default문을 실행할때까지 다음 조건문 실행.

for in 객체의 속성을 순회할때 사용

for of iterable한 객체를 순회하면 값을 꺼낼때 사용

ex)  Array, string,Map,set

for in 주로 객체의 속성을 순회할때 사용 ex) hello={ a ='a', b='b'} 이런것들! key값으로 접근한다!

for of는 재할당을 해야하기때문에 변수를 let으로 해야한다.

### 함수

```javascript
const restOpr = function (arg1,arg2,...restArgs){
    return [arg1,arg2,restArgs]
}
```

```javascript
const spreadOpr = function(arg1, arg2, arg3){
    return arg1 + arg2 + arg3
}
const = number = [1,2,3]
spreadOpr(...numbers)
```

```javascript
function add(arg1, arg2) {
    return arg1 + arg2
}
```

표현식

```javascript
const arrow1 = (name) => {
    return console.log('hi')
}
```

### String

```javascript
const str = 'a santa at nasa'

str.includes('hi') // true
str.includes('asan') // false
const str = 'a cup'
str.split() // ['a cup']
str.split('') // ['a',' ','c','u','p']
str.split(' ') // ['a','cup']
```

```javascript
str.replace(' ','-')
str.replaceAll(' ','-')
const str = '     hello     '
str.trim() // 'hello'
str.trimStart() // 'hello    '
str.trimEnd() // '    hello'
```

### Array

```javascript
const numbers=[1,2,3,4,5]

console.log(number[0]) // 1
console.log(number[-1]) // undefined
console.log(number.length) // 5
```

reverse : 원본 배열

push & pop : 가장 뒤에 추가 제거(뒤를 조짐)

unshift & shift : 가장 앞에 추가 제거(앞에 조짐)

includes : 배열에 특정값이 존재하는지  참/거짓 판별 

indexOf : 요건 인덱스반환

join : 모든 요소를 구분자를 이용하여 연결. split 반대

```javascript
const numbers=[1,2,3,4,5]

number.unshift(100)
console.log(numbers) // [100,1,2,3,4,5]

number.shift()
console.log(numbers) // [1,2,3,4,5]
```

```javascript
const numbers=[1,2,3,4,5]
let result

result = numbers.join()
console.log(result) // 1,2,3,4,5

result = numbers.join('')
console.log(result) //12345

result = numbers.join(' ')
console.log(result) // 1 2 3 4 5

result = numbers.join('-')
console.log(result) // 1-2-3-4-5
```



```javascript
const array=[1,2,3]
const newArray = [0, ...array,4]

console.log(newArray) // [0,1,2,3,4]
```

카멜케이스 - 변수, 객체, 함수 파스칼케이스 - 클래스, 생성자스네이크케이스 - 상수

Arrays배열

forEach

map

filter

reduce

find

some

every

````javascript
const fruits = ['딸기','수박','사과','체리']

fruits.forEach((fruit, index) => {
    console.log(fruit,index)
    // 딸기 0
    // 수박 1
    // 사과 2
    // 체리 3
})

const numbers = [1,2,3,4,5]
const doublenumbers = numbers.map((num) => {
    return num * 2
})
console.log(doublenumbers)

const Oddnums = numbers.filter((num) => {
    return num%2
})
console.log(oddNums) // 1,3,5

array.reduce((acc,element,index,array) =>{
    // do something
}, initialValue)

const numbers = [1,2,3]
const result = numbers.reduce((acc,num) => {
    console.log(`전 : ${acc}`) 
    return acc + num
    cosole.log(`후 : ${acc}`) // 출력x 
},0) // 하나의 값

console.log(result) // 6
// return하면 위로 돌아감!

const numbers = [1,3,5,7,9]

const hasEvenNumber = numbers.some((num) => {
    return num % 2 === 0 // 조건
})
````

### object

```javascript
const books = ['Learning JS','Learning Python']
const magazines = ['Vogue','Science']

const bookShop = {
    books,
    magazines
}

console.log(bookShop)

const obj = {
    greeting() {
        console.log('Hi')
    }
}

obj.greeting()

const key = 'regions'
const value = ['광주','대전','구미']

const ssafy = {
    [key] : value,
}
console.log(ssafy)

const UserInformation = {
    name : 'ssafy Kim',
    userId : 'ssafyStudent1234'
}

const name = UserInformation.name
const userId = UserInformaion.UserId

const {name} = UserInformation
```

JSON 자바스크립트 객체와 유사하게 생겼으나 문자열타입.

JSON.parse() => JSON => 자바스크립트 객체

JSON.stringfy() => 자바스크립트 객체 => JSON

const copy = array.CloneDeep(original)