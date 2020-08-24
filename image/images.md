# 웹에서 사용하는 이미지(Image)

<br />

## 비트맵(Bitmap)과 벡터(Vector) 이미지
이미지(그래픽)는 크게 비트맵과 벡터로 구분됩니다.

<br />

### 비트맵(Bitmap)
비트맵(Bitmap)은 각 픽셀이 모여 만들어진 정보의 집합으로, 픽셀 단위로 화면에 렌더링합니다. 일반적으로 사용하는 대부분의 이미지가 비트맵 형식입니다. 그림판, 포토샵과 같은 툴로 편집할 수 있습니다.
> 레스터(Raster) 이미지라고도 부릅니다.

<br />

### 벡터(Vector)
수학적 정보의 형태(Shape)들이 만들어내는 결과물로, 이미지가 가지고 있는 점, 선, 면의 위치(좌표), 색상 등의 정보를 온전히 가지고 있습니다.
확대 및 축소를 해도 이미지가 깨지지 않으며 용량 변화가 없습니다.
일러스트 같은 툴로 편집할 수 있습니다.

<br />

## JPG(JPEG)
JPG(Joint Photographic coding Experts Group) Full-color와 Gray-scale의 압축을 위해 만들어졌으며 압축률이 훌륭합니다.
- 손실 압축
- 표현 색상도(24비트, 약 1600만 색상) 뛰어나 고해상도 표시장치에 적합
- 이미지의 품질과 용량을 쉽게 조절 가능

<br />

## PNG
PNG(Portable Network Graphics)는 Gif의 대체 포맷으로 개발되었습니다.
- 비손실 압축
- 8비트(256 색상) / 24비트(약 1600만 색상) 컬러 이미지 처리
- Alpha Channel 지원(투명도)
- W3C 권장 포맷

<br />

## GIF
GIF(Graphics Interchange Format)는 이미지 파일 내에 이미지 및 문자열 같은 정보들을 저장할 수 있습니다.
- 비손실 압축
- 여러 장의 이미지를 한 개의 파일에 저장가능(움짤, 애니메이션)
- 8비트 컬러만 지원

<br />

## WEBP
JPG, PNG, GIF를 모두 대체할 수 있는 구글이 개발한 이미지 포맷입니다.
- 완벽한 손실/비손실 압축 지원
- GIF 같은 애니메이션 지원
- Alpha Channel 지원(손실, 비손실 모두)
> 브라우저 호환성 문제로 많이 사용하지 않습니다. [WEBP 지원하는 브라우저](https://caniuse.com/#feat=webp)

<br />

## SVG
SVG(Scalable Vector Graphics)는 마크업 언어(HTML/XML) 기반의 벡터 이미지 포맷입니다.
- 해상도의 영향에서 자유로움
- CSS로 Styling 가능
- JavaScript로 Event Handling 가능
- 코드 혹은 파일로 사용 가능

<br />

***
#### _References_
- [입문자에게 추천하는 HTML, CSS 첫걸음 | HEROPY Tech](https://heropy.blog/2019/04/24/html-css-starter/)