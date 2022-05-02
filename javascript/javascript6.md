표준화를 안하면 크로스 브라우징이 나타나서 망함

```javascript
const h1=document.querySelector('h1')
```

getElementId(id)

```javascript
getElementid(id)
getElementsByTagName(name)
getElementByClassName(names)
```

id - byTagName - ClassName

Element.append()

Node의 자식 NodeList중 마지막 자식 다음에 Node 객체나 DOMstring을 삽입

여러개의 Node 객체 Domstring추가 가능

Node.appendChild()

한개의 Node만 추가가능. 

만약 주어진 Node가 이미 문서에 존재하는 다른 Node를 참조하면 새로운 위치로 이동.

append는 반환값이 있지만 appendchild는 추가된 Node객체를 반환.

appendchild는 2개 넣으면 하나만 추가됨.

append는 문자열와 객체 추가가능.

HTML + Js = DOM 실제로 사용자에게 보여지는 것은 render tree.

innerHTML은 XSS(크로스사이트 스크립팅이 일어날 수 있음.)

```javascript
Element.getAttribute(attributeName)
getAttr.getAttribute('class') // class가 뭔지나옴. 'id'라치면 id가 나옴!
```

DOM 조작 

1. 선택한다

: querySelector, getElementid,getElementbyclassName,getElementbyname

2. 변경한다.

:innerText, innerHTML, element.style.color, setAttribute, 

element.classList.add('className')

element.classList.remove('className')



### Event

~하면 ~한다!

```javascript
EventTarget.addEventListener('이벤트','할일')
```



preventDefault() 기본동작을 막음.

event.preventDefault()