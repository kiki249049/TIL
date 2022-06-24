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
