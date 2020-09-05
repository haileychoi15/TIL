## 객체(Object)

### 객체 비구조화 할당

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

### 객체 안의 함수

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


### `getter`/`setter`

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