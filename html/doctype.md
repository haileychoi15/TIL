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

## `<html>` 태그
`<html>` 태그는 HTML 문서의 전체 범위를 지정합니다. 웹 브라우저가 해석해야 하는 HTML 문서가 어디에서 시작하며, 어디에서 끝나는지 알려주는 역할을 합니다.
`<html>` 태그 밖에 있는 내용은 문서의 범위에 해당하지 않으므로 웹 브라우저가 렌더링하지 않습니다.

### lang 속성
문서의 주요 언어를 설정합니다. 
```
<html lang="en-US">
	..
</html>
```

<br />

## `<head>` 태그
`<head>` 태그 안에서 사용하는 태그들은 HTML 문서의 정보를 가지고 있습니다.
```
<!DOCTYPE html>
<html>
	<head>
		..
	</head>
</html>
```
아래의 태그들은 `<head>` 태그 내에서 문서에 대한 정보, 외부 리소스 연결, CSS, 기준 URL을 작성할 때 사용합니다.
- `<title>`
- `<meta>`
- `<link>`
- `<style>`
- `<base>`

<br />

## `<title>` 태그
HTML 문서의 제목을 정의합니다.
웹 브라우저의 각 사이트 탭에서 이름으로 표시됩니다.
```
<head>
 <title>네이버</title>
</head>
```

<br />

## `<meta>` 태그
HTML 문서(웹페이지)에 관한 정보(표시 방식, 제작자(소유자), 내용, 키워드 등)를 검색엔진이나 브라우저에 제공합니다.
빈(Empty) 태그입니다.
```
<head>
 <meta charset="UTF-8">
 <meta name="author" content="최유영">
 <meta name="description" content="자기소개 사이트">
</head>
``` 
각 태그는 자신이 사용할 수 있는 속성과 값이 정해져 있습니다. <meta>에서 사용할 수 있는 속성은 다음과 같습니다.
- charset
- http-equiv
- name
- content
> [더 많은 속성과 설명보기](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta)

<br />

## 웹 표준 검사하기
우리가 작성한 HTML 문서가 표준에 부합하는지 테스트를 해볼 수 있습니다. [W3C validator](https://validator.w3.org/#validate_by_upload)
에 접속하여 작성한 HTML 문서를 업로드하고 기본적인 표준 여부를 판단할 수 있습니다.
> 사이트(페이지) 주소로 검사할 수도 있습니다.

<br />

***
### _References_
- [입문자에게 추천하는 HTML, CSS 첫걸음 | HEROPY Tech](https://heropy.blog/2019/04/24/html-css-starter/)
- [What’s in the head? Metadata in HTML | MDN](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/The_head_metadata_in_HTML)
