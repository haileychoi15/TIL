# Error
React 프로젝트를 진행하면서 발생한 문제상황과 여러가지 오류들에 대한 기록 노트입니다. 아래는 정리되어 있는 주제들의 제목을 나열한 목록입니다.

<br />

- `window.addEventListener`

<br /><br />

## `window.addEventListener`

### 상황

한 컴포넌트에서 `window` 객체에 이벤트리스너를 등록하였는데, 이 컴포넌트가 쓰이지 않는 다른 페이지에서도 이벤트리스너가 작동하는 상황. <br />
이벤트리스너의 실행함수에는 `state`를 바꾸는 로직이 포함되어 있어 아래와 같은 오류가 발생했다. 

### 오류

```text
Can't perform a React state update on an unmounted component. This is a no-op, but it indicates a memory leak in your application. To fix, cancel all subscriptions and asynchronous tasks in a useEffect cleanup function.
```

### 해결

- [cleanUp 함수 사용법](https://velog.io/@ohgoodkim/-%EC%97%90%EB%9F%AC%EB%85%B8%ED%8A%B8-Cant-perform-a-React-state-update-on-an-unmounted-component) <br />
- [stackoverflow 의 여러 가지 해결 방법](https://stackoverflow.com/questions/32896624/react-js-best-practice-regarding-listening-to-window-events-from-components) <br />

내가 위의 문서들을 참고하여 해결한 방법은 아래와 같다. 컴포넌트가 unmounted 되기 직전에 cleanUp 함수를 이용하여 `window` 객체의 이벤트리스너를 제거하였다.

```jsx
useEffect(() => {
        window.addEventListener('scroll', 실행함수);
        return () => window.removeEventListener('scroll', 실행함수); // cleanUp 함수 사용
    }, []);
```

<br /><br />

***
#### _References_
- [❗️📚 에러노트 - Can't perform a React state update on an unmounted component | ohgoodkim](https://velog.io/@ohgoodkim/-%EC%97%90%EB%9F%AC%EB%85%B8%ED%8A%B8-Cant-perform-a-React-state-update-on-an-unmounted-component) <br />
- [React.js best practice regarding listening to window events from components | stackoverflow](https://stackoverflow.com/questions/32896624/react-js-best-practice-regarding-listening-to-window-events-from-components) <br />
