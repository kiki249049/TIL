# React

### 1. JSX

```react
const root = document.getElementById("root")
    function Title() {
      return(
        <h3 id="title" onMouseEnter={() => console.log("mouseEnter")}>
        Hello I'm a title
        </h3>
      );
    }
    function Button() {
     return(
      <button style={{ backgroundColor: "tomato",}} onClick={() => console.log("clicked!")}>click me!</button>
     ) 
    }
    function Container () {
     return (
         <div>
            <Title/>
            <Button/>
          </div>
     )   
    }
     
    ReactDOM.render(<Container/>, root)
```

JSX component의 첫글자는 항상 대문자!

React는 이전에 렌더링된 화면과 비교하여 바뀐부분만 업데이트해준다.

### 2. setState

```react
const [data,setData] = React.useState();
// useState는 그 값을 담고있는 변수와 그것을 바꿔주는 함수를 같이 반환한다.
// [0,f]
// setData는 data를 바꾸고 자동으로 리렌더링 시켜준다.
```

```react
const root = document.getElementById("root")
    function App() {
      const [counter,setCounter] = React.useState(0);
      function countUp(){
        setCounter(current => current+1)
      }
      return(
        <div>
          <h3>Total Clicks : {counter}</h3>
          <button onClick={countUp}>Click me</button>
        </div>
      );
    }
    ReactDOM.render(<App/>, root)
```

label클릭하면 옆에 input이 선택

onChange를 달아줘야 변화를 감지가능!

```react
const [flipped, setflipped] = React.useState(false)
function onFlip(){
        setflipped(!flipped)
      }
<button onClick={onFlip}>Flipped</button>
// !flipped 기존의 상태에서 변환을 시키는 코드
```



### 3. props

커스텀 컴포넌트에 넣으면 전부 props!!  html요소에 onClick을 직접 넣는다면 그건 addEventListener!

```react
function Btn(props){
      return (
      <button 
        style={{
          backgroundColor : "tomato",
          color : "white",
          padding : "10px 20px",
          border : 0,
          borderRadius : 10,
        }}
      >{props.text}</button>)
    }
    function App() {
      return(
        <div>
          <Btn text="Save Changes" />
          <Btn text="Continue" />
        </div>
      );
    }
//props는 유일한 인자 props={text:"~~"}
function Btn({text, fontSize=14}){
      return (
      <button 
        style={{
          backgroundColor : "tomato",
          color : "white",
          padding : "10px 20px",
          border : 0,
          borderRadius : 10,
          fontSize : fontSize
        }}
      >{text}</button>)
    }
// btn props대신에 {text}를 넣어서 바로 받아오기도 가능
// fontSize 기본값 설정가능
```

### 4. memo

```react
const MemorizedBtn = React.memo(Btn)
// 이렇게하면 자식의 state가 바뀔때 새로 rerender될때 바뀐부분만 render시킨다.
return(
        <div>
          <MemorizedBtn text={value} 
            changeValue={changeValue}
          />
          <MemorizedBtn text="Continue" />
        </div>
      );
```

### 5. create-react-app

```react
npx create-react-app projectname
```

### 6. global한 css적용 원하지않을때

```react
// css파일을 만든후 원하는 js컴포넌트에서 import!
```

### 7. 필요한거면 re-render하고 싶을때 => useEffect!!

state가 바뀌면 모든 요소가 재실행된다

```react
import { useState, useEffect } from 'react';
function iRunOnlyOnce(){
    console.log("한번만!")
  }
  useEffect(iRunOnlyOnce,[]) // 두번째 인자에 리스트에는 변화를 발동시키는 변수를 입력
  return (
    <div className={styles.title}>
      <h1>{count}</h1>
      <button onClick={upupup}>click!</button>
    </div>
  );
// iRunOnlyOnce는 처음에 한번 렌더링되고 state바뀔때 재실행되지않음!
```

useEffect(changeKeyword,[keyword])라는게 있으면 changeKeyword안의 keyword가 바뀌어야 changeKeyword가 실행된다.

```react
useEffect(()=>{
    if(keyword !== "" && keyword.length >= 6){
    console.log("SEARCH FOR", keyword)}
  }, [keyword])
```

