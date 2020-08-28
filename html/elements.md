# HTML 요소 참고서(HTML elements reference)
모든 HTML 요소의 목록과 시멘틱 마크업(Semantic Markup)을 위한 요소별 설명을 다루고 있습니다.

<br />

## HTML 요소 목록(HTML elements list)
`<body>` 요소 내에서 쓰이는 요소들을 기능별로 분류한 목록입니다.

<br />

### Content sectioning
구획 요소를 사용해 페이지 콘텐츠의 큰 틀을 잡을 수 있습니다. 
- `<header>`
- `<footer>`
- `<main>`
- `<section>`
- `<aside>`
- `<address>`
- `<article>`
- `<nav>`
- `<h1>-<h6>`
- `<hgroup>`

    > 다수의 `<h1>-<h6>` 요소를 묶을 때 사용합니다.

<br />

### Text content
해당 콘텐츠의 목적이나 구조 판별에 사용하므로 접근성과 SEO(검색 엔진 최적화)에 중요합니다.
- `<div>`
- `<main>`
- `<ul>`/`<ol>`/`<li>`
- `<dl>`/`<dt>`/`<dd>`
- `<p>`
- `<hr />`

    > 이야기 장면 전환, 구획 내 주제 변경 등, 문단 레벨 요소에서 주제의 분리를 나타냅니다.
- `<pre>`

    > 미리 서식을 지정한 텍스트를 나타내며, HTML에 작성한 내용 그대로 표현합니다.
- `<blockquote>`
- `<figure>`
- `<figcaption>`


<br />

