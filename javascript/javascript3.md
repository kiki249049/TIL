for문 (초기값, 종료조건, 증가량)

for .. in  : key들을 순회할때 사용

```javascript
const bestMovie = {
  title: '벤자민 버튼의 시간은 거꾸로 간다',
  releaseYear: 2008,
  actors: ['브래드 피트', '케이트 블란쳇'],
  genres: ['romance', 'fantasy'],
}
for(let value in bestMovie){
  console.log(`${value} : ${bestMovie[value]}`)
}
```

for .. of : 반복가능한 객체를 순회하며 값을 꺼낼때

```javascript
const movies = [
  {title: '어바웃 타임'},
  {title: '굿 윌 헌팅'},
  {title: '인턴'},
]
for(let value of movies){
  console.log(value.title)
}
// for in 으로 value를 돌면 value가 안의 객체로 안나오고 숫자로 나온다.
```

선언식 function

```javascript
function isValid(password) {
    if(..){
        
    }
}
```

shift & pop -> 빼는거

unshift & push -> 넣는것

콜백함수 사용

map, reduce, forEach,find

str.split('').reverse().join('')