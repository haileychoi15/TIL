# Hook
Hook은 함수 컴포넌트에서 React state와 생명주기 기능(lifecycle features)을 “연동(hook into)“할 수 있게 해주는 함수입니다. 
> Hook은 class 안에서는 동작하지 않습니다. 대신 class 없이 React를 사용할 수 있게 해주는 것입니다.

- [useState](https://ko.reactjs.org/docs/hooks-reference.html#usestate)
- [useEffect](https://ko.reactjs.org/docs/hooks-reference.html#useeffect)
- [useContext](https://ko.reactjs.org/docs/hooks-reference.html#usecontext)
- [useReducer](https://ko.reactjs.org/docs/hooks-reference.html#usereducer)
- [useCallback](https://ko.reactjs.org/docs/hooks-reference.html#usecallback)
- [useMemo](https://ko.reactjs.org/docs/hooks-reference.html#usememo)
- [useRef](https://ko.reactjs.org/docs/hooks-reference.html#useref)
- [useImperativeHandle](https://ko.reactjs.org/docs/hooks-reference.html#useimperativehandle)
- [useLayoutEffect](https://ko.reactjs.org/docs/hooks-reference.html#uselayouteffect)
- [useDebugValue](https://ko.reactjs.org/docs/hooks-reference.html#usedebugvalue)

<br /><br />

## `useState`
`useState`는 state를 함수 컴포넌트 안에서 사용할 수 있게 해줍니다.
```jsx
import React, { useState } from 'react';

function Example() {
  // 새로운 state 변수를 선언하고, 이것을 count라 부르겠습니다.
  const [count, setCount] = useState(initialValue);
```
- `count` : 현재상태를 나타내는 변수
- `setCount` : `count` 변수의 값을 갱신하는 함수
- `initialValue` : `state`의 초기값

<br /><br />

## `useEffect`
`useEffect`를 사용하면 함수 컴포넌트에서 `side effect`를 수행할 수 있습니다.
데이터 가져오기, 구독(subscription) 설정하기, 수동으로 리액트 컴포넌트의 DOM을 수정하는 것까지 이 모든 것이 `side effects`입니다.

> 리액트의 class lifecycle 메서드인 `componentDidMount`와 `componentDidUpdate`, `componentWillUnmount`가 합쳐진 것으로 생각할 수 있습니다.

<br />

### 정리(Clean-up)를 이용하지 않는 Effects
리액트가 DOM을 업데이트한 뒤 추가로 코드를 실행해야 하는 경우가 있습니다.
네트워크 리퀘스트, DOM 수동 조작, 로깅 등의 경우들입니다.

- `useEffect`를 컴포넌트 안에서 구현 : effect를 통해 컴포넌트 함수 범위 안에 있는 state 변수(또는 prop)에 접근할 수 있게 됩니다. 
- `useEffect`은 매번 수행 : 기본적으로 첫번째 렌더링과 이후의 모든 업데이트에서 수행됩니다.

```jsx
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  // componentDidMount, componentDidUpdate와 같은 방식으로
  useEffect(() => {
    // 브라우저 API를 이용하여 문서 타이틀을 업데이트합니다.
    document.title = `You clicked ${count} times`;
  });
```
위의 코드는 state 변수를 선언한 뒤 리액트에게 effect를 사용함을 말하고 있습니다. `useEffect` Hook에 함수를 전달하고 있는데 이 함수가 바로 effect입니다.

<br />

### 정리(clean-up)를 이용하는 Effects
- effect에 정리(clean-up)가 필요한 경우에는 함수를 반환합니다.
- 리액트는 컴포넌트가 마운트 해제되는 때에 정리(clean-up)를 실행합니다. 
- 매 랜더링 때마다 다음 차례의 effect를 실행하기 전에, 이전의 렌더링에서 파생된 effect를 정리합니다.


친구의 온라인 상태를 구독할 수 있는 ChatAPI 모듈의 예를 들어보겠습니다. 친구의 상태를 구독(subscribe)하고 보여주는 코드입니다.
```jsx
import React, { useState, useEffect } from 'react';

function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    // effect 이후에 어떻게 정리(clean-up)할 것인지 표시합니다.
    return function cleanup() {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```
구독(subscription)의 추가와 제거가 모두 하나의 effect를 구성하는 것입니다.

<br />

### 성능 최적화
특정 값들이 리렌더링 시에 변경되지 않는다면 리액트로 하여금 effect를 건너뛰도록 할 수 있습니다. 

- `useEffect`의 두 번째 인자(optional)로 배열을 넘기면 됩니다.
- 배열이 컴포넌트 범위 내에서 바뀌는 값들과 effect에 의해 사용되는 값들을 모두 포함해야 합니다.

#### 정리(Clean-up)를 이용하지 않는 Effects
```jsx
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]); // count가 바뀔 때만 effect를 재실행합니다.
```

#### 정리(clean-up)를 이용하는 Effects
```jsx
useEffect(() => {
  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
  return () => {
    ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
  };
}, [props.friend.id]); // props.friend.id가 바뀔 때만 재구독합니다.
```

<br /><br />

***
#### _References_
[Hook 개요 | React](https://ko.reactjs.org/docs/hooks-overview.html) <br />
[Using the State Hook | React](https://ko.reactjs.org/docs/hooks-state.html) <br />
[Using the Effect Hook | React](https://ko.reactjs.org/docs/hooks-effect.html) <br />