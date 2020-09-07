# 표현식(Expressions)
자주 쓰이는 자바스트립트의 표현식들과 개념을 정리하고 있는 문서입니다.

- [단축 평가 논리 계산법](#단축-평가-논리-계산법)
- [비구조화 할당(Destructuring assignment)](#비구조화-할당)
- [`getter`/`setter`](#gettersetter)
- [`spread` 구문](#spread)
- [`rest` 파라미터](#rest)
- [객체(Object) 안의 함수(Fuction)](#객체object-안의-함수fuction)

<br />

## 단축 평가 논리 계산법

<br />

### `&&` 연산자
`A && B`연산자를 사용할 때는 A와 B 모두 `true`여야 결과가 `true`가 됩니다. 
따라서, A가 `false`이거나 `falsy`하다면 B를 더이상 확인하지 않고 결과는 A가 됩니다. 
반면에, A가 `true`이거나 `truthy`하다면, 결과는 B가 됩니다.

```javascript
console.log(true && 'hello'); // hello
console.log(false && 'hello'); // false
console.log('hello' && 'bye'); // bye
console.log(null && 'hello'); // null
```

<br />

### `||` 연산자
`A || B`연산자를 사용할 때는 A와 B 중 하나만 `true`여도 결과가 `true`가 됩니다. 
따라서, A가 `true`이거나 `truthy`하다면 B를 더이상 확인하지 않고 결과는 A가 됩니다. 
반면에, A가 `false`이거나 `falsy`하다면, 결과는 B가 됩니다.
```javascript
console.log(false || 'hello'); // hello
console.log('' || 'hello'); // hello
console.log(null || 'hello'); // hello
console.log(1 || 'hello'); // 1
```

<br />

### 예제
```javascript
const namelessDog  = {
    name : '',
};

function getName(animal) {
    const name = animal && animal.name; // '&&' 연산자 사용
    return name || '이름이 없는 동물입니다.'; // '||' 연산자 사용
}


const name = getName(namelessDog);
console.log(name); // 이름이 없는 동물입니다.
```
`animal` 객체가 `null`이거나 `undefined`일 때 오류가 발생하지 않습니다. 또한, 이 때 출력 할 메시지(여기 에서는 `'이름이 없는 동물입니다.'`)를 설정할 수 있습니다. 

<br /><br />

## 비구조화 할당
배열이나 객체에서 어떤 값을 분해해 할당할지 정의합니다.

<br />

### 객체 예제
객체에서 이루어지는 비구조화 할당입니다.
```javascript
const ironMan = {
  name: '토니스타크',
  actor:  '로버트 다우니 주니어',
  alias: '아이언맨',
};

const captainAmerica = {
  name: '스티븐 로저스',
  actor:  '크리스 에반스',
  alias: '캡틴 아메리카',
};

function print(hero){
  const { alias, name, actor } = hero; // 비구조화 할당
  const text = `${alias}(${name}) 역할을 맡은 배우는 ${actor}입니다.`;
  console.log(text);
}

print(ironMan); // 아이언맨(토니스타크) 역할을 맡은 배우는 로버트 다우니 주니어입니다.
print(catainAmerica); // 캡틴아메리카(스티븐 로저스) 역할을 맡은 배우는 크리스 에반스입니다.
```

<br />

비구조화 할당을 사용할 때 이름을 바꿀 수 있습니다. 
```javascript
const animal = {
  name: '멍멍이',
  type: '개'
}

const { name: nickname } = animal;
// const nickname = animal.name; 이렇게 사용하는 것과 동일합니다.

console.log(nickname);
```
기존 객체는 `name`을 그대로 유지합니다.

<br />

객체의 깊속한 곳에서 값을 꺼내어 할당 할 수 있습니다.
```javascript
const deepObject = {
  state: {
    information: {
      name: 'velopert',
      languages: ['korean', 'english', 'arabic']
    }
  },
  value: 5
}

// 키 값이 name, languages, value인 값들을 비구조화 할당 하고자 합니다.
const { name, languages: [firstLang, secondLang] } = deepObject.state.information;
const { value } = deepObject;

// 비구조화 할당을 한 값들을 가지고 새로운 객체를 선언합니다.
const extracted = {
  name, // name: name,
  firstLang, // firstLang: firstLang,
  secondLang, // secondLang: secondLang,
  value // value: value
};

console.log(extracted);
// Object {name: "velopert", firstLang: "korean", secondLang: "english", value : 5}
```
위의 코드를 보면 `extracted` 객체를 선언할 때, `key`값에 따른 `value`값을 생략했습니다. 특정 `key` 이름으로 선언된 값이 이미 존재한다면, `value` 값 설정을 생략할 수 있습니다.

<br />

### 배열 예제

```javascript
const array = [1, 2, 3, 4, 5];

const [one, two] = array; // 배열의 좌측부터 할당합니다.

console.log(one); // 1
console.log(two); // 2
```
<br />

객체 비구조화 할당처럼 기본값을 지정할 수 있습니다.
```javascript
const array = [1];

const [one, two = 3] = array;

console.log(one); // 1
console.log(two); // 3
```

<br /><br />

## `getter`/`setter`

### 예제

```javascript
const dog = {
  _name: '멍멍이',
  get name() {
    console.log('_name을 조회합니다..');
    return this._name;  
  },
  set name(value) {
    console.log('이름이 바뀝니다..' + value);  
    this._name = value;
  }
};

console.log(dog.name); // 멍멍이
dog.name = '뭉뭉이';
console.log(dog.name); // 뭉뭉이
```

<br /><br />

## `spread` 구문
기존의 객체(`Object`, `Array`)를 참고하여 새로운 객체를 생성할 때 사용할 수 있습니다. 객체를 참조할 때는 객체명앞에 `...`을 붙여 사용합니다.
```javascript
// 함수 호출
myFunction(...object);

// 배열 리터럴과 문자열
[...object, value1, value2, ...];

// 객체 리터럴 (ECMAScript 2018에서 추가)
let objectClone = {...object};
```
- `object` : 반복가능(iterable)한 객체
- `value1`/`value2` : 추가할 배열 요소

<br />

### 예제

#### 배열(Array)
배열 리터럴에서 `spread` 구문을 아래의 예시처럼 사용할 수 있습니다. 
```javascript
const animals = ['개', '고양이', '말', '토끼'];
const moreAnimals = [...animals, '생쥐', '기린'];
// const moreAnimals = animals.concat('생쥐', '기린'); 와 동일한 방법입니다.

console.log(animals); // ["개", "고양이", "말", "토끼"]
console.log(moreAnimals); // ["개", "고양이", "말", "토끼", "생쥐", "기린"]
```
<br />

배열 안에서 `spread` 구문을 여러번 쓸 수 있습니다.

```javascript
const numbers = [1, 2, 3, 4, 5];
const spreadNumbers = [...numbers, 1000, ...numbers];

console.log(spreadNumbers); // [1, 2, 3, 4, 5, 1000, 1, 2, 3, 4, 5]
```

<br />

#### 객체(Object)

객체 리터럴에서 `spread` 구문을 아래의 예시처럼 사용할 수 있습니다. 
```javascript
const slime = {
  name: '슬라임'
};

const softSlime = {
  ...slime,
  attribute: 'soft'
};

const purpleSoftSlime = {
  ...softSlime,
  color: 'purple'
};

const greenSoftSlime = {
  ...purpleSoftSlime,
  color: 'green'
};

console.log(slime); // Object {name: "슬라임"}
console.log(softSlime); // Object {name: "슬라임", attribute: "soft"}
console.log(purpleSoftSlime); // Object {name: "슬라임", attribute: "soft", color: "purple"}
console.log(greenSoftSlime); // Object {name: "슬라임", attribute: "soft", color: "green"}
```

#### 함수(Function)

`spread` 구문을 함수의 인자에 사용할 수도 있습니다. 아래의 예시를 살펴봅시다.

```javascript
function sum(...params) {
  params.reduce((acc, current) => acc + current, 0);
}

const numbers = [1, 2, 3, 4, 5, 6, 7, 8];
const result  = sum(...numbers);
// const result = sum(1, 2, 3, 4, 5, 6, 7, 8); 의 방법과 동일합니다.

console.log(result); // 36
```
`spread` 구문을 사용하면 원래 함수에 지정된 파라미터의 개수보다 전달된 인자의 개수가 모자라서, 함수 처리 과정에서 파라미터가 `undefined`되는 것을 막을 수 있습니다. 
또한, 전달된 인자의 개수가 넘쳐서 함수 처리 과정에서 제외되는 것을 막을 수 있습니다.

<br /><br />

## `rest` 구문
`rest` 구문은 `spread` 구문과 문법이 같습니다. 대신 배열이나 객체를 분해할 때 사용됩니다.

- `rest` 구문을 사용할 때 `rest` 명칭을 사용자가 정의할 수 있습니다.
- `rest` 구문은 꼭 마지막 요소(파라미터)로만 사용해야 합니다. 
- `rest`가 비어있더라도, 여전히 객체형태를 갖습니다.
    - 객체에서 사용하는 경우 : 비어있는 객체(object)
    - 배열에서 사용하는 경우 : 비어있는 배열(array)
    - 함수에서 사용하는 경우 : 비어있는 배열(array)
    
<br />

### 예제

#### 배열(Array)
```javascript
const numbers = [0, 1, 2, 3];

const [first, ...rest] = numbers;

console.log(first); // 0
console.log(rest); // [1, 2, 3];
```

<br />

#### 객체(Object)
객체 비구조화 할당 과정에서 사용할 수 있습니다.
```javascript
const blueCuteSlime = {
  name: '슬라임',
  attribute: 'cute',
  color: 'blue'
}

const { color, ...rest } = blueCuteSlime;
console.log(color); // blue
console.log(rest); // Object {name: "슬라임", attribute: "cute"}
```

<br />

#### 함수(Function)
인자에 넣어준 값들이 배열의 형태로 파라미터에 전달됩니다.
```javascript
const getNumbers = (a, b, ...rest) => {

  console.log(a); // one
  console.log(b); // two
  console.log(rest); // ["three", "four", "five", "six"]
}

getNumbers('one', 'two', 'three', 'four', 'five', 'six');
```

<br /><br />

## 객체(Object) 안의 함수(Fuction)

### 예제

```javascript
const dog = {
  name: '멍멍이',
  sound: '멍멍!',
  say: function() {
    console.log(this.sound); // 여기서 this는 자신이 속한 곳, 즉 dog 객체를 가리킵니다.
  }
};

const cat = {
  name: '야옹이',
  sound: '야옹~'
};

cat.say = dog.say;
dog.say(); // 멍멍!
cat.say(); // 야옹~ 


const catSay = cat.say;
catSay(); // 오류 발생
```
위의 코드에서 마지막 줄에서 다음과 같은 오류가 발생했습니다. 왜 그럴까요?
```html
TypeError: Cannot read property 'sound' of undefined 
```
`const catSay`는 객체 안이 아니라 밖으로 꺼냈기 때문에 아무 곳에도 엮여 있지 않게 됩니다. 여기서 `this`는 `undefined`가 되기 때문입니다.  

> 객체 안의 함수가 화살표 함수일 때에는 `this`가 자신이 속한 곳을 가리키지 않습니다.

<br /><br />

***
### _References_
[Destructuring assignment | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) <br />
[Spread syntax &#40;...&#41; | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) <br />
[Rest parameters | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)