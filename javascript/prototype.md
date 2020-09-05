# 프로토타입(Prototype)과 클래스(Class)

<br />

### 예제1 
```javascript
class Animal {
    constrctor(type, name, sound){
        this.type = type;
        this.name = name;
        this.sound = sound;
    }
    
    // Animal.prototype 에 등록이 됩니다. 
    say() { 
        console.log(this.sound);
    }
}

const dog = new Animal('개', '멍멍이', '멍멍');
const cat = new Animal('고양이', '야옹이', '야옹');

dog.say(); // 멍멍
cat.say(); // 야옹
```

<br />

### 예제2 : 상속
```javascript
class Animal {
    constrctor(type, name, sound){
        this.type = type;
        this.name = name;
        this.sound = sound;
    }
    
    say() { 
        console.log(this.sound);
    }
}

class Dog extends Animal {
    constructor(name, sound) {
        super('개', name, sound);
    }
}

class Cat extends Animal {
    constructor(name, sound) {
        super('고양이', name, sound);
    }
}

const dog = new Dog('멍멍이', '멍멍');
const cat = new Cat('야옹이', '야옹');

dog.say(); // 멍멍
cat.say(); // 야옹
```

<br />

### 예제3
```javascript
class Food {
    constructor(name) {
        this.name = name;
        this.brands = [];
    }    
    addBrand(brand) {
        this.brands.push(brand);
    }
    print() {
        console.log(`${this.name} 파는 음식점들 : `);
        console.log(this.brands.join(', '));
    }
}

const pizza = new Food('피자');
pizza.addBrand('피자헛');
pizza.addBrand('도미노 피자');

const chicken = new Food('치킨');
chicken.addBrand('굽네치킨');
chicken.addBrand('BBQ');
chicken.addBrand('교촌치킨');

pizza.print(); // 피자 파는 음식점들 : 피자헛, 도미노 피자
chicken.print(); // 치킨 파는 음식점들 : 굽네치킨, BBQ, 교촌치킨
```