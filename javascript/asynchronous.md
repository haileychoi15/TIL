# 비동기적 처리(Asynchronous programming)
특정 코드의 로직이 끝날 때까지 코드의 실행을 멈추지 않고 다음 코드를 먼저 실행하는 자바스크립트의 특성을 의미합니다.

<img width="500" alt="스크린샷 2020-09-08 오후 5 41 19" src="https://user-images.githubusercontent.com/60546778/92453845-b8a28c80-f1fa-11ea-97c1-129e115c8477.png">

<br />
<br />

- `ajax` 통신
- `setTimeout()`

```javascript
function work() {
  setTimeout(() => {

    const start = Date.now();
    for (let i=0; i < 1000000000; i++){
      
    }   
    const end = Date.now();
    console.log(end - start + 'ms'); // 512ms

  }, 0)
}

console.log('작업 시작');
work();
console.log('다음 작업');
```

비동기적 처리를 이해하지 못했다면, 위의 코드에서 작업 실행 순서는
```javascript
작업 시작 -> 512ms -> 다음 작업
```
이렇게 예상할 수 있을 것입니다. 그러나, 실제 작업 실행 순서는
```javascript
작업 시작 -> 다음 작업 -> 512ms
```
이라는 결과가 나옵니다. `work()`가 호출되고 작업이 이루어지는 동안 다른 작업(여기서는 `console.log('다음 작업')`) 또한 시행되기 때문이죠.

<br />

그렇다면 이전 단계 비동기 작업이 성공하고 나서 그 결과값을 이용하여 다음 비동기 작업을 실행해야 하는 경우 어떻게 해야할까요?
아래의 방법들이 해결방법이 될 수 있습니다. 

