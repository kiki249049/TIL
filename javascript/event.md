**이벤트의 종류**

- User Interface Events
  - load
  - unload
  - error
  - select
- Focus Events
  - focusin
  - focus
  - focusout
  - blur
- Mouse Events
  - onclick
  - ondbclick
  - onmousedown
  - onmouseup
  - onmouseover
- Input Events
  - input
  - beforeinput
- Keyboard Events
  - keyup
  - keydown
  - keypress

## EventListener

These objects implement the `EventTarget` interface and can therefore add event listeners to observe events by calling `addEventListener()`

- 이벤트 객체들은 `EventTarget` 인터페이스를 구현하기 때문에 `addEventListener` 메서드를 호출하여 이벤트를 관찰 가능
- 이벤트의 발생과 더불어 수행해야 하는 일을 콜백 함수를 통해 지정
- "특정한 이벤트가 발생하면, 할 일을 등록"하는 구조
- Django 예시
  - url 요청 → 이벤트
  - view의 매핑된 함수 → 콜백 함수