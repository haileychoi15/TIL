# React
- 개발 환경 준비
- JS, CSS 코딩하는 법
- Components
- JSX
- Props
- State
- Lists and Keys
- 배포하는 법

<br />

## 1. 개발 환경 준비
> `yarn` 을 사용하고 있습니다. `yarn`이 없다면, `npm`을 사용하시면 됩니다. 사용방법은 동일합니다.

<br />

## 2. JS, CSS 코딩하는 법
### CSS 불러오기
```jsx
import 'CSS 파일 위치';
```

<br /><br />

## Components
컴포넌트는 일종의 UI 조각이라고 할 수 있습니다.

### Function type

```jsx
function 컴포넌트명() {
  return (
  
  );
}
```

### Class type
```jsx
class 컴포넌트명 extends Component {
  render () {
    return (
      <header>
        // ... 
      </header>
    );
  }
}

class App extends Component {
  render () {
    return (
      <div className="App">
        <컴포넌트명></컴포넌트명>
      </div>
    );
  }
}
```
`App`라는 class가 react 가 가지고 있는 `Component` class 를 상속합니다.
- `App`는 영문대문자로 시작해야 합니다.
- `render()` 안에서 `Component`는 하나의 최상위 태그로 시작합니다.

웹 브라우저는 위의 코드들을 아래와 같이 이해할 것입니다.
```html
<div class="App">
  <header>
    <!-- ... -->
  </header>
</div>
```

<br />

#### How to import `React.Components`
react 를 사용하기 위한 기본 코드입니다.
```jsx
import React from 'react';
```

```jsx
import React, { Component } from 'react';
```
#### How to export component
```jsx
export default 컴포넌트명
```

#### How to import component 
```jsx
import 컴포넌트명 from '가져올 컴포넌트 위치' ;
```
파일의 위치를 지정할때는 확장자를 생략할 수 있습니다.

<br /><br />

## JSX
JSX을 사용하여 XML 형태로 선언을 하면, `create-react-app`이 JS로 변환해줍니다. 

### 문법
- 태그는 꼭 닫혀야 합니다. `<input />`, `<br />` 등의 태그는 꼭 self-closing 되도록 작성해주세요.
- 두 개 이상의 요소는 꼭 하나의 요소로 묶여야합니다.`<div> .. </div>`로 감싸고 싶지 않다면, `<> .. </>` (fragment)를 사용해 보세요.
- JSX 내부에서 JS 값을 사용하려면 `{ .. }` 로 깜싼 뒤, 그 안에 변수나 상수를 넣으세요.
- inline-style를 지정하고 싶다면, 객체 형태로 만들어 넣어주어야 합니다.
- `class`를 지정하고 싶다면 `className` 속성을 사용하세요.
- 주석을 사용하는 올바른 방법은 `{/* .. */}`입니다. 태그 내부에서의 주석은 `// ..` 이렇게 작성할 수 있습니다.

```jsx
function App() {
    const name = 'react';
    const style = {
      backgroundColor: 'black',  /* camelCase로 작성해야 합니다. */
      color: 'aqua',
      fontSize: 24, /* 기본 단위는 px 입니다. */
      padding: '1rem' /* 단위를 따로 설정하려면, 문자열로 작성해 주세요. */
    }
    return (
      <>
        {/* 주석 테스트 */} 
        <Header />
        <div style={style}>{name}</div>
        <div 
          // 주석 테스트
        >{name}</div>
      </>
    )
}
```

<br /><br />

## Props
> properties

```jsx
// App.js
function App() { 
  return (
    <Hello name="react" color="red">
  );
}

// Hello.js
function Hello(props) { 
  console.log(props); // {name: "react"}
  return <div style={{color: props.color}}>hello, {props.name}!</div>
  /* style 에서 바깥 {  }는 내부에 JS 값을 넣어주기 위한 문법이며, 내부 { }는 객체를 의미합니다. */
}
```
위의 코드를 구조 분해 할당을 사용하려면 더욱 간결해집니다.

```jsx
// Hello.js
function Hello({ color, name }) {
  return <div style={{color}}>hello, {name}!</div>
}
```

### defaultProps
props가 전달 되지 않았을 때 기본적으로 사용할 props을 설정할 수 있습니다. 객체 형태입니다.
```jsx
// App.js
function App() { 
  return (
    <>
      <Hello name="react" color="red">
      <Hello color="blue"> {/* name 값이 지정되지 않았습니다. */}
    </>
  );
}

// Hello.js
function Hello({ color, name }) {
  return <div style={{color}}>hello, {name}!</div>
}

Hello.defaultProps = {
  name: 'world'
};
```

<br />

###childrenProps
컴포넌트 내부에서 다른 컴포넌트를 랜더링 하고 싶을 때 사용합니다.
```jsx
// App.js
function App() { 
  return (
    <Wrapper>
      <Hello name="react" color="red"> 
      <Hello color="blue">
    </Wrapper>
  );
}

// Wrapper.js
function Wrapper({ children }) {  /* children을 사용해 랜더링하고자하는 컴포넌트를 추출해옵니다. */
  const style = {
    border: '2px solid black',
    padding: 16
  }
  return (
    <div style={style}>{children}</div> /* div는 검정 테두리가 있는 상자 형태입니다. */
  );
}
```

<br /><br />

## State

