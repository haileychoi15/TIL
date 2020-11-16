# Hook
Hook은 함수 컴포넌트에서 React state와 생명주기 기능(lifecycle features)을 “연동(hook into)“할 수 있게 해주는 함수입니다. 
> Hook은 class 안에서는 동작하지 않습니다. 대신 class 없이 React를 사용할 수 있게 해주는 것입니다.

- [useState](#useState)
- [useEffect](#useEffect)
- [useContext](#useContext)
- [useReducer](#useReducer)
- [useCallback](#useCallback)
- [useMemo](#useMemo)
- [useRef](#useRef)
- useImperativeHandle
- useLayoutEffect
- useDebugValue

<br />

## 규칙
- 최상위(at the Top Level)에서만 Hook을 호출해야 합니다.
    - 반복문, 조건문 혹은 중첩된 함수 내에서 Hook을 호출하지 마세요.
- 오직 React 함수 내에서 Hook을 호출해야 합니다.
    - React 함수 컴포넌트에서 Hook을 호출하세요.
    - Custom Hook에서 Hook을 호출하세요.

> 위 두가지 규칙을 강제하는 [eslint-plugin-react-hooks](https://www.npmjs.com/package/eslint-plugin-react-hooks) 라는 ESLint 플러그인이 있습니다.

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
useEffect 는 리액트 컴포넌트가 렌더링 될 때마다 특정 작업을 수행하도록 설정 할 수 있는 Hook 입니다.
여기서 특정 작업이란 데이터 가져오기, 구독(subscription) 설정하기, 수동으로 리액트 컴포넌트의 DOM을 수정하는 것이 될 수 있습니다.

> 리액트의 class lifecycle 메서드인 `componentDidMount`와 `componentDidUpdate`, `componentWillUnmount`가 합쳐진 것으로 생각할 수 있습니다.


- `useEffect`를 컴포넌트 안에서 구현 : effect를 통해 컴포넌트 함수 범위 안에 있는 state 변수(또는 prop)에 접근할 수 있게 됩니다. 
- `useEffect`은 매번 수행 : 기본적으로 첫번째 렌더링과 이후의 모든 업데이트에서 수행됩니다.

<br />

### 정리(Clean-up)를 이용하지 않는 Effects
리액트가 DOM을 업데이트한 뒤 추가로 코드를 실행해야 하는 경우가 있습니다.
네트워크 리퀘스트, DOM 수동 조작, 로깅 등의 경우들입니다.

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
- effect에 정리(clean-up)가 필요한 경우에는 함수를 반환합니다. 이를 `cleanup` 함수라고 부릅니다.
- 컴포넌트가 사라질 때 `cleanup` 함수가 호출됩니다.
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

<br />

#### 마운트 될 때만 실행
`useEffect`가 화면에 가장 처음 렌더링 될 때만 실행되고 업데이트 할 경우에는 실행 할 필요가 없는 경우엔 함수의 두번째 인자로 비어있는 배열을 넣어주시면 됩니다.
```jsx
  useEffect(() => {
    console.log('마운트 될 때만 실행됩니다.');
  }, []);
```

<br />

#### 특정 값이 업데이트 될 때만 실행
`useEffect`의 두번째 인자로 전달되는 배열 안에 검사하고 싶은 값을 넣어주시면 된답니다.
배열 안에는 `useState`를 통해 관리하고 있는 상태를 넣어줘도 되고, `props` 로 전달받은 값을 넣어주어도 됩니다.
```jsx
useEffect(() => {
  document.title = `You clicked ${count} times`;
  return () => {
        console.log('count 가 바뀌기 전..');
      };
}, [count]); // count가 바뀔 때만 effect를 재실행합니다.
```

<br /><br />

## `useContext`
프로젝트 안에서 전역적으로 사용 할 수 있는 값을 관리 할 수 있습니다. 이 값은 상태일 수도 있고, 함수일수도 있고, 어떤 외부 라이브러리 인스턴스일수도 있고 심지어 DOM 일 수도 있습니다.

<br />

### 1. createContext

```jsx
const UserDispatch = React.createContext(null);
```
- `createContext`의 파라미터 : Context 값을 따로 지정하지 않았을 때 기본값. 여기서는 `null`입니다.
- Context 객체 : `createContext` 의 반환 값을 담고있는 객체입니다. 여기서는 `UserDispatch` 입니다.

<br />

#### Context 객체 내보내기
```jsx
export const UserDispatch = React.createContext(null);
```
#### Context 객체 불러오기
```jsx
import { UserDispatch } from './App';
```

<br />

### 2. Context 값 설정
Context 객체 안에 Provider 라는 컴포넌트가 들어있는데 이 컴포넌트를 통하여 Context 의 값을 정할 수 있습니다. 이 컴포넌트를 사용할 때, `value` 라는 값을 설정해주면 됩니다.
```jsx
<UserDispatch.Provider value={dispatch}>
    // ...
</UserDispatch.Provider>
```

<br />

### 3. useContext
`useContext` Hook 을 사용해서 우리가 만든 Context 객체를 조회할 수 있습니다.
```jsx
import React, { useContext } from 'react';
import { UserDispatch } from './App'; /* UserDispatch를 외부에서 가져온다면 작성해주세요. */

function User({ user }) {
    const dispatch = useContext(UserDispatch);
    return <div onClick={() => {dispatch({ id: user.id, name: user.name })}} ></div>
}
```
`useContext`을 사용하여 context 객체인 `UserDispatch`의 현재 값을 `dispatch` 변수에 담습니다.
context의 현재 값은 트리 안에서 이 Hook을 호출하는 컴포넌트에 가장 가까이에 있는 `<MyContext.Provider>`의 `value` prop에 의해 결정됩니다.

- `useContext`로 전달한 인자는 context 객체 그 자체여야 합니다. (예 : `useContext(UserDispatch.id)`처럼 사용할 수 없습니다.)
- `useContext`를 호출한 컴포넌트는 context 값이 변경되면 항상 리렌더링 됩니다.
- [하위 컴퍼넌트에서 `context` 값 변경하기](https://dev.to/efearas/how-to-usecontext-and-set-value-of-context-in-child-components-in-3-steps-3j9h)

<br /><br />

## `useReducer`
`useState`의 대체 함수입니다. `useReducer`를 사용하면 컴포넌트의 상태 업데이트 로직을 컴포넌트에서 분리시킬 수 있습니다.  

<br />

### 1. reducer 함수
`reducer` 함수는 현재 상태와 액션 객체를 파라미터로 받아와서 새로운 상태를 반환해주는 함수입니다.
```jsx
function reducer(state, action) {
  // 새로운 상태를 만드는 로직
  // const nextState = ...
  return nextState;
}
```
- `state` : 현재 상태
- `action` : 업데이트를 위한 정보를 가지고 있는 객체
    - 주로 `type` 값을 지닌 객체 형태로 사용합니다.
    - `type` 값은 대문자와 `_` 로 구성하는 관습이 있습니다. (예 : `'CHANGE_INPUT'`)
- `nextState` : 컴포넌트가 지닐 새로운 상태

<br />

### 2. useReducer
```jsx
const [state, dispatch] = useReducer(reducer, initialState, init);
```
- `state` : 현재 상태
- `dispatch` : 액션을 발생시키는 함수 (예 : `dispatch({ type: 'INCREMENT' })`)
- `reducer` : `reducer` 함수
- `initialState` : 초기 상태
- `init`(optional) : 초기화 지연 함수

<br />

### 3. 예제
```jsx
import React, { useReducer } from 'react';

function reducer(state, action) {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1;
    case 'DECREMENT':
      return state - 1;
    default:
      return state;
  }
}

function Counter() {
  const [number, dispatch] = useReducer(reducer, 0);

  const onIncrease = () => {
    dispatch({ type: 'INCREMENT' });
  };

  const onDecrease = () => {
    dispatch({ type: 'DECREMENT' });
  };

  return (
    <div>
      <h1>{number}</h1>
      <button onClick={onIncrease}>+1</button>
      <button onClick={onDecrease}>-1</button>
    </div>
  );
}

export default Counter;
```

<br /><br />

## `useMemo`
`useMemo`는 의존성 값(`deps`)이 변경되었을 때에만 메모이제이션된 값만 다시 계산 할 것입니다. 이 최적화는 모든 렌더링 시의 고비용 계산을 방지하게 해 줍니다.
> `useMemo`로 전달된 함수는 렌더링 중에 실행됩니다. 랜더링 이후 특정 작업을 실행하려면 `useEffect`를 사용하세요.

```jsx
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```
- [메모이제이션](https://ko.wikipedia.org/wiki/%EB%A9%94%EB%AA%A8%EC%9D%B4%EC%A0%9C%EC%9D%B4%EC%85%98) 된 값을 반환합니다.
- 함수 안에서 참조되는 모든 값(여기서는 `a`,`b`)은 의존성 값의 배열(`deps`)에 나타나야 합니다. 
- 배열이 없는 경우 매 렌더링 때마다 새 값을 계산합니다.

<br /><br />

## `useCallback`
`useMemo`는 특정 결과값을 재사용 할 때 사용하는 반면, `useCallback` 은 특정 함수를 새로 만들지 않고 재사용하고 싶을때 사용합니다.

> `useCallback(fn, deps)`은 `useMemo(() => fn, deps)`와 같습니다.

```jsx
const memoizedCallback = useCallback(
  () => {
    doSomething(a, b);
  },
  [a, b],
);
```
- [메모이제이션](https://ko.wikipedia.org/wiki/%EB%A9%94%EB%AA%A8%EC%9D%B4%EC%A0%9C%EC%9D%B4%EC%85%98) 된 콜백을 반환합니다.
- 함수 안에서 참조되는 모든 값(여기서는 `a`,`b`)은 의존성 값의 배열(`deps`)에 나타나야 합니다. 

<br /><br />

## `useRef`
컴포넌트에서 특정 DOM 을 선택해야 할 때, 컴포넌트 안에서 조회 및 수정 할 수 있는 변수를 관리할 때 사용합니다.

<br />

### 특정 DOM 선택
- 특정 엘리먼트의 크기
- `scroll` 위치
- 특정 엘리먼트 포커스 설정
- 외부 라이브러리의 기능을 특정 DOM 에다 적용

```jsx
function example() {
  const targetInput = useRef();
  const onFocus = () => {
    targetInput.current.focus();
  }
  return (
    <div>
      <input onFocus={onFocus} ref={targetInput} />
    </div>
  );
}
```
`useRef`를 사용하여 Ref 객체를 만들고, 이 객체를 우리가 선택하고 싶은 DOM 에 `ref` 값으로 설정해주어야 합니다. 
그러면, Ref 객체의 `.current` 값은 우리가 원하는 DOM 을 가르키게 됩니다.

<br />

### 변수 관리
`useRef`로 관리하는 변수는 값이 바뀐다고 해서 컴포넌트가 리렌더링되지 않습니다. 
리액트 컴포넌트에서의 상태는 상태를 바꾸는 함수를 호출하고 나서 그 다음 렌더링 이후로 업데이트 된 상태를 조회 할 수 있는 반면, 
`useRef`로 관리하고 있는 변수는 설정 후 바로 조회 할 수 있습니다.

- `setTimeout`, `setInterval` 을 통해서 만들어진 `id`
- 외부 라이브러리를 사용하여 생성된 인스턴스
- `scroll` 위치   

```jsx
const nextId = useRef(4);
  const onCreate = () => {
    // ...
    nextId.current += 1; // 값이 변하여도, 리렌더링되지 않습니다.
  };
```
`useRef`를 사용 할 때 파라미터(여기서는 `4`)를 넣어주면, 이 값이 Ref 객체(여기서는 `nextId`)의 `.current` 값의 기본값이 됩니다. 값을 수정하거나 조회할 때는, Ref 객체의 `.current`를 사용합니다.

<br /><br />

***
#### _References_
[Hook 개요 | React](https://ko.reactjs.org/docs/hooks-overview.html) <br />
[Using the State Hook | React](https://ko.reactjs.org/docs/hooks-state.html) <br />
[Using the Effect Hook | React](https://ko.reactjs.org/docs/hooks-effect.html) <br />
[[번역] useEffect 완벽 가이드 | rinae's devlog](https://rinae.dev/posts/a-complete-guide-to-useeffect-ko)