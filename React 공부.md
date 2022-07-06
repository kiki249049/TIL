1. React

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
   
   !
   
   ### 3. props
   
   ```react
   
   ```
   
   