state 는 props 와 비슷하지만, 프라이빗하고 컴포넌트에 의해 완전히 controll 된다는 특징이 있습니다. 그렇다면 왜 state를 사용할까요?
state 를 사용하면 앱 외부에서 컴포넌트를 실행시킬 때 컴포넌트의 state 값이 있는지 없는지 알 수 없습니다. state는 오로지 앱 내부에서 사용됩니다. 즉, 사용자가 알 필요가 없는 정보를 외부로부터 은닉시킬 수 있습니다.
state 를 사용하기 위해서는 컴포넌트의 state를 초기화 하는 클래스 생성자를 추가하면 됩니다.

```jsx
class App extends React.Component {

  constructor(props) { // state 초기화하는 생성자
      super(props);
      this.state = {
        subject: {title:'Hello, world!', desc:'How to start react'}
      };
    }

  render() {
    return (
      <div>
        <h1>{this.state.subject.title}</h1> //  JS 코드로써 실행되기 위해서 { .. } 를 사용합니다.
        <h2>Today's subject is {this.state.subject.desc}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

`constructor()`의 역할은 컴포넌트가 실행될 때 `render()` 보다 먼저 실행되면서 컴포넌트의 초기화를 담당합니다. 초기화가 끝나면 `this.state = { .. }`에서 state 값을 초기화 시킵니다.
예제에서는 `subject`의 값을 state화 시키기 위해서, `subject`의 프로퍼티 값으로 `{title:' .. ', desc:' .. '}` 이라는 객체를 넣어줍니다.
이제 상위  컴포넌트의 state 값을 하위 컴포넌트의 props 값으로 전달하여 사용할 수 있습니다.

<br />

### State 동적으로 바꾸기
```jsx
this.setState({
  value: 'welcome';
});
```
`setState()`를 사용합니다. 아래의 방법처럼 쓰지 않도록 주의해주세요.
```jsx
this.state.value = 'welcome' // 옳지 못한 문법;
```

<br /><br />

## Lists and Keys

```jsx
class App extends Component {

    constructor(props) { // state 초기화하는 생성자
        super(props);
        this.state = {
            subject: {title:'WEB', sub:'World wide Web'},
            contents: [
                {id: 1, title:'HTML', desc:'HTML is for information'},
                {id: 2, title:'CSS', desc:'CSS is for design'},
                {id: 3, title:'JavaScript', desc:'JavaScript is for interactive'},
            ]
        };
    }

    render() {
        let lists = [];
        let i = 0;
        let data = this.state.contents;
        while(i < data.length){
            lists.push(<li>{data[i].title}</li>);
            i = i + 1;
        }
        return (
            <div className="App">
                <h1>{this.state.subject.title}</h1> {/* JS 코드로써 실행되기 위해서 { .. } 를 사용합니다. */}
                <h2>Today's subject is {this.state.subject.sub}.</h2>
                <nav>
                    <ul>
                        {lists}
                    </ul>
                </nav>
            </div>
        );
    }
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```
반복문을 이용해 list 를 자동생성하고 있습니다. 이 때, 이러한 오류가 발생합니다.
```text
Warning: Each child in a list should have a unique "key" prop.
```
왜 그럴까요? 각각의 list 는 key 라는 porps 를 가져야 합니다. 각각의 목록을 다른 것들과 구분할 수 있는 식별자를 제공하는 것입니다. 
```jsx
lists.push(<li key={data[i].id}>{data[i].title}</li>);
```
위의 코드처럼 list를 자동 생성해주는 코드에 key props를 넣어주면 됩니다.

<br /><br />

## 3. 배포하는 법 

### 배포 폴더 생성
```text
yarn start
```
터미널에 위와 같은 명령어를 입력하면, `build`라는 이름의 디렉토리가 생성됩니다.
`build` 디렉토리 안에 `index.html`파일 이 있습니다. 이는 실제 프러덕션에서 사용하는 앱을 만들기 위해서 우리가 원래 가지고 있던 
`public` 디렉토리 안에 `index.html` 파일과 `src` 디렉토리에서 불필요한 부분을 살균시킨 것이라고 생각하면 됩니다. 즉, 실제 서비스는 용량이 작아집니다.

<br />

실제로 서비스를 할 때는 `build` 폴더 안의 파일들을 쓰면 됩니다. 웹 서버가 문서를 찾는 최상위 폴더에 `build` 폴더 안의 파일들을 위치 시키면 됩니다. 그렇다면 이제 실서버 환경이 구축되었습니다.

<br />

### 서버 설치

```text
npm install -g serve
```
위의 명령어를 입력하면 작업하는 PC의 어디에서나 `serve`라는 명령어를 통해서 웹서버를 설치 할 수 있습니다.

```text
npx serve
```
한번만 실행 시킬 웹서버를 다운받아서 실행시킵니다.

```text
npx serve -s build
```
여기서 `-s`는 웹서버를 실행시킬 때 `build` 디렉토리를 `document.root`로 사용하겠다는 의미입니다. 이제 어떤 주소로 접속하면 되는지 사용자에게 알려줄 것입니다.
주소로 접속하면 개발 환경의 앱보다 용량이 훨씬 가벼워진 것을 확인할 수 있습니다.  

<br /><br />

***
#### _References_
[벨로퍼트와 함께하는 모던 리액트 | velopert](https://react.vlpt.us/) <br />
[React | 생활코딩]()