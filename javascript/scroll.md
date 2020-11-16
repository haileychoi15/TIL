# Improving scrolling performance with passive listeners

`addEventListener` 이벤트 리스너는 여러 매개변수를 가지고 있습니다. 

```js
target.addEventListener(type, listener, options);
```
- `type` : 이벤트 유형 (`click`, `scroll` ...)
- `listener` : `type`에 지정된 이벤트가 발생했을 때 실행하는 함수, `callback`으로 사용할 수 있습니다.
- `options` : 이벤트 리스너에 대한 특성을 지정하는 옵션 객체

`options`에 어떤 선택지가 있는지 살펴보겠습니다. 

<br />

## `options`
- `capture` : DOM 트리의 하단에 있는 EventTarget 으로 등록된 `listener`의 전송 여부를 나타내는 `Boolean`
- `once` : 리스너를 추가한 후 한 번만 호출함을 지정하는 `Boolean`, `true`이면 호출할 때 `listener`가 자동으로 삭제됩니다.
- `passive` : `listener`에서 지정한 함수의 `preventDefault()` 호출 여부를 나타내는 `Boolean`, `true`이면 호출하지 않습니다.

이 중에서 `passive`는 `scroll`의 성능 향상과 관련이 있는데요, 어떻게 `passive`가 영향을 줄 수 있는지 알아보겠습니다. 

<br />

### `scroll jank`
아마 모바일에서 페이지를 스크롤 할 때 손가락의 움직임에 비해 스크롤이 지연되는 경우를 경험하신 적이 있을 텐테요.
이것을 `scroll jank`라고 부릅니다. `scroll jank`의 주된 원인은 보통 `touch event listener`입니다.
현재 브라우저는 `touch event listener`가 스크롤을 취소할지 아닐지 알 수 없습니다. 따라서, 브라우저는 페이지를 스크롤 하기 전에
`listener`가 끝났는지 항상 기다려야합니다. 그래서 이 기다림 때문에 `scroll jank`가 발생하는 것이죠.
이 문제를 `passive` 옵션을 통해 해결 할 수 있습니다.

<br />

### `passive` option
```js
target.addEventListener(type, listener, { passive: true });
````
`listener` 옵션에서 `passive`를 `true`로 지정하는 것인데요, 이렇게 하면 `listener`가 스크롤을 취소하지 않을 거라고 브라우저에게 알려줍니다.
그렇게 때문에 페이지 스크롤이 발생했을 때, 브라우저는 `listener`가 끝나기를 기다리지 않고 바로 스크롤을 실행합니다.

> 베이직한 `scroll`이벤트는 취소 될 수 없기 때문에(cannot be canceled), `passive`를 꼭 지정할 필요는 없습니다. 그러나, 지정하여서 expensive work을 미리 방지한다면 좋겠죠?

<br />
<br />

#### References
    
[EventTarget.addEventListener() | MDN](https://developer.mozilla.org/ko/docs/Web/API/EventTarget/addEventListener) <br />
[Improving Scroll Performance with Passive Event Listeners | Kayce Basques](https://developers.google.com/web/updates/2016/06/passive-event-listeners) <br />
