### React 생태주기

```react
const mounted = useRed(false);

useEffect(){
    if(!mounted.current){
        mounted.current = true;
    }else{
        // ajax
    }
}
// 업데이트 될때만 실행하고 싶을때 이 방법을 쓴다.
// 첫번째 mounted 됐을때는 false로 가서 true로 바꿔주는 것만 실행
```

### cleanUp

```react
useEffect(() => {
    console.log('effect')
    console.log(name);
    return () => {
        console.log('cleanUp')
        console.log(name)
    }
},[]);

// cleanUp은 return 뒤에나오는 함수이고 useEffect의 뒷정리함수이다
```