- [`callback`](#callback)
- [`promise`](#promise) (ECMAScript 2015에 추가)
- [`async`/`await`](#asyncawait) (ECMAScript 2017에 추가)

<br />

## `Callback` 
작업을 실행하는 함수의 파라미터에 `callback`을 사용할 수 있습니다.

```javascript
function work(callback) {
  setTimeout(() => {

    const start = Date.now();
    for (let i=0; i < 1000000000; i++){
      
    }   
    const end = Date.now();
    console.log(end - start + 'ms'); // 512ms
    callback(end - start); //  callback의 파라미터에 작업 결과를 넣어준다.

  }, 0)
}

console.log('작업 시작');

work((time) => {
  console.log(`작업하는데 걸린 시간은 ${time}ms 입니다.`)
});

console.log('다음 작업');
```
위의 코드에서 작업 실행 순서는 비동기적 처리에 의해
```javascript
작업 시작 -> 다음 작업 -> 512ms -> 작업하는데 걸린 시간은 512ms 입니다.
```
이렇게 됩니다. 이 과정에서 `work()`의 작업 결과를 `callback`을 통해 불러와서 `작업하는데 걸린 시간은 512ms 입니다.` 이라는 작업을 수행하였습니다.

<br />

그러나, 이 방법은 코드량이 많거나 작업을 반복 수행해야 할 때 코드를 복잡하게 만들 수 있습니다. 
따라서, ES6에서 도입된 `promise` 또는 `async`/`await` 을 사용하기를 권장합니다.

<br /><br />

## `Promise` 
`Promise`는 비동기 작업의 최종 완료 또는 실패를 나타내는 객체입니다. 기본적으로 `Promise`는 함수에 콜백을 전달하는 대신에, 콜백을 첨부하는 방식의 객체입니다.
> IE 지원 X

<br />

`Promise()`객체를 생성하는 것은 `setTimeout()`처럼 이미 프로미스를 지원하지 않는 함수를 감쌀 때 주로 사용합니다. 하지만 이 사실과 별개로 사용할 수도 있습니다.

```javascript
const myPromise = new Promise((resolve, reject) => {
  // 구현 ...
})

myPromise.then(() => {
  // 구현 ...
}).catch(() => {
  // 구현 ...
})
```
- `resolve` : `Promise`가 성공 했을 때 호출되는 함수
- `reject` : `Promise`가 실패 했을 때 호출되는 함수
- `then()` : 새로운 `promise`를 반환(처음에 만들었던 `promise`와는 다른 새로운 `promise`)
    - `then()`에 넘겨지는 인자는 선택적(optional)
- `catch()` : `then(null, reject)` 의 축약

<br />

### 상태 
`new Promise()`로 생성된 `promise`는 다음 중 하나의 상태를 가집니다.

- 대기(Pending) : 비동기 처리 로직이 아직 완료되지 않은 상태
- 이행(Fulfilled) : 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태
- 실패(Rejected) : 비동기 처리가 실패하거나 오류가 발생한 상태

<br />

#### 대기(Pending)

```javascript
new Promise();
```

위의 코드 처럼 `new Promise()` 메서드를 호출하면 대기 상태가 됩니다. 이 때 콜백 함수를 선언할 수 있고, 콜백 함수의 인자는 `resolve`, `reject`입니다.

```javascript
new Promise((resolve, reject) => {
  // 구현 ...
});
```

<br />

#### 이행(Fulfilled)
콜백 함수의 인자 `resolve`를 아래와 같이 실행하면 이행 상태가 됩니다.
```javascript
new Promise(function(resolve, reject) {
  resolve();
});
```

그리고 이행 상태가 되면 아래와 같이 `then()`을 이용하여 처리 결과 값을 받을 수 있습니다.
```javascript
function getData() {
  return new Promise(function(resolve, reject) {
    let data = 100;
    resolve(data);
  });
}

// resolve()의 결과 값 data를 resolvedData로 받습니다.
getData().then((resolvedData) => {
  console.log(resolvedData); // 100
});
```
> `promise`의 이행 상태를 완료라고 표현할 수 있습니다.

<br />

#### 실패(Rejected)
콜백 함수 인자 `resolve`와 `reject`중에 `reject`를 아래와 같이 호출하면 실패 상태가 됩니다.
```javascript
new Promise(function(resolve, reject) {
  reject();
});
```

그리고 실패 상태가 되면 에러(실패 처리의 결과 값)를 `catch()`로 받을 수 있습니다.

```javascript
function getData() {
  return new Promise(function(resolve, reject) {
    reject(new Error("Request is failed"));
  });
}

// reject()의 결과 값 Error를 e로 받습니다.
getData().then().catch(function(e) {
  console.log(e); // Error: Request is failed
});
```

에러는 `then()`의 두번째 인자로 처리할 수도 있습니다. 그러나 이 방법은 `then()`의 첫번째 콜백함수 내부에서 발생한 오류는 잡아내지 못할 수 있습니다. 
따라서, 예외처리는 `catch()`를 사용할 것을 권장합니다.
 
<br />

### 속성과 매서드

- `legnth` : 값이 언제나 `1`인 길이 속성
- `prototype` : `Promise` 생성자의 프로토타입
- `all()` : [별도정리](#promiseall)
- `race()` : [별도정리](#promiserace)
- `reject()`
- `resolve()`

<br />

#### 프로토타입 매서드

- `catch()`
- `then()`
- `finally()`

<br />

### 예제

```javascript
function increaseAndPrint(n) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const value = n + 1;
      if (value === 3){
        const error = new Error();
        error.name = 'ValueFiveError';
        reject(error);
        return;
      }
      console.log(value);
      resolve(value);
    }, 1000)
  });
}

increaseAndPrint(0).then(increaseAndPrint)
.then(increaseAndPrint)
.then(increaseAndPrint)
.catch(e => { // n = 3 인 경우
  console.error(e); // ValueFiveError 발생
})
```
위의 코드의 결과는 아래와 같습니다.
```javascript
// 1
// 2
// ValueFiveError
```

<br />

이번에는 로그인 인증 로직을 예제로 들어보겠습니다.

```javascript
let user = {
  id: 'imdud12@gmail.com',
  pw: '******'
};

function processValue1() {
  return new Promise({
    // ...
  });
}
function processValue2() {
  return new Promise({
    // ...
  });
}
function processValue3() {
  return new Promise({
    // ...
  });
}

getData(user)
  .then(processValue1)
  .then(processValue2)
  .then(processValue3);
```

위의 예제를 보면 `then()`을 여러번 사용하였습니다. 
순차적으로 각각의 비동기적 단계가 실행되는 것을 `promise chain`이라고 합니다.

> `then()`을 사용할 때는 반환값이 반드시 있어야 합니다. 만약 없다면, 콜백 함수가 이전의 `Promise`의 결과를 받지 못합니다.

`promise chain`에서 작업이 실패한 후에도 새로운 작업 수행이 가능할까요?
이것은 `promise`의 아주 유용한 장점입니다. 아래의 예시를 살펴보시죠.

```javascript
new Promise((resolve, reject) => {
    console.log('Initial');

    resolve();
})
.then(() => {
    throw new Error('Something failed');
        
    console.log('Do this');
})
.catch(() => {
    console.log('Do that');
})
.then(() => {
    console.log('Do this, whatever happened before');
});
```
그러면 다음 텍스트가 출력됩니다.

```javascript
// Initial
// Do that
// Do this, whatever happened before
```
`Do this`가 출력되지 않았습니다. `Something failed` 에러가 `rejection`을 발생시켰기 때문입니다. 그러나 `catch()`를 사용해 해결하고 다음 작업들을 이어나갑니다.

### 문제점

`Promise` 또한 불편한 점들이 있습니다. `then()`이 여러번 쓰이다 보면 어떤 단계에서 오류가 발생한지 파악하기 어렵습니다. 또한 `then()`이 이어져 있기 때문에 특정 조건에 따라 분기를 나누는 작업 또한 어렵습니다.

<br /><br />

## `async`/`await` 
기존의 비동기 처리 방식들의 단점을 보완하고 개발자가 읽기 좋은 코드를 작성할 수 있게 도와주기 위해서 ES8 에 추가된 문법입니다. `async` 함수는 `Promise` 객체를 반환합니다.
> IE 지원 X
>
<br />

```javascript
async function 함수명() {
  await 비동기_처리_메서드_명();
}
```

<br />

### 예외 처리
`async`/`await` 문법에서 예외처리는 `try`/`catch`문을 사용합니다.

```javascript
async function 함수명() {
  
  try {
    await 비동기_처리_메서드_명();
  } catch (e) {
    // ...
  }
}
```

<br />

### 예제
여기 `async`/`await`를 사용하지 않은 코드 예제가 있습니다.
```javascript
function process() {

  // fetchUser()라고 하는 코드는 서버에서 데이터를 받아오는 HTTP 통신 코드라고 가정합니다.
  let user = fetchUser('server.com/user/info');
  if (user.id === 1) {
    console.log(user.name);
  }
}
```

위의 코드에서 `fetchUser()`의 결과값을 변수 `user`에 넣어 사용하려면 `callback`을 사용해야합니다. 아래의 코드처럼 말이죠.

```javascript
function process() {

  fetchUser('server.com/user/info', user => {
    if (user.id === 1) {
      console.log(user.name);
    }
  });
}
```

`async`/`await`을 사용하면 `callback`을 사용하지 않고 이러한 처리를 할 수 있습니다.
```javascript
async function process() {

  await fetchUser('server.com/user/info');
  if (user.id === 1) {
    console.log(user.name);
  }
}
```

<br />

다른 예제를 살펴보겠습니다.

```javascript
function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function makeError() {
  await sleep(1000);
  const error = new Error();
  throw error;
}


async function process() {
  console.log('hello');
  await sleep(1000);
  console.log('nice to meet you');
 
  return 'bye'
}

process().then(value => {
  console.log(value); // bye
});

// hello
// nice to meet you (hello가 출력되고 1000ms 뒤에 출력)
// bye
```

`async` 함수는 `Promise` 객체를 반환하기 때문에 위의 예제처럼 결과 값을 `then()`에서 인자로 받아와 사용할 수 있습니다. 

<br /><br />

## `Promise.all()`
`Promise.all()`은 여러 `promise`의 결과를 집계할 때 유용하게 사용할 수 있습니다.

```javascript
Promise.all(iterable);
```
- `iterable` : `Array`와 같이 순회 가능한(iterable) 객체

<br />

### 특징
- `Promise.all()`은 배열 내 모든 값의 이행하고 결과 값을 배열(`Array`)에 담아 반환합니다.
- 등록하는 객체에 `promise`가 아닌 값이 들어있어도, 이행 시 결과 배열에는 포함합니다.
- 주어진 `promise` 하나라도 `reject()`가 있다면, 다른 `promise`의 이행 여부와 상관없이 거부합니다.
    - 발생할 수 있는 거부를 사전에 처리해(`catch()` 사용) 동작 방식을 바꿀 수 있습니다.

<br />

### 예제
```javascript
function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

const getDog = async () => {
  await sleep(1000);
  return '멍멍이';
}

const getRabbit = async () => {
  await sleep(500);
  return '토끼';
}

const getTurtle = async () => {
  await sleep(3000);
  return '거북이';
}

async function process() {
  const [dog, rabbit, turtle] = await Promise.all([getDog(), getRabbit(), getTurtle()]);   

  console.log(dog); // 멍멍이
  console.log(rabbit); // 토끼
  console.log(turtle); // 거북이
}

process();
```
`Promise.all`은 각각의 `promise`가 처리되는 시간은 다르지만 제일 마지막으로 작업이 끝나는 `promise` 기준으로, 모든 `promise`가 이행된 이후에 결과값들을 배열에 담아 반환합니다.

<br />

`Promise.race`를 쓰게 되면 등록된 `promise` 중 가장 따른 `promise`의 결과값만 반환됩니다. 그렇다면 `process()`을 호출하는 부분의 코드가 이렇게 바뀌겠네요.

```javascript
async function process() {
  const first = await Promise.all(getDog(), getRabbit(), getTurtle());   

  console.log(first); // 토끼
}

process();
```

<br /><br />
***
### _References_
[General asynchronous programming concepts | MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Concepts) <br />
[Promise | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise) <br />
[Using promises | MDN](https://wiki.developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Using_promises) <br />
[Promise.prototype.then() | MDN](https://wiki.developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/then) <br />
[async function | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function) <br />
[자바스크립트 비동기 처리와 콜백 함수 | Captain Pangyo](https://joshua1988.github.io/web-development/javascript/javascript-asynchronous-operation/) <br />
[자바스크립트 Promise 쉽게 이해하기 | Captain Pangyo](https://joshua1988.github.io/web-development/javascript/promise-for-beginners/) <br />
[자바스크립트 async와 await | Captain Pangyo](https://joshua1988.github.io/web-development/javascript/js-async-await/) <br />