### Inline text semantics
텍스트의 의미, 구조, 스타일을 정의할 수 있습니다.
- `<a>`
- `<abbr>`
- `<b>`
- `<bdo>`
- `<br />`
- `<cite>`
- `<code>`
- `<data>`
- `<dfn>`
- `<em>`/`<strong>`
- `<i>`
- `<kbd>`
- `<mark>`
- `<q>`
- `<ruby>`
- `<sub>`/`<sup>`
- `<u>`
- `<span>`
- `<time>`
>  더 많은 요소와 설명을 [여기](https://developer.mozilla.org/ko/docs/Web/HTML/Element)에서 볼 수 있습니다.

<br />

### Image and multimedia
사진, 오디오, 비디오 등 다양한 멀티미디어 리소스를 지원하는 요소입니다.
- `<img>`
- `<audio>`
- `<video>`
- `<map>`

    > 이미지 맵(클릭 가능한 링크 영역)을 정의할 때 사용합니다.
- `<area>`

    >  이미지의 핫스팟 영역을 정의하고, 하이퍼링크를 추가할 수 있습니다. `<map>` 요소 안에서만 사용할 수 있습니다.
- `<track>`

    > 미디어 요소(`<audio>`, `<video>`)의 자식으로서, 자막 등 시간별 텍스트 트랙(시간 기반 데이터)를 지정할 때 사용합니다.

<br />

### Embedded content
일반적인 멀티미디어 콘텐츠 이외의 콘텐츠를 포함하는 요소입니다.
- `<iframe>`
- `<embed>`
- `<object>`
- `<param>`
- `<picture>`
- `<source>`

<br />

### Scripting
동적인 콘텐츠와 웹 어플리케이션을 위해 스크립트 언어(주로 JavaScript)를 지원하는 요소입니다.
- `<script>`
- `<noscript>`
- `<canvas>`

<br />

### Demarcating edits
텍스트의 특정 부분이 수정됐다는 것을 표시하는 요소입니다.
- `<del>`
- `<ins>`

<br />

### Table content
표 형식의 데이터를 나타내는 요소입니다.
- `<table>`
- `<thead>`/`<tbody>`
- `<th>`/`<tr>`/`<td>`
- `<caption>`
- `<col>`
- `<colgroup>`

<br />

### Form
웹 서버에 데이터를 제출하기 위해 사용하는 양식(Form)을 구성하는 요소입니다. 여러가지 입력 가능한 요소를 제공합니다.
- `<form>`
- `<input />`
- `<label>`
- `<button>`
- `<select>`
- `<datalist>`
- `<option>`/`<optgroup>`
- `<textarea>`
- `<output>`
- `<progress>`
- `<fieldset>`
- `<legend>`
- `<meter>`

<br />

### Interactive elements
상호작용 가능한 사용자 인터페이스 객체를 만들 때 사용할 수 있는 요소입니다.
- `<details>`
- `<dialog>`
- `<menu>`
- `<summary>`

<br />

### Web Components
완전히 새로운 형태의 요소를 생성한 후 일반적인 HTML처럼 사용할 수 있는 기술을 지원하는 요소입니다.
- `<slot>`
- `<template>`

<br />
<br />

## `<h1> - <h6>`
제목의 정보를 사용해 자동으로 문서 콘텐츠의 표를 만드는 등의 작업을 수행할 수 있습니다. 제목 구획 단계는 `<h1>`이 가장 높고 `<h6>`은 가장 낮습니다.

- 글씨 크기를 위해 제목 태그를 사용하지 마세요. 대신 CSS의 `font-size` 속성을 사용하세요.
- 제목 단계를 건너뛰는 것을 피하세요. 언제나 `<h1>`로 시작해서 순차적으로 기입하세요.
- 페이지 당 하나의 `<h1>`만 사용하세요. `<h1>`은 가장 중요한 제목이므로 전체 페이지의 목적을 설명하고 이는 SEO(검색 엔진 최적화)와 연결됩니다.

<br />

## `<header>`
제목, 로고, 검색 폼, 작성자 이름 등의 요소를 포함할 수 있습니다.

- `<header>` 또는 `<footer>`가 자손으로 올 수 없습니다.

<br />

## `<footer>`
구획의 작성자, 저작권 정보, 관련 문서 등의 내용을 담습니다.

- `<header>` 또는 `<footer>`가 자손으로 올 수 없습니다.
- `<address>` 요소로 감싼 작성자 정보를 `<footer>` 요소에 배치하세요.

> 접근성 고려사항 : [VoiceOver](https://help.apple.com/voiceover/mac/10.15/) 스크린 리더는 랜드마크 로터에서 푸터의 랜드마크 역할을 표현하지 않는 문제가 있습니다. 해결하려면 `<footer>`에 `role="contentinfo"`를 추가하세요.

<br />

## `<main>`
문서 `<body>`의 주요 콘텐츠를 나타냅니다. 

- IE 지원이 불가합니다. 
- (`hidden` 속성 없이는) 문서 전체에 하나의 `<main>` 요소만 존재해야 합니다.
- 해당 문서만의 유일한 내용을 담아야 합니다. 사이드바, 탐색 링크, 저작권 정보, 사이트 로고, 검색 Form 등 여러 문서에 걸쳐 반복되는 콘텐츠는 포함해선 안됩니다. 그러나 검색 폼이 페이지의 주요 기능이라면 예외로 둘 수 있습니다.
- 개요에 영향을 주지 않습니다. `<body>` 등의 요소나 `<h2>`와 같은 제목 요소와 달리, `<main>`은 페이지의 개념적 구조를 바꾸지 않으며 온전히 정보 제공용입니다.

> 브라우저 호환성 이슈 : Internet Explorer 11 이하를 지원할 땐 `<main>` 요소에 `"main"` [role](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques#Landmark_roles) [ARIA](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques) 역할을 명시해 접근성을 확보하는 것이 좋습니다.

```
<main role="main">
  ...
</main>
```

<br />

## `<article>`
독립 적으로 구분해 배포하거나 재사용 할 수 있는 구획을 나타냅니다. 사용 예제로 게시판과 블로그 글, 매거진이나 뉴스 기사 등이 있습니다. 

- 예를 들어, 사용자가 스크롤하면 계속해서 다음 글을 보여주는 블로그의 경우, 각각의 글이 `<article>` 요소가 될 수 있고, 그 안에는 또 여러 개의 `<section>`이 존재할 수 있습니다.
- 주로 제목 요소(`<h1>` ~ `<h6>`)를 포함하여 각각의 <article>을 식별합니다.
- `<article>` 요소 안에 <article> 요소를 중첩할 수 있습니다.
- 작성자 정보를 `<address>` 요소를 이용하여 제공할 수 있습니다. 그러나 중첩 `<article>`에는 적용되지 않습니다.
- 작성일자와 시간은 `<time>` 요소의 `datetime` 속성을 이용하여 설명할 수 있습니다.

<br />

## `<section>`
독립적인 구획을 나타내며, 문서 요약에 해당 구획이 논리적으로 나타나야 할 때 사용합니다.

> 요소의 콘텐츠를 외부와 구분하여 단독으로 묶는 것이 나아보인다면 `<article>` 요소가 더 좋은 선택일 수 있습니다.

- 주로 제목 요소(`<h1>` ~ `<h6>`)를 포함하여 각각의 <article>을 식별합니다.
- `<section>` 요소는 `<address>`의 자손이 될 수 없습니다.
- `<section>` 요소를 일반 컨테이너로 사용하지 마세요. 특히 단순한 스타일링이 목적이라면 `<div>` 요소를 사용해야 합니다.

<br />

## `<aside>`
문서의 주요 내용과 간접적으로만 연관된 부분을 나타냅니다. 주로 사이드바 혹은 콜아웃 박스로 표현합니다.

- `<aside>` 요소는 `<address>`의 자손이 될 수 없습니다.

다음 예제는 글 내의 문단을 `<aside>`로 표시합니다. 해당 문단은 글의 주제와 간접적으로만 연결되어 있습니다.
```
<article>
  <p>
    디즈니 만화영화 <em>인어 공주</em>는
    1989년 처음 개봉했습니다.
  </p>
  <aside>
    인어 공주는 첫 개봉 당시 8700만불의 흥행을 기록했습니다.
  </aside>
  <p>
    영화에 대한 정보...
  </p>
</article>
```

<br />

## `<nav>`
현재 페이지 내, 또는 다른 페이지로의 링크를 보여주는 구획을 나타냅니다. 자주 쓰이는 예제는 메뉴, 목차, 색인입니다.

- 문서의 모든 링크가 `<nav>` 요소 안에 있을 필요는 없습니다. `<nav>` 요소는 주요 탐색 링크 블록을 위한 요소입니다. 대개 `<footer>` 요소가 `<nav>`에 들어가지 않아도 되는 링크를 포함합니다.
- 하나의 문서에서 여러 개의 `<nav>` 태그를 가질 수 있습니다. 이럴 때 [`aria-labelledby`](https://developer.mozilla.org/ko/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_aria-labelledby_attribute) 를 사용해 접근성을 향상할 수 있습니다.
- 스크린 리더 등 장애를 가진 사용자를 위한 사용자 에이전트는 최초 렌더링에서 탐색 전용 콘텐츠를 제외할지 결정할 때 `<nav>`를 참고합니다.

<br />

## `<address>`
사람, 단체, 조직 등에 대한 연락처 정보를 나타냅니다. 또한 `<article>` 내부에 배치해서 글의 작성자를 나타낼 수도 있습니다.

- `<address>` 요소는 `<address>`를 부모 요소로 가질 수 없습니다.
- `<address>` 요소 안에 반드시 포함해야 하는 정보는 연락처가 가리키는 개인, 조직, 단체의 이름입니다.
- 연락처 외의 정보(출판일 등)를 담아서는 안됩니다.

<br />

예제
```
<address>
	<a href="mailto:imdud0612@gmail.com">imdud0612@gmail.com</a><br />
	<a href="tel:+13115552000">(311) 555-2000</a>
</address>
```

`<a href="mailto:...">` 를 클릭하면, 각 플랫폼에서 지원하는 메일 쓰기 페이지/앱으로 이동합니다. <br />
`<a href="tel:...">` 를 클릭하면, 각 플랫폼에서 지원하는 전화 앱으로 이동합니다.

<br />

## `<div>`
아무 의미가 없는 영역을 나타냅니다. 스타일링 목적으로 사용합니다.

<br />

## `<ul>`/`<ol>`/`<li>`
순서가 있는 목록(`<ol>`) / 순서가 없는 목록(`<ul>`)에 사용합니다. `<li>` 태그는 목록의 각 아이템입니다.

- `<ol>`과 `<ul>`은 자식으로 `<li>`만 올 수 있습니다.
- `<li>`는 단독으로 사용할 수 없습니다.
- 항목의 순서를 바꿨을 때 의미도 바뀐다면 `<ol>`을 사용하세요. (단계별 요리법, 내비게이션, 영양정보에서 비율의 내림차순으로 정렬한 원재료 목록)
- `<ul>` 요소에서 스타일적 요소의 넘버링이 필요하다면 CSS의 list-style 속성으로 제어할 수 있습니다.

<br />

### `<ul>` 요소의 특성
- `type` : 넘버링 타입 ()

    - `a` : lowercase letters
    - `A` : uppercase letters
    - `i` : lowercase Roman numerals
    - `I` : uppercase Roman numerals
    - `1` : numbers (default)
    
        > `<li>` 태그에 별도로 `type` 속성을 명시하지 않으면 `<ol>` 태그의 `type` 속성이 적용됩니다. 

- `reversed` : 역순 정렬 (Boolean)
- `start` : 아이템에 넘버링을 할 때 첫 번째 순서를 나타내는 숫자

     > type 값이 A와 같이 문자이더라도, start 속성 값은 3과 같이 숫자만 지정할 수 있습니다.

<br />

예제
```
<ol type="1" reversed>
	<li>Mix flour, baking powder, sugar, and salt.</li>
	<li>In another bowl, mix eggs, milk, and oil.</li>
	<li>Stir both mixtures together.</li>
	<li>Fill muffin tray 3/4 full.</li>
	<li>Bake for 20 minutes.</li>
</ol>
```

<br />

### `<li>` 요소의 특성

- `value` : `<ol>` 요소 내부에서 이 값에서부터 번호를 매깁니다. 숫자만 넣을수 있습니다. 

> 부모 `<ol>` 요소에서 지정하는 유형을 덮어쓰는 `type` 속성은 사용이 중단됐습니다. 대신 CSS [list-style-type](https://developer.mozilla.org/ko/docs/Web/CSS/list-style-type) 속성을 사용하세요.

<br />

## `<dl>`/`<dt>`/`<dd>`
`<dl>` 태그는 설명 그룹의 목록을 나타냅니다. 설명 그룹은 용어(`<dt>`) + 정의(`<dd>`)를 한 그룹으로 합니다. 주로 용어사전 구현이나 메타데이터(키-값 쌍 목록)를 표시하는데 사용합니다. <br />
(Definition Term / Definition Details / Description List)

- `<dl>`은 `<dd>`, `<dt>`만을 포함해야 합니다.

<br />

### Styling
용어 그룹을 묶어서 스타일링할 때 `<div>` 태그를 사용할 수 있습니다.

```
<dl>
	<div>
		<dt>Beast of Bodmin</dt>
		<dd>A large feline inhabiting Bodmin Moor.</dd>
	</div>

	<div>
		<dt>Morgawr</dt>
		<dd>A sea serpent.</dd>
	</div>

	<div>
		<dt>Owlman</dt>
		<dd>A giant owl-like creature.</dd>
	</div>
</dl>
```

<br />

### 웹 접근성 고려
일부 스크린 리더는 `<dl>`의 콘텐츠를 리스트로 표현하지 않습니다. 따라서, 각 아이템의 콘텐츠는 리스트 그룹 내 다른 항목과의 관계를 표현할 수 있는 방식으로 작성해야 합니다. <br /><br />
웹 접근성을 고려하여 `<ul>`과 `<dfn>` 태그를 사용할 수 있겠네요.

> `<dfn>`은 용어 하나를 정의하는 태그입니다.

```
<ul>
	<li>
		<dfn>Beast of Bodmin</dfn>
		<p>A large feline inhabiting Bodmin Moor.</p>
	</li>

	<li>
		<dfn>Morgawr</dfn>
		<p>A sea serpent.</p>
	</li>

	<li>
		<dfn>Owlman</dfn>
		<p>A giant owl-like creature.</p>
	</li>
</ul>
```

<br />

## `<p>`
하나의 문단을 나타냅니다. HTML에서 문단은 이미지나 입력 폼 등 서로 관련있는 콘텐츠 무엇이나 될 수 있습니다.

- 콘텐츠를 문단으로 나누면 페이지의 접근성을 높입니다. 스크린 리더 등의 보조 기기는 `<p>` 태그를 사용하여 다음 문단으로 넘어갈 수 있는 단축키 등을 제공합니다.

<br />

### 닫는 태그 생략
자신의 닫는 태그(`</p>`) 이전에 다른 블록 레벨 태그가 분석되면 자동으로 닫힙니다.

> 닫는 태그는 `<p>` 요소의 바로 뒤에 `<address>`, `<article>`, `<aside>`, `<blockquote>`, `<div>`, `<dl>`, `<fieldset>`, `<footer>`, `<form>`, `<h1>-<h6>`, `<header>`, `<hr>`, `<menu>`, `<nav>`, `<ol>`, `<pre>`, `<section>`, `<table>`, `<ul>`, `<p>` 요소가 위치하는 경우, 또는 부모 태그의 콘텐츠가 더 존재하지 않고 부모가 `<a>` 요소가 아닐 때 생략할 수 있습니다.

<br />

## `<hr />`
문단을 분리합니다. 이야기 장면 전환, 구획 내 주제 변경 등 문단 레벨에서 주제의 분리를 나타냅니다.
> (Horizontal Rule)

- `<hr>`은 브라우저에서 시각적인 가로줄로 그려질 뿐만 아니라, 의미를 가집니다. 

<br />

예제
```
<p>
This is the first paragraph of text. 
This is the first paragraph of text.
</p>

<hr>

<p>
This is second paragraph of text. 
This is second paragraph of text.
</p>
```

<br />

### Styling
`<hr />` 요소는 사실 단순한 가로줄이 아닌, 납작한 박스 형태입니다. 기본적으로 모든 요소는 사각형의 박스 형태를 하고 있죠. 따라서 `border` 속성 값을 아래와 같이 작성하면, 해당 `<hr />` 요소가 그려내는 가로줄의 두께는 2px이 됩니다.

```
hr {
	border: 1px solid tomato;
}
```

가로줄을 숨기거나 꾸미려면 브라우저마다 제각각 적용된 `border` 스타일을 제거하세요. (`border: none`) 쓰면 됩니다.

```
hr {
	border: none;
	border-top: 1px solid tomato;
}
```
위와 같이 하면 `<hr />` 가로줄의 두께는 1px 입니다.

<br />

## `<pre>`
미리 서식을 지정한 텍스트를 나타내며, HTML에 작성한 내용 그대로 표현합니다. 내부에 [구문 콘텐츠](https://developer.mozilla.org/ko/docs/Web/Guide/HTML/Content_categories#%EA%B5%AC%EB%AC%B8_%EC%BD%98%ED%85%90%EC%B8%A0) 태그만 사용할 수 있습니다.
> (Preformatted Text)

<br />

### 접근성 고려사항
`<pre>` 요소로 만든 이미지나 도표에 대한 대체 설명을 지정하는 것이 중요합니다. 

```
<figure role="img" aria-labelledby="cow-caption">
  <pre>
  _______________________
< 나는 이 분야의 전문가다. >
  -----------------------
         \   ^__^ 
          \  (oo)\_______
             (__)\       )\/\
                 ||----w |
                 ||     ||
  </pre>
  <figcaption id="cow-caption">
    소 한 마리가 "나는 이 분야의 전문가다"라고 말하고 있습니다. 소는 미리 서식을 적용한 텍스트로 그려져있습니다.
  </figcaption>
</figure>
```

위의 예시에서는 `<figure>`, `<figcaption>` 태그, `id` 속성, ARIA `role`, `aria-labelledby` 속성을 조합하여 사용했습니다. `<pre>` 요소를 마치 이미지처럼 표현하면서 `<figcaption>` 요소를 사용하여 대체 설명을 제공하고 있습니다.

<br />

## `<blockquote>`
텍스트가 긴 인용문임을 나타냅니다. 주로 들여쓰기를 한 것으로 그려집니다.
> (Block Quotation)

- 인용문의 들여쓰기를 바꾸려면 CSS `margin-left`와 `margin-right`를 사용하세요.
- 별도의 블록을 쓰지 않아도 될 짧은 인용문은 `<q>` 요소를 사용하세요.

<br />

 속성|의미|값
 ---|---|---
 cite|인용문의 맥락 혹은 출처 정보를 가리키는 URL|URL
 
 <br />
 
 예제
 ```
<blockquote cite="https://www.huxley.net/bnw/four.html">
	<p>
		Words can be like X-rays, if you use them properly—they’ll go through
		anything. You read and you’re pierced.
	</p>
	<footer>—Aldous Huxley, <cite>Brave New World</cite></footer>
</blockquote>
```

<br />

## `<a>`
다른 페이지나 같은 페이지의 어느 위치, 파일, 이메일 주소와 그 외 다른 URL로 연결할 수 있는 하이퍼링크를 만듭니다. 
> Anchor

- `href` 특성을 통해 다른 URL로 이동할 수 있습니다.
- `<a>` 안의 콘텐츠는 링크 목적지의 설명을 나타내야 합니다.

### `<a>`요소의 특성
- `download` : 링크로 이동하는 대신 사용자에게 URL을 저장할지 물어봅니다. 값을 지정하면 저장할 때의 파일 이름으로서 제안합니다. `/`와 `\` 문자는 `_`로 변환합니다. 값이 없으면 파일 이름과 확장자는 브라우저가 다양한 인자로부터 생성해 제안합니다.(Content-Disposition HTTP 헤더, URL 경로의 마지막 조각, 미디어 유형)

    > `download`는 동일 출처 URL과 `blob:`, `data:` 스킴에서만 작동합니다.
                                                                                                                                               
- `href` : 하이퍼링크가 가리키는 URL. 링크는 HTTP 기반 URL일 필요는 없고, 브라우저가 지원하는 모든 URL 스킴을 사용할 수 있습니다.
- `hreflang`
- `ping`
- `rel`
- `target`

***
### _References_
- [HTML elements reference | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)
- [한눈에 보는 HTML 요소(Elements & Attributes) 총정리 | HEROPY Tech](https://heropy.blog/2019/05/26/html-elements/)