### 8. 쌩으로 3항 연산사용

```react
function Hello(){
  return <h1>Hello</h1>
}

<div>
      {showing ? <Hello/> : null}
      <button onClick={onClick}>{showing ? "Hide" : "show"}</button>
    </div>
```

### 9. cleanUp function

```react
function Hello(){
  function destroyedFn(){
    console.log("destroyed")
  }
  function effectFn(){
    console.log("created");
    return destroyedFn // 이 부분이 destroy될때 발동되는 함수!
  }
  useEffect(effectFn,[])
  return <h1>Hello</h1>
}
```

javascript는 function을 =>로 치환해서 가능

```react
function Hello(){
    <h1>Hello!!</h1>
}

function App(){
    const [showing,setShowing] = useState("false")
    const trans = () => {
        setShowing(current => !current)
    }
    return <div>
        {showing ? <Hello/> : null}
        <button>{showing ? "hide" : "show"  }</button>
    </div>
}
```

### 10. Todo추가

```react
const [todo,setTodo] = useState("")
  const [todos,setTodos] = useState([])
  const onChange = (event) => {
    setTodo(event.target.value)
  }
  const onSubmit = (event) => {
    event.preventDefault()
    if(todo === ""){
      return
    }else{
      setTodo("")
      setTodos(todos => [todo,...todos])
    }
  }
  return (
    <div>
      <h1>My Todos {todos.length}</h1>
      <form onSubmit={onSubmit}>
        <input onChange={onChange} value={todo} type="text" placeholder='Write your todo'></input>
        <button>Add To Do</button>
      </form>
    </div>
```

### React javascript를 써서 ul안에 li넣기

```react
<ul>
  {todos.map((todo,index)=> <li key={index}>{todo}</li>)}
</ul>
// 이런식으로 하게 되면 ul안에 todos안에있는 요소로 li가 자동으로 넣어지게 된다.key도 필수!
```

### select, option

```react
// html에서 목록을 보여준다!
<div>
      <h1>The Coins! {loading ? "" : `(${coins.length})`}</h1>
      {loading ? <strong>Loading...</strong> : <select>
        {coins.map((info) => <option key={info.id}>{info.name}({info.symbol}), {info.quotes.USD.price}</option>)}
      </select>}
    </div>
```

3항 연산자를 잘 쓸것!

### router

```react
import { 
  BrowserRouter as Router,
  Routes,
  Route
} from "react-router-dom"
import Home from "./routes/Home"
import Detail from "./routes/Detail"


function App() {
 return <Router>
  <Routes>
    <Route path="/" element={<Home/>}>
    </Route>
    <Route path='/movie' element={<Detail/>}>
    </Route>
  </Routes>
 </Router> 
}
// Router => 해당 URL로 이동
```

### async, await

```react
const [loading,setLoading] = useState(true);
const [movies, setMovies] = useState([])
const getMovies = async() => {
   	 const response = await fetch(
      URL
    );
    const json = await response.json()
    setMovies(json.data.movies)
    setLoading(false)
  }
```

보시다시피 fetch후 then연발과 매우 비슷하다

비동기식으로 then대신에 await를 쓰는 느낌!

### javascript 화살표 함수 주의사항

```react
const Button = () => (
<button>Hello world</button>
                     )
// 소괄호면 return이 된다!

```

```react
const Button = () => {
    <button>Hello world</button>
}

console.log(Button); // undefined
// 중괄호는 리턴이 안됨!
```

### useParams

```react

```

### useContext => vue에서의 vueX같은 역할

/context/ThemeContext.js

```react
import { createContext } from "react";

export const ThemeContext = createContext(null);
```





: 전역적인 상태관리 

```react
function App() {
  const [isDark, setIsDark] = useState(false)
  return (
    <ThemeContext.Provider value={{isDark,setIsDark}}>
      <Page isDark={isDark} setIsDark={setIsDark} />
    </ThemeContext.Provider>
    )
}
// app에서 정보 필요한 하위 컴포넌트들에게 value에 들어가 있는 정보제공
```

