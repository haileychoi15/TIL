# HTML 문서의 정보

<br />

## DOCTYPE(DTD, 버전 지정)
DOCTYPE(DTD, Document Type Definition)은 마크업 언어에서 문서 형식을 정의합니다.
이는 웹 브라우저에 우리가 제공할 HTML 문서를 어떤 HTML 버전의 해석 방식으로 구조화하면 되는지를 알려줍니다.
> HTML은 크게 1, 2, 3, 4, X-, 5 버전이 있습니다.
```
 <!-- HTML 5 -->
 <!DOCTYPE html>
 
 <!-- XHTML 1.0 Transitional -->
 <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
```

<br/>

## `<html>` 요소
`<html>` 요소는 HTML 문서의 전체 범위를 지정합니다. 웹 브라우저가 해석해야 하는 HTML 문서가 어디에서 시작하며, 어디에서 끝나는지 알려주는 역할을 합니다.
`<html>` 요소 밖에 있는 내용은 문서의 범위에 해당하지 않으므로 웹 브라우저가 렌더링하지 않습니다.

### lang 속성
문서의 주요 언어를 설정합니다. 
```
<html lang="en-US">
	..
</html>
```

<br />

## `<head>` 요소
`<head>` 요소 안에서 사용하는 요소들은 HTML 문서의 정보를 가지고 있습니다.
```
<!DOCTYPE html>
<html>
	<head>
		..
	</head>
</html>
```
아래의 요소들은 `<head>` 요소 내에서 문서에 대한 정보, 외부 리소스 연결, CSS, 기준 URL을 작성할 때 사용합니다.
- `<title>`
- `<meta>`
- `<link>`
- `<style>`
- `<base>`

<br />

### `<link>` 요소
 `<link>` 요소는 현재 문서와 외부 리소스의 관계를 명시합니다.  `rel` 특성은 관계(relationship)를 뜻하며, 현재 문서와 연결한 아이템의 관계가 어떻게 되는지 설명합니다.

- 외부 스타일 시트를 연결하려면 `<head>` 안에 다음과 같은 `<link>` 요소를 배치하세요.

    ```
    <link href="main.css" rel="stylesheet">
  ```
- 사이트의 파비콘을 연결하려면 다음과 같이 사용합니다.

    ```
    <link rel="icon" href="favicon.ico">
  ```
