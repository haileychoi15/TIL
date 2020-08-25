# 블록(Block level)요소 / 인라인(Inline)요소
블록(Block) vs. 인라인(Inline) 요소 개념은 HTML 4.01 이하 버전에서 계속 사용되었습니다. HTML 5 부터는 조금 더 복잡한 [Content categories](https://developer.mozilla.org/ko/docs/Web/Guide/HTML/Content_categories) 개념으로 대체되었습니다. 하지만 블록/인라인 개념은 여전히 페이지 레이아웃을 이해하는데 유효한 중요한 개념입니다.
<br />
> 일반적으로 블록 레벨 요소는 인라인 요소와 (때때로) 다른 블록 레벨 요소를 포함할 수 있습니다. 이런 고유한 구조적 차이점으로 인해 블록 레벨 요소는 인라인 요소보다 더 큰 구조를 생성할 수 있습니다.

<br />

## 블록(Block level)요소
- 사용가능한 최대 가로 너비를 사용합니다.
- 새로운 줄에서 시작합니다.
- 크기를 지정할 수 있습니다.(`width: 100%; height: 0;` 으로 시작)
- 브라우저에서 기본값은 `width: auto; height: auto;`

- 예) `<div>`, `<h1>`, `<section>`, `<table>`, `<p>` 태그 등
> [모든 블록 레벨 요소 보기](https://developer.mozilla.org/en-US/docs/Web/HTML/Block-level_elements#Elements)

<br />

## 인라인(Inline)요소
- 콘텐츠 만큼의 너비를 사용합니다.(`width: 0; height: 0;` 으로 시작)
- 줄의 어느 곳에서나 시작할 수 있습니다.
- 크기를 지정할 수 없습니다.
- `margin`/`padding` 속성의 위/아래(`top`/`bottom`) 값을 지정할 수 없습니다. 무조건 0 입니다.

    > 주의 : `padding` 속성의 경우 `bottom` 값을 지정하고 시각적으로 구현할 수도 있습니다. 하지만 외부의 다른 요소와의 거리를 구현하기 위해 사용하지 마십시오. 요소간의 거리를 형성하는 것은 `margin` 속성의 역할일 뿐더러, 인라인 요소의 `padding-bottom` 값은 아래에 위치한 요소와의 거리를 형성하지 못해 요소가 겹치는 문제가 발생합니다.
- 브라우저에서 기본값은 `width: auto; height: auto;`
- 예) `<span>`, `<a>`, `<img>`, `<data>`, `<u>` 태그 등
> [모든 인라인 요소 보기](https://developer.mozilla.org/en-US/docs/Web/HTML/Inline_elements#Elements)

<br />

***
### _References_
- [Block-level elements | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Block-level_elements)
- [Inline elements | MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Inline_elements)
- [Block and inline layout in normal flow | MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flow_Layout/Block_and_Inline_Layout_in_Normal_Flow)
