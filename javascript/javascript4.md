```javascript
target.addEventListener('click',function)
```

충전기 road = [0]*(N+1)

road 인자에 충전기가 있는곳에 1 설치

K만큼가서 1이 없으면 뒤로 K만큼까지 뒤로 갔는데 계속 1이 없으면 0출력

1 발견하면 다시 K 만큼가고 똑같은 과정 반복. ans += 1

0 1 2 3

window console, document

const 는 참조하고 있는 곳이 안바뀐다는 소리임.

즉, dic이나 list는 참조하고있는 위치는 그대로여도 안에있는 요소들은 바꿀수가 있다는 얘기

but, boolean이나 number는 참조하고있는 위치가 const로 치면 그 요소 자체이기때문에 요소를 바꿀수가 없다.