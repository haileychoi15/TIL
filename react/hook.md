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

<br /><br />

***
#### _References_
[Hook 개요 | React](https://ko.reactjs.org/docs/hooks-overview.html) <br />
[Using the State Hook | React](https://ko.reactjs.org/docs/hooks-state.html) <br />
[Using the Effect Hook | React](https://ko.reactjs.org/docs/hooks-effect.html) <br />
[[번역] useEffect 완벽 가이드 | rinae's devlog](https://rinae.dev/posts/a-complete-guide-to-useeffect-ko)