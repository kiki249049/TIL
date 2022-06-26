# React공부

JSX는 className으로 class를 지정.

```react
// 중괄호 문법
function App () {
    let post = '강남우동 맛집'
    return <div>{ post }</div>
}
```

```react
// style 넣기
function App () {
    let post = '강남우동 맛집'
    return <div style={ { color : 'red', fontSize : '16px' } }>{ post }</div>
}
```

### useState(매우 중요!!)

```react
// style 넣기
import { useState } from 'react';

function App () {
    let post = '강남우동 맛집';
    let [글제목,b] = useState('남자 코트 추천')
    // useState에는 ['남자 코트 추천', 함수]
    // 글제목에는 남자 코트추천이 b에는 그것을 바꿀 수 있는 함수가 들어가 있다.
    return <div style={ { color : 'red', fontSize : '16px' } }>{ post }</div>
}
```

state쓰는 이유?? 그냥 post를 바꾼다고하면 새로고침을 해야 적용이 되는데 state를 사용하면 새로고침을 안해도 폰app처럼 적용이 된다.

### onClick

```react
// onClick안에는 무조건 함수!
function likeUp(){
    내용기입.
}

<div className='list'>
        <h4 style={ {fontWeight:'bold'} }>{ 글제목[0] } <span onClick={ likeUp } >👍</span> {좋아요} </h4>
        <p>2월 17일 발행</p>
      </div>
```

### useState로 state 변경할떄 유의점

: 기존state === 신규 state의 경우 변경을 해주지 않는다.

```react
// 바로 바뀌지 않는 경우.
let [글제목, setTitle] = useState(['남자 코트 추천','강남 우동 맛집','파이썬 독학']);
<button onClick={ () => { 
        let copy = 글제목 // copy한것
        copy[0] = '여자코트 추천'
        setTitle(copy)}}>글 수정</button>
// 바로 바뀌는것.
<button onClick={ () => { 
        let copy = [...글제목] // copy한것
        copy[0] = '여자코트 추천'
        setTitle(copy)}}>글 수정</button>
```

왜 바로 바뀌지 않느냐? 

array object특징때문

```react
// arr에는 [1,2,3]이 저장이 되는게 아니라 [1,2,3]을 가리키는 위치가 저장이 됨.
let arr = [1,2,3]
// 바로 바뀌지 않는 경우.
let [글제목, setTitle] = useState(['남자 코트 추천','강남 우동 맛집','파이썬 독학']);
<button onClick={ () => { 
        let copy = 글제목 // copy한것
        copy[0] = '여자코트 추천'
        setTitle(copy)}}>글 수정</button>
// 이런식으로 하게 되면 copy에 내용은 바뀌었지만 화살표는 바뀌지 않아 state는 변경점이 없다고 생각하여 바뀌지않음.
// console.log(copy === 글제목) 해보면 true가 나온다.
```

그래서 copy = [...글제목] 하게 되면 화살표도 바꿔줌

...이 괄호를 벗겨주라는 의미

### component 만들기

```react
function Modal(){
  return (
    <div className='modal'>
        <h4>제목</h4>
        <p>날짜</p>
        <p>상세내용</p>
      </div>
  )
}
```

따로 function으로 정의해서 원하는 곳에 <Modal>이런식으로 사용

첫번째 알파벳은 무조건 대문자!!



어떤걸 컴포넌트로 만들면 좋은가?

1. html 반복적으로 축약할때
2. 큰 페이지들
3. 자주 변경되는 것들