> `rel` 의 다양한 값과 `<link>` 요소의 다른 특성들을 [여기](https://developer.mozilla.org/ko/docs/Web/HTML/Element/link) 에서 살펴보세요.
 
 <br />
 
### `<style>` 요소
`<style>` 요소는 문서의 `<head>` 안에 위치해야 합니다. 그러나, 일반적으로 스타일은 외부 스타일 시트에 작성하고, `<link>` 요소로 연결하는 편이 좋습니다. <br />
문서가 다수의 `<style>`과 `<link>` 요소를 포함하면 서로의 순서대로 DOM에 스타일을 적용합니다. 따라서 예상치 못한 종속 문제를 피하려면 올바른 순서를 따라 `<style>` 및 `<link>` 요소를 배치해야 합니다.

#### MIME 타입
MIME 타입이란 클라이언트에게 전송된 문서의 다양성을 알려주기 위한 메커니즘입니다. 브라우저들은 리소스를 내려받았을 때 해야 할 기본 동작이 무엇인지를 결정하기 위해 대게 MIME 타입을 사용합니다. MIME 타입은 대소문자를 구분하지는 않지만 전통적으로 소문자로 쓰여집니다.

- text/plain
- text/html
- image/jpeg
> [MIME 타입의 구조](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types)를 살펴보세요.

<br />

### `<base>` 요소
HTML `<base>` 요소는 문서 안의 모든 상대 URL이 사용할 기준 URL을 지정합니다. 문서에는 하나의 `<base>` 요소만 존재할 수 있습니다.

```
<base href="http://www.example.com/page.html">
```



## `<title>` 요소
HTML 문서의 제목을 정의합니다.
웹 브라우저의 각 사이트 탭에서 이름으로 표시됩니다.
```
<head>
 <title>네이버</title>
</head>
```

<br />

## `<meta>` 요소
`<meta>` 요소는 `<base>`, `<link>`, `<script>`, `<style>`, `<title>`과 같은 다른 메타관련 요소로 나타낼 수 없는 메타데이터를 나타냅니다.
HTML 문서(웹페이지)에 관한 정보(표시 방식, 제작자(소유자), 내용, 키워드 등)를 검색엔진이나 브라우저에 제공합니다.
빈(Empty) 요소입니다.
```
<head>
 <meta charset="UTF-8">
 <meta name="author" content="최유영">
 <meta name="description" content="자기소개 사이트">
</head>
``` 

<br />

### `<meta>` 요소 속성들
각 요소는 자신이 사용할 수 있는 속성과 값이 정해져 있습니다.

#### `charset` 
- 페이지의 문자 인코딩을 선언합니다.
- 값은 반드시 대소문자 구분없는 문자열 "`utf-8`"이어야 합니다.
 
#### `content`
- `http-equiv` 또는 `name` 특성의 값을 담습니다.
 
#### `http-equiv`
- 프래그마 지시문을 정의합니다.
- `content-security-policy` 는 현재 페이지의 콘텐츠 정책을 정의할 수 있습니다. 대부분의 콘텐츠 정책은 허용하는 서버 출처와 스크립트 엔드포인트를 지정해 사이트 간 스크립트 공격 방어에 도움을 줍니다.
- `content-type` 을 지정할 경우, `content` 특성의 값은 반드시 "`text/html; charset=utf-8`"이어야 합니다.
- `default-style` 는 기본 CSS 스타일 시트 세트의 이름을 지정합니다.
- `x-ua-compatible` 을 지정할 경우, `content` 특성의 값은 반드시 "`IE=edge`"여야 합니다. 사용자 에이전트는 이 프래그마를 무시해야 합니다.
- `refresh` 는 다음을 지정합니다.
    - `content` 특성에 양의 정수 값을 설정한 경우, 페이지를 다시 불러오기 전까지의 초 단위 대기시간.
    - `content` 특성이 양의 정수 값을 가지고 그 뒤를 문자열 `;url=`과 유효한 URL이 뒤따른다면, 해당 URL로 이동하기 전까지의 초 단위 대기시간.
        > 접근성 고려사항 주의 : refresh 값을 지정한 페이지의 경우 새로고침 사이 간격이 너무 짧을 우려가 있습니다. 스크린리더를 이용하는 사용자는 자동 새로고침 이전에 페이지의 내용을 읽고 이해하지 못할 수 있습니다. 또한 저시력 사용자에게 갑작스럽고 사전 안내도 없는 콘텐츠 업데이트는 어지러울 수 있습니다. 

#### `name`
- `name`과 `content` 특성을 함께 사용하면 문서의 메타데이터를 이름-값 쌍으로 제공할 수 있습니다. 
- `name`은 이름, `content`는 값을 담당합니다.
> [표준 메타데이터 이름](https://developer.mozilla.org/ko/docs/Web/HTML/Element/meta/name) 문서에서 HTML 명세에 포함된 표준 메타데이터 목록을 살펴보세요.

<br />

## 웹 표준 검사하기
우리가 작성한 HTML 문서가 표준에 부합하는지 테스트를 해볼 수 있습니다. [W3C validator](https://validator.w3.org/#validate_by_upload)
에 접속하여 작성한 HTML 문서를 업로드하고 기본적인 표준 여부를 판단할 수 있습니다.
> 사이트(페이지) 주소로 검사할 수도 있습니다.

<br />

***
### _References_
- [&lt;meta&gt;: 문서 레벨 메타데이터 요소 | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta)
- [&lt;link&gt;: 외부 리소스 연결 요소 | MDN](https://developer.mozilla.org/ko/docs/Web/HTML/Element/link)
- [&lt;style&gt;: 스타일 정보 요소 | MDN](https://developer.mozilla.org/ko/docs/Web/HTML/Element/style)
- [&lt;base&gt; | MDN](https://developer.mozilla.org/ko/docs/Web/HTML/Element/base)
- [What’s in the head? Metadata in HTML | MDN](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/The_head_metadata_in_HTML)
- [MIME 타입 | MDN](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types)
- [입문자에게 추천하는 HTML, CSS 첫걸음 | HEROPY Tech](https://heropy.blog/2019/04/24/html-css-starter/)
