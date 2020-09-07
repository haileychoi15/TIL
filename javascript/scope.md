# 스코프(Scope)
현재 실행되는 `context`를 말합니다. 여기서 `context`는 값과 표현식이 표현되거나 참조 될 수 있음을 의미합니다. 
만약 변수 또는 다른 표현식이 '해당 스코프'내에 있지 않다면 사용할 수 없습니다.

<br />

자바스크립트에서 스코프(Scope)는 크게 두 가지로 나눌 수 있습니다. 
- 전역 스코프 (Global scope) : 코드 어디에서든지 참조 가능
- 지역 스코프 (Local scope or Function-level scope) : 함수 또는 코드 블록(`{ ... }`)이 만든 스코프로 함수/블록 자신과 하위 함수/블록에서만 참조

    > 자바스크립트에서 지역 스코프는 기본적으로 함수 레벨 스코프(Function-level Scope) 입니다. 다만, ES6에서 도입된 `let`, `const` 키워드로 선언된 변수는 블록 레벨 스코프(Block-level Scope)를 따릅니다.

모든 변수는 스코프를 갖습니다. 다만, 선언위치에 따라 어떤 스코프를 가지느냐가 결정되죠.
전역에서 선언된 변수는 전역 스코프를 갖는 전역 변수이고, 지역(자바스크립트의 경우 함수 내부)에서 선언된 변수는 지역 스코프를 갖는 지역 변수가 됩니다.

## 전역 스코프(Global Scope)
전역에 변수를 선언하면 이 변수는 어디서든지 참조할 수 있는 전역 스코프를 가지며, 전역 객체에 할당된 `window` 객체의 프로퍼티가 됩니다.

> 서버 사이드 환경(Node.js)에서 전역 객체는 `global` 객체 입니다.

<br /><br />

## 함수 레벨 스코프(Function-level Scope)
JavaScript는 함수 레벨 스코프를 따릅니다. 함수 내에서 선언된 변수(매개변수 포함)들은 함수 밖에서는 참조할 수 없는 지역변수가 됩니다.
> `var` 키워드로 선언한 변수가 함수 레벨 스코프를 따릅니다. `let`, `const` 키워드로 변수를 선언하면 블록 레벨 스코프를 따르게 됩니다.

```javascript
var hello = 'good morning'; // global variable

function print() {
	var bye = 'good bye'; // function-level variable(local variable)
}

console.log(hello); // good morning
console.log(bye); // undefined
```
위의 코드에서 변수 `bye`는 함수 외부에서 참조할 수 없어 `undefined`입니다.

<br /><br />

## 블록 레벨 스코프(Block-level Scope)
블록 레벨 스코프란 코드 블록 `{ ... }` 내에서 유효한 스코프를 말합니다.
ES6에서는 블록 레벨 스코프를 지원하기 위해 `let`, `const` 키워드를 도입했습니다. 이 두 키워드로 변수를 선언하면 블록 레벨 스코프를 따르게 됩니다.
> 코드 블록은 `if`, `for`, `while`, `try`/`catch` 등의 Statement에서 쓰이는 블록을 말합니다.

```javascript
function testScope(){
  let value = 'first';

  if(true){
    let value = 'second';
    console.log(value); // second
  }

  console.log(value); // first
}
```
위의 코드에서 `if`문 안에서 선언된 변수 `value`는 코드 블록 안에서만 참조가 유효합니다. 
따라서, 마지막 줄에서 출력된 `value` 값은 `first`가 됩니다. 만약 변수를 선언할 때, `let` 키워드를 쓰지 않고 `var` 키워드를 사용했다면 어떨까요?
이 때에는 `if`문 안에서 선언된 변수 `value`가 함수 레벨 스코프를 따르기 때문에 변수 `value`가 재정의 된 것 처럼 처리됩니다. 그러니, 코드 마지막 줄의 `value`의 값은 `second`가 될 것입니다.

<br /><br />


## 암묵적 전역(implicit global)
변수를 선언하지 않고 사용하면 어떻게 될까요?

```javascript
var x = 10;

function sum() {
  y = 20; // 선언하지 않은 식별자

  console.log(x + y);
}

sum(); // 30
```
위의 코드에서 `y`는 선언하지 않았기 때문에 참조 에러가 발생할 것 같지만, 마치 선언된 것처럼 동작합니다.
그 이유는 선언하지 않은 식별자에 값을 할당하면 전역 객체(`window`)의 프로퍼티가 되기 때문입니다.

<br />

`sum()` 함수가 호출되면 JavaScript 엔진은 변수 `y`에 값을 할당하기 위해 먼저 스코프 체인을 통해 선언된 변수인지 확인합니다. 
이때 변수 `y`의 선언은 찾을 수 없지만, `y = 20`을 `window.y = 20`으로 해석하여 프로퍼티를 동적 생성하게 됩니다. 실제로 변수가 아니지만 변수처럼 동작하는 것이죠.
이러한 현상을 암묵적 전역(implicit global)이라고 합니다.

> `y`는 변수가 아니므로 변수 호이스팅이 발생하지 않습니다.


***
### _References_
[Scope | MDN](https://developer.mozilla.org/en-US/docs/Glossary/Scope)  <br />
[스코프 | poiemaweb.com](https://poiemaweb.com/js-scope) <br />
[Lexical Scope and Dynamic Scope | bestalign's dev blog](https://bestalign.github.io/2015/07/12/Lexical-Scope-and-Dynamic-Scope/)
[let | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/let)
[var | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/var)