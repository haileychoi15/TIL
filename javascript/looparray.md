# 반복문(Loop statement)과 배열(Array)
자바스크립트의 반복문의 종류와 배열의 여러 속성들을 다루고 있는 문서입니다.
- [반복문(Loop Statement)](#반복문loop-statement)
- [배열 내장 매서드(Methods)](#배열-내장-매서드methods)

<br />

## 반복문(Loop Statement)

<br />

### `for`
`for` 반복문은 어떤 특정한 조건이 거짓으로 판별될 때까지 반복합니다.
```html
for ([초기문]; [조건문]; [증감문])
  문장
```

<br />

#### 예제
```javascript
let str = '';

for (let i = 0; i < 9; i++) {
  str = str + i;
}

console.log(str); // '0123455678'
```

```javascript
let i = 0;

for (;;) {
  if (i > 3) break;
  console.log(i);
  i++;
}
```
초기문, 조건문, 증감문 모두 생략가능합니다. 이때에는 `break` 문을 사용해 반복을 탈출할 수 있도록 조건을 추가해야 합니다.  

<br /><br />

### `do ... while`
특정한 조건이 거짓으로 판별될 때까지 반복합니다.
```javascript
do
  문장
while (조건문);
```
조건문을 확인하기 전에 문장은 한번 실행됩니다. 그리고 매 실행 마지막마다 조건문이 확인됩니다. 조건문이 참이라면, 문장은 다시 실행됩니다. 조건문이 거짓이라면, 실행을 멈추고 `do...while` 문 바로 아래에 있는 문장으로 넘어가게 합니다.

<br />

#### 예제
다음 예제에서, `do` 반복문은 최소 한번은 반복됩니다. 그리고 i 가 5보다 작지 않을 때까지 계속 반복됩니다.
```javascript
do {
  i += 1;
  console.log(i);
} while (i < 5);
```

<br /><br />

### `while`
`while` 문은 어떤 조건문이 참이기만 하면 문장을 계속해서 수행합니다.
```javascript
while (조건문)
  문장
```
만약 조건문이 거짓이 된다면, 그 반복문 안의 문장은 실행을 멈추고 반복문 바로 다음의 문장으로 넘어갑니다.
조건문은 항상 참이되는 것은 피해야 합니다. 그 반복문은 무한 루프가 되기 때문이죠.

<br />

#### 예제
다음 `while` 반복문은 n이 3보다 작은 한, 계속 반복됩니다.
```javascript
n = 0;
x = 0;
while (n < 3) {
  n++;
  x += n;
}
```

<br /><br />

### `for ... of`
 반복가능한 객체 (`Array`, `Map`, `Set`, `String`, `TypedArray`, `arguments` 객체 등을 포함)에 대해서 반복합니다.
```javascript
for (variable of iterable) {
  statement
}
```
- `variable` : 각 반복에 서로 다른 속성값이 variable에 할당
- `iterable` : 반복되는 열거가능(enumerable)한 속성이 있는 객체

<br />

#### `Array` 객체 예제
```javascript
let iterable = [10, 20, 30];

for (const value of iterable) {
  console.log(value);
}
// 10
// 20
// 30
```

#### `String` 객체 예제
```javascript
let iterable = "boo";

for (let value of iterable) {
  console.log(value);
}
// "b"
// "o"
// "o"
```

#### DOM 컬렉션 예제
[`NodeList`](https://developer.mozilla.org/ko/docs/Web/API/NodeList) 같은 DOM 컬렉션에 대해 반복할 수 있습니다. 

```javascript
// 주의: 이는 NodeList.prototype[Symbol.iterator]가
// 구현된 플랫폼에서만 작동합니다
let articleParagraphs = document.querySelectorAll("article > p");

for (let paragraph of articleParagraphs) {
  paragraph.classList.add("read");
}
```
위의 예제에서 `article`의 직계 자손인 `paragraph`에 `read` 클래스를 추가합니다.

<br /><br />

### `for ... in`
임의의 순서로 객체의 속성들에 대해 반복합니다.([Symbol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol) 로 키가 지정된 속성은 무시합니다.)
> `for...in`은 인덱스의 순서가 중요한 `Array`에서 반복을 위해 사용할 수 없습니다. 배열이 데이터의 저장에 있어서는 더 실용적이지만, `키-값 쌍`이 선호되는 데이터의 경우 for...in을 사용할 수 있습니다.

> 만약 객체의 프로토타입이 아닌 객체 자체에 연결된 속성만 고려한다면 [`hasOwnProperty()`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty) 를 사용하세요.

```javascript
for (variable in object) { ... }    
```
- `variable` : 매 반복마다 다른 속성 이름(Value name)이 변수(variable)로 지정
- `object` : 반복 작업을 수행할 객체로 열거형 속성을 가지고 있는 객체

<br />

#### 예제
```javascript
let object = {a: 1, b: 2, c: 3};
    
for (const key in object) {
  console.log(`object.${key} = ${object[key]}`);
}

// 'object.a = 1'
// 'object.b = 2'
// 'object.c = 3'
```

<br /><br />

## 배열 내장 매서드(Methods)
- `from()`
- `isArray()`
- `of()`
- [`concat()`](#concat)
- `copyWithin()`
- `entries()`
- `every()`
- `fill()`
- [`filter()`](#filter)
- `find()`
- `findIndex()`
- `flat()`
- `flatMap()`
- [`forEach()`](#foreach)
- [`includes()`](#includes)
- `indexOf()`
- `join()`
- `keys()`
- `lastIndexOf()`
- [`map()`](#map)
- [`reduce()`](#reduce)
- `reduceRight()`
- `reverse()`
- [`shift()`](#shiftpop)/[`pop()`](#shiftpop)
- [`slice()`](#slice)
- `some()`
- `sort()`
- [`splice()`](#splice)
- `toLocaleString()`
- `toSource()`
- [`unshift()`](#unshiftpush)/[`push()`](#unshiftpush)
- `values()`

<br /><br />

### `forEach()`
주어진 함수를 배열 요소 각각에 대해 실행합니다. 콜백 함수는 세 가지 매개변수를 받습니다.
```javascript
array.forEach(function(value, index, array) {
  
}, this)
```
`undefined`를 반환합니다.

- `value` : 처리할 현재 요소
- `index` : 처리할 현재 요소의 인덱스
- `array` : `forEach()`를 호출한 배열
- `this` : `callback`은 전달받은 `this`의 값을 자신의 `this` 값으로 사용할 수 있습니다. 

> 예외를 던지지 않고는 `forEach()`를 중간에 멈출 수 없습니다. 중간에 멈춰야 한다면 `forEach()`가 적절한 방법이 아닐지도 모릅니다. 간단한 `for` 반복문,  `every()`, `some()`, `find()`, `findIndex()` 등을 사용하면 중간에 반복을 종료할 수 있습니다. 

<br /><br />

### `map()`
배열 내의 모든 요소 각각에 대하여 주어진 함수를 호출한 결과를 모아 새로운 배열을 반환합니다.
```javascript
array.map(function(value, index, array) {
  
}, this)
```
`callback`의 결과를 모은 새로운 배열를 반환합니다.

> `map`을 호출한 배열의 중간이 비어있는 경우, 결과 배열 또한 동일한 인덱스를 빈 값으로 유지합니다.

- `value` : 처리할 현재 요소
- `index` : 처리할 현재 요소의 인덱스
- `array` : `map()`를 호출한 배열
- `this` : `callback`은 전달받은 `this`의 값을 자신의 `this` 값으로 사용할 수 있습니다. 

<br />

#### 예제1
```javascript
const items = [
  {
    id: 1,
    text: 'hello'  
  },
  {
    id: 2,
    text: 'bye'  
  }
];

const texts = items.map(item => item.text);
console.log(texts); // ['hello', 'bye']
```
`items` 배열의 각 `value`에서 키값이 `text`인 값들로 새로운 배열을 생성합니다.

<br />

#### 예제2
```javascript
['1', '2', '3'].map(parseInt);
```
위 코드의 결과를 `[1, 2, 3]` 으로 기대할 수 있습니다. 그러나 실제 결과는 `[1, NaN, NaN]` 입니다.
왜 그럴까요? 바로 `parseInt`와 `map`의 정의 때문입니다.
`parseInt`는 두가지 매개변수를 전달 받습니다. 첫번째 인자는 변환하고자하는 `value`이고, 두번째 인자는 변환할 때 사용할 진법입니다. 두번째인가 특정되지 않거나 '0'일 경우에는 10진법을 사용합니다.
이제 `map`의 정의를 다시 살펴 봅시다. 다음은 `map`의 콜백을 명시하는 문장입니다.
```text
the callbackfn is called with three arguments: the value of the element, the index of the element, and the object that is being traversed.
```
이 문장이 의미하는 바는, 아래와 같이 보이는 것이
```javascript
parseInt("1")
parseInt("2")
parseInt("3")
```
사실은 세가지의 인자를 가지고 있다는 것입니다.
```javascript
parseInt("1", 0, array) // 여기서 array는 원래의 배열인 ['1', '2', '3']를 가리킵니다.
parseInt("2", 1, array)
parseInt("3", 2, array)

// 1
// NaN
// NaN
```
두번째와 세번째 함수에서 각각의 두번째 인자가 `1`과 `2`이기 때문에 결과는 `[1, NaN, NaN]`이 됩니다. <br />

그렇다면 이러한 경우에 어떤 방법을 사용할 수 있을까요? 여기 여러 가지 예시가 있습니다. 

```javascript
function returnInt(element) {
  return parseInt(element, 10);
}

['1', '2', '3'].map(returnInt); // [1, 2, 3]
```

```javascript
['1', '2', '3'].map(str => parseInt(str));
```

```javascript
['1', '2', '3'].map(Number); // [1, 2, 3]

// 그러나 `parseInt`와 달리 float이나 지수표현도 반환합니다.
['1.1', '2.2e2', '3e300'].map(Number); // [1.1, 220, 3e+300]
```

<br /><br />

### `filter()`
주어진 함수의 테스트를 통과하는 모든 요소를 모아 새로운 배열로 반환합니다.
```javascript
array.filter(function(value, index, array) {
  
}, this)
```
- `value` : 처리할 현재 요소
- `index` : 처리할 현재 요소의 인덱스
- `array` : `map()`를 호출한 배열
- `this` : `callback`은 전달받은 `this`의 값을 자신의 `this` 값으로 사용할 수 있습니다. 

<br />

#### 예제

```javascript
const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

const result = words.filter(word => word.length > 6);

console.log(result); // ['exuberant', 'destruction', 'present']
```

```javascript
const fruits = ['apple', 'banana', 'grapes', 'mango', 'orange'];

const filterItems = (query) => {
  return fruits.filter((el) =>
    el.toLowerCase().indexOf(query.toLowerCase()) > -1
  );
}

console.log(filterItems('ap')); // ['apple', 'grapes']
console.log(filterItems('an')); // ['banana', 'mango', 'orange']
```

<br /><br />

### `includes()`
배열이 특정 요소를 포함하고 있는지 판별합니다. Boolean 값을 반환 합니다.
> IE 지원 X

```javascript
array.includes(value, index);
```
- `value` : 탐색할 요소
- `index`(optional) : 배열에서 검색을 시작할 위치 (기본값 `0`)

> 문자나 문자열을 비교할 때, `includes()`는 대소문자를 구분합니다.

<br />

#### 예제
```javascript

const isAnimal = (text) => {
  const animals = ['고양이', '개', '거북이', '토끼'];
  return animals.includes(text);
}

console.log(isAnimal('개')); // true
console.log(isAnimal('사슴')); // false
```
찾는 값이 있으면 `true`, 없으면 `false`를 반환합니다.

만약에 배열이 아닌 어떠한 값에 따른 value를 찾고 싶다면요? 이때는 아래의 예시처럼 객체를 사용해보세요.
```javascript
const getSound = (animal) => {
  const sounds = {
    개: '멍멍',
    고양이: '야옹',
    참새: '짹짹',
    비둘기: '구구구'  
  };
  return sounds[animal] || '해당하는 소리가 없습니다.'    
}

console.log(getSound('개')); // 멍멍
console.log(getSound('여우')); // 해당하는 소리가 없습니다.
```


<br /><br />

### `splice()`
배열의 기존 요소를 삭제 또는 교체하거나 새 요소를 추가하여 배열의 내용을 변경합니다. 제거한 요소를 담은 배열을 반환합니다.
> 하나의 요소만 제거한 경우 길이가 `1`인 배열을 반환합니다. 아무 값도 제거하지 않았으면 빈 배열을 반환합니다.

```javascript
array.splice(start, deleteCount, item1, item2, ... )
```
- `start` : 배열의 변경을 시작할 인덱스, 음수인 경우 배열의 끝에서부터 요소를 세어나갑니다.
- `deleteCount` : 배열에서 제거할 요소의 수
    - 생략/`array.length - start`보다 큰 경우 : `start`부터의 모든 요소를 제거
    - `0` 이하인 경우 : 어떤 요소도 제거 X, 이 때는 최소한 하나의 새로운 요소를 지정해야 합니다.
- `item1`/`item2` : 배열에 추가할 요소, 지정하지 않으면 `splice()`는 요소를 제거하기만 합니다.

<br />

#### 예제

하나도 제거하지 않고, 2번 인덱스에 `'drum'`을 추가합니다.
```javascript
let myFish = ['angel', 'clown', 'mandarin', 'sturgeon'];
let removed = myFish.splice(2, 0, 'drum');

// myFish is ['angel', 'clown', 'drum', 'mandarin', 'sturgeon'] 
// removed is [], no elements removed
```

3번 인덱스에서 두 개 요소를 제거합니다.
```javascript
let myFish = ['angel', 'clown', 'drum', 'mandarin', 'sturgeon'];
let removed = myFish.splice(3, 2);

// removed is ['mandarin', 'sturgeon']
// myFish is ['angel', 'clown', 'drum'] 
```

<br /><br />

### `slice()`
어떤 배열의 `begin`부터 `end`바로 이전까지 복사하여 새로운 배열 객체로 반환합니다. 원본 배열은 바뀌지 않습니다.

```javascript
array.slice(begin, end)
```
- `start` : `0`을 시작으로 하는 추출 시작점에 대한 인덱스를 의미
    - `undefined`인 경우 : 0번 인덱스부터 `slice` 
    - 배열의 길이보다 큰 경우 : 빈 배열을 반환
- `end` : 추출을 종료 할 0 기준 인덱스, `slice` 는 `end` 인덱스를 제외하고 추출합니다.
    - 생략/배열의 길이보다 큰 경우 : 배열의 끝까지 추출

<br />

#### 예제
기본 배열의 일부를 반환합니다.

```javascript
let fruits = ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango']
let citrus = fruits.slice(1, 3)

// fruits contains ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango']
// citrus contains ['Orange','Lemon']
```

`slice(2,-1)` 는 세번째부터 끝에서 두번째 요소까지 추출합니다.
```javascript
let fruits = ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango']
let citrus = fruits.slice(2, -1)

// fruits contains ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango']
// citrus contains ['Lemon', 'Apple']
```

<br /><br />

### `shift()`/`pop()`
`shift()`는 배열에서 첫 번째 요소를, `pop()`은 마지막 요소를 제거하고 제거된 요소를 반환합니다. 이 때, 원래 배열의 길이를 변하게 합니다.

```javascript
array.shift();

array.pop();
```
> 배열의 길이가 `0`이라면 `undefined`를 리턴 합니다.

<br />

#### 예제
`shift()` 메서드는 while 문의 조건으로 사용되기도 합니다.
```javascript
let names = ['Andrew', 'Edward', 'Paul', 'Chris' ,'John'];

while( (i = names.shift()) !== undefined ) {
    console.log(i);
}

// Andrew, Edward, Paul, Chris, John
```

<br /><br />

### `unshift()`/`push()`
`unshift()`는 새로운 요소를 배열의 맨 앞쪽에 추가하고, `push()`는 배열의 마지막에 추가하며 배열의 새로운 길이(추가하는 요소의 개수)를 반환합니다.

```javascript
array.unshift(element1, element2, ...);

array.push(element1, element2, ...);
```
- `element1`/`element2` : 배열에 추가할 요소 

<br />

#### 예제

```javascript
let sports = ['축구', '야구'];
let total = sports.push('미식축구', '수영');

console.log(sports); // ['축구', '야구', '미식축구', '수영']
console.log(total);  // 4
```

두 개의 배열을 합치고 싶을 때는 어떤 방법이 좋을까요? 이 때에는 두번째 배열의 모든 엘리먼트를 `push` 하기 위해 `apply()`를 사용할 수 있습니다.
```javascript
var vegetables = ['설탕당근', '감자'];
var moreVegs = ['셀러리', '홍당무'];

Array.prototype.push.apply(vegetables, moreVegs); // 기존 배열, 추가할 배열

console.log(vegetables); // ['설탕당근', '감자', '셀러리', '홍당무']
```

> 주의할 점 : 추가할 배열의 길이가 아주 클 경우 `apply()`를 쓸 수 없습니다. JavaScript 엔진의 인수 길이 제한 때문입니다. 엔진마다 함수가 받을 수 있는 인수의 개수는 다르지만, JavaScriptCore의 경우 인수의 개수 제한은 `65536`입니다.

> 두 개의 배열을 합치는 방법은 `concat()`을 사용할 수도 있습니다. 

<br /><br />

### `concat()`
인자로 주어진 배열이나 값들을 기존 배열에 합쳐서 새 배열을 반환합니다. 기존배열을 변경하지 않습니다.  

```javascript
array.concat(value1, value2, ...);
```
- `value`(optional) : 기존 배열에 합쳐질 배열 또는 값

> 인자를 생략하면 기존 배열의 얕은 복사본을 반환합니다.

<br />

#### 예제
```javascript
const num1 = [1, 2, 3];
const num2 = [4, 5, 6]; 
const num3 = [7, 8, 9];

const result = num1.concat(num2, num3);

console.log(result); // [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

```javascript
const alpha = ['a', 'b', 'c'];

const result = alpha.concat(1, [2, 3]);

console.log(result); // ['a', 'b', 'c', 1, 2, 3]
```

<br /><br />

### `reduce()`
배열의 각 요소에 대해 주어진 리듀서(reducer) 함수를 실행하고, 하나의 결과값을 반환합니다.

```javascript
const callback = (accumulator, currentValue, currentIndex, array) => {    
    return returnValue;
};

array.reduce(callback, initialValue);
```
`callback` 함수는 네 개의 인자를 가집니다.
- `accumulator` : 콜백의 반환값을 누적한 값
- `currentValue` : 처리할 현재 요소
- `currentIndex`(optional) : 처리할 현재 요소의 인덱스
    - `initialValue`를 제공한 경우 : `0`부터 시작
    - 제공하지 않은 경우 : `1`부터 시작
- `array`(optional) : reduce()를 호출한 배열

`initialValue`(optional)는 최초 호출에서 첫 번째 인수에 제공하는 값입니다. 초기값을 생략하면 배열의 첫번째 요소가 초기값이 됩니다.
> 빈 배열에서 초기값 없이 `reduce()`를 호출하면 [TypeError](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/TypeError) 가 발생합니다.

<br />

#### 예제1
여기 하나의 배열이 있습니다. 
```javascript
const numbers = [1, 2, 3, 4, 5];
```

`reduce()`를 사용해 배열 안의 모든 원소를 더해봅니다.
```javascript
const sum = numbers.reduce((accumulator, current) => accumulator + current, 0);
console.log(sum); // 15
```

같은 배열을 가지고 평균을 구해봅니다.
```javascript
const avg = numbers.reduce((accumulator, current, index, array) => {

    if(index === array.length - 1){ // 배열의 마지막 원소일 때
        return (accumulator + current) / array.length;
    }
    return accumulator + current;

}, 0);

console.log(avg); // 3
```
<br />

#### 예제2
하나의 배열에 똑같은 값이 몇 번씩 들어가 있는지 알아봅니다.

```javascript
const alphabets = ['a', 'a', 'a', 'b', 'c', 'c', 'd', 'e'];

const counts = alphabets.reduce((acc, current) => {

    if(acc[current]) { // 누적된 객체 acc에 current 라는 키값이 존재한다면
        acc[current] += 1;
    }
    else{
        acc[current] = 1;
    }   

}, {}) // 초기값은 비어있는 객체입니다. 

console.log(counts); // Object {a: 3, b: 1, c: 2, d: 1, e: 1}
```

<br /><br />

***
### _References_
[Loops and iteration | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Loops_and_iteration)
[for | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for)
[for...in | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for...in)
[for...of | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for...of)
[Array.prototype.forEach() | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
[Array.prototype.map() | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
[Array.prototype.filter() | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
[A JavaScript Optional Argument Hazard | Allen Wirfs-Brock](http://www.wirfs-brock.com/allen/posts/166)
[Array.prototype.splice() | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)
[Array.prototype.slice() | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)
[Array.prototype.shift() | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/shift)
[Array.prototype.pop() | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)
[Array.prototype.unshift() | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift)
[Array.prototype.push() | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/push)
[Function.prototype.apply() | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)
[Array.prototype.concat() | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/concat)
[Array.prototype.reduce() | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)
[Array.prototype.includes() | MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)
