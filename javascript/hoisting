# 호이스팅(Hoisting)
호이스팅(Hoisting)은 선언된 모든 변수들의 선언 정보가 코드가 실행되기 전에 최상단으로 끌어올려지는 현상입니다. 함수의 경우, 표현식이 아닌 선언식으로 작성되었다면 함수 선언식이 통째로 호이스팅 됩니다.

<br />

## 함수 선언식과 표현식의 호이스팅
함수 선언식과 달리, 함수 표현식은 호이스팅되지 않습니다.


아래의 코드가 실행 될 때 
```javascript
declaration();
expression();

function declaration(){
    return 'declaration';
}

var expression = function(){
    return 'expression';
}
```
호이스팅에 의해 자바스크립트 해석기는 코드를 아래와 같이 인식합니다.

```javascript
function declaration(){
    return 'declaration';
}

var expression;

declaration(); // 'declaration'
expression(); // 오류 발생

var expression = function(){
    return 'expression';
}
```
함수가 호출이 되었을 때 함수 선언식은 호이스팅의 영향을 받아 값이 잘 출력된 것을 확인할 수 있습니다. 그러나, 함수 표현식이 호출되었을 때에는 오류가 발생했습니다. 오류메시지는 다음과 같습니다.

```html
TypeError: expression is not a function
```
이는 `expression` 선언이 변수로 인식되었기 때문입니다. 왜 그럴까요? 함수 표현식 `expression`에서 `var` 선언만 호이스팅이 적용되어 상단으로 끌어올려졌습니다. 그러나, `expression`라는 선언에 함수가 할당되기 전에 호출되었기 때문에 변수로 인식되어 오류가 발생하게 됩니다.

<br />

## `let`,`const`와 호이스팅

#### `var`

```javascript
console.log(name); // undefined

var name = 'mark';
```

#### `let`
```javascript
console.log(name); // ReferenceError

let name = 'mark';
```

`var`와 달리, `let`,`const`는 호이스팅되지 않는 것처럼 동작합니다. 그러나, 실제로 호이스팅이 되지 않는 것이 아니라 `Temporal Dead Zone`에 영향을 받기 때문에 그렇게 보이는 것인데요.

### TDZ(Temporal Dead Zone)란?
호이스팅 되었지만, (실행중인 코드에서) 아직 선언되지 않은 변수가 있는 곳을 말합니다. TDZ에 있는 변수에는 접근할 수 없으며, 변수가 선언되는 지점에 TDZ에서 나오게 됩니다.

```javascript
let letValue = 'out Scope';

function test() {
  // letValue가 TDZ에 영향을 받는 순간
  console.log('letValue', letValue); // ReferenceError
  let letValue = 'inner scope'; // letValue가 초기화 됨으로써, TDZ가 끝나게 됩니다.
};

test();
```
위의 코드에서 만약 let 변수인 `letValue`이 호이스팅 되지 않았다면, `outScope`가 출력될 것 입니다. 

그러나 실제 결과는 `ReferenceError`가 발생했습니다. 이는 호이스팅은 되었지만 아직 TDZ에 있기 때문에 접근할 수 없기 때문인데요.
실행 컨텍스트가 생성될 때 `let`/`const` 변수 선언은 Lexical Environment에 저장됩니다. 여기에 저장된 변수들은 초기화(값 바인딩)되기 전까지는 접근할 수 없는 TDZ 상태에 있게 됩니다.
여기서 변수의 초기화는 변수가 선언될 때를 의미합니다. 초기화가 되지 않은 바인딩에 접근할 때, 미리 초기화하라고 `ReferenceError` 메시지를 띄워주게 되는 것이죠.

> `var` 변수 선언은 Variable Environment에 따로 저장되며, TDZ의 영향을 받지 않습니다.


<br /><br />

***
### _References_
[함수 표현식 vs 함수 선언식 | 캡틴판교](https://joshua1988.github.io/web-development/javascript/function-expressions-vs-declarations/)
[Hoisting | MDN](https://developer.mozilla.org/ko/docs/Glossary/Hoisting)
[&#91;ES6&#93; Hoisting & Temporal Dead Zone&#40;TDZ&#41; | wrfg12.log](https://velog.io/@wrfg12/ES6-Hoisting-Temporal-Dead-ZoneTDZ)
[Don't Use JavaScript Variables Without Knowing Temporal Dead Zone | Dmitri Pavlutin](https://dmitripavlutin.com/javascript-variables-and-temporal-dead-zone/)