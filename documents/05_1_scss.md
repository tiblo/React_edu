# CSS 전처리기(Preprocessor)
CSS 전처리기는 변수와 제어용 문장, 내장함수 등이 제공되며 문법에 따라 작성한 문장을 컴파일하여 CSS로 변환하는 방식이다.

종류
- Sass(Scss)
- Less
- Stylus

![image](https://github.com/tiblo/React_edu/assets/34559256/c8ccdf97-3be4-493f-955e-4d32e348ce3e)

(이미지 출처 : https://nykim.work/97)

여기에서는 Sass를 다룬다.

SASS(SCSS) - Syntactically Awesome Style Sheets.(문법적으로 멋진 스타일시트)

- 단순히 반복되는 내용을 줄이고 효율적으로 사용할 수 있도록 만든 CSS 전처리기 스타일시트 언어

## Sass vs. Scss
Scss는 Sass에서 지원하는 확장자 형식으로 두 가지는 동일한 전처리기(같은 라이브러리)이지만 작성 문법이 조금 다르다.

.sass
```css
body
	background: yellow
	color: blue
```

.scss
```css
body {
	background: yellow;
	color: blue;
}
```
(예제 출처 : 리액트를 다루는 기술[개정판])

위의 예제에서 보듯 scss가 css와 유사한 구조를 가지고 있기 때문에 일반 css의 경험이 있다면 조금 더 쓰기가 편하다.

.sass 확장자는 중괄호({})와 세미콜론(;)을 사용하지 않고 작성하는 형식이다.

여기에서는 css와 유사한 scss를 사용한다.

## Sass 설치 및 활용
Scss를 사용한 하려면 scss로 작성한 내용을 css로 변환하기 위한 ``node-sass``라는 라이브러리가 필요하다.

```
> yarn add node-sass
```

확장자가 ``.scss``인 파일을 생성하여 스타일시트를 작성한다.(components 폴더 하위에 css용 폴더를 생성하여 작성하는 것이 좋다.)

예) components 폴더에 scss 폴더를 생성하고 ``mystyle.scss``파일을 생성한다.
```css
.mydiv {
	width: 200px;
	height: 50px;
	border: 1px solid red;
}
```

```javascript
import React from "react";
import "./scss/mystyle.scss";

function MyComponet({ data, children }) {
	return (
		<div className="mydiv">
			<div>data: {data}</div>
			<div>{children}</div>
		</div>
	);
}

export default MyComponet;
```

![image](https://github.com/user-attachments/assets/08d6621a-7fde-4869-bb4c-8a99a843eb4a)


## 문법
Scss 문서를 작성하는 기본적인 문법은 일반 css(선택자와 속성)와 동일하다. 

### 주석
``//``를 사용하여 한줄 주석을 작성할 수 있으며, ``/* ... */``를 사용하여 블록 주석을 작성할 수 있다.

### 변수
Scss는 변수의 사용을 지원한다. 반복적으로 사용하는 값들(색상, 글꼴, 간격, 크기 등)을 변수에 저장하여 사용할 수 있다.

변수를 정의할 때는 ``$`` 기호를 사용한다.

```css
$main-color: #0000ff;
$sub-color: #00ffff;
$m-size: 100;
```
``$`` ``변수명`` ``:`` ``설정값`` ``;`` 순으로 작성한다.

변수를 사용할 때도 ``$`` 기호를 사용한다.
```css
body {
	background-color: $main-color;
	width: #{$m-size}px;
	height: #{$m-size}%;
}
```
수치값을 저장하거나 파일명과 같은 변화되는 값을 저장한 변수를 사용할 때 ``#{}``를 활용할 수 있다.
``m-size`` 값은 ``width``에서는 100px로 사용되고, ``height``에서는 100%로 사용된다.


### 중첩
계층화 되어 있는 요소에 스타일을 적용할 때 활용하는 문법으로, 부모 요소의 스타일 영역에 자식 요소의 스타일을 정의하는 방식이다.

```html
<div class="grand-parent">
	<div class="parent">
		<div class="child"></div>
	</div>
</div>
```
Html의 구조가 위와 같을 때 css로 스타일을 작성하면 다음과 같다.
```css
.grand-parent {
	background: red;
}
.grand-parent>.parent {
	background: green;
}
.grand-parent>.parent>.child {
	background: blue;
}
```

Scss의 중첩을 사용하면 다음과 같이 작성할 수 있다.
```css
.grand-parent {
	background: red;

	.parent {
		background: green;

		.child {
			background: blue;
		}
	}
}
```
요소의 계층 구조에 맞춰 스타일을 작성하여 직관적으로 파악할 수 있게 된다. 또한 클래스명을 중복해서 작성하지 않아도 되는 편의성이 제공된다.

#### 중첩 속성
css 속성들 중에는 background-, padding- 등과 같이 '하이픈 구분 속성'(Hyphen-separated propeties)들은 중첩하여 간결하게 표현할 수 있다.
```css
div {
	background-image: url(...);
	background-repeat: no-repeat;
	background-size: cover;
}
```
위의 예는 다음과 같이 작성할 수 있다.
```css
div {
	background: {
		image: url(...);
		repeat: no-repeat;
		size: cover;
	}
}
```

### 부모 선택자 참조
``&`` 선택자는 중첩 상태일 때 상위 선택자를 대체하는 기호이다. 

```html
<div class="content-grand-parent">
	<div class="content-parent">
		<div class="content-child"></div>
	</div>
</div>
```
위와 같이 클래스명이 지정되어 있을 경우 다음과 같이 ``&``를 사용하여 작성할 수 있다.
```css
.content {
	&-grand-parent {	/* .content-grand-parent 가 된다. */
		background: red;
	
		&-parent {
			background: green;
	
			&-child {
				background: blue;
			}
		}
	}
}
```
``&``는 가상 선택자를 활용한 스타일 작성에도 활용한다.
```css
.box-div {
	background-color: blue;

	&:hover {
		background-color: gray;
	}
}
```
그 외에도 다중 클래스 활용, 같은 스타일을 사용하는 요소와 요소 사이의 스타일 등에서도 활용한다.
```css
.box-div {
	background-color: blue;
	color: white;
	width: 500px;
	height: 50px;
 
	&.w-10 {
		width: 10%;
	}
	
	& + & {
		margin-top: 50px;
	}
};
```
``+`` 컴포넌트와 컴포너트 사이를 나타낸다. ``& + &``는 같은 선택자를 사용하는 컴포넌트 사이에 적용될 스타일을 설정하는 것을 나타낸다.

두 번째 ``&`` 대신 다른 컴포넌트의 선택자가 올 수 있으며, 예를 들어 ``& + p``이면 ``.box-div``와 ``<p>`` 컴포넌트가 연속적으로 작성되어 있을 때 스타일이 적용된다.

```javascript
const MyComponent = () => {
	return (
		<div>
			<div className="box-div">BOX1</div>
			<div className="box-div w-10">BOX2</div>
			<div className="box-div">BOX3</div>
			<div className="other">BOX4</div>
		</div>
	);
}
```
위 코드에서 ``BOX2`` div는 가로길이가 10%로 표현되며, class가 ``box-div``인 ``div``들 간 사이에 margin-top이 50px씩 적용된다.(``BOX3``과 ``BOX4`` 사이에는 margin-top이 적용되지 않는다.

![image](https://github.com/user-attachments/assets/ae5f2d13-f8c5-47d1-9da7-b8d41815d874)


### Mixins
Scss에서는 ``@mixin``을 사용하여 함수와 같은 형태의 스타일 블록을 정의하여 사용할 수 있다.

Mixin은 재사용이 가능한 스타일을 정의할 수 있는 문법이다.

재사용 가능 스타일을 정의할 때는 ``@mixin``을 앞에 붙여주고, 사용할 때는 ``@include``를 붙인다.

#### @mixin
@mixin은 재사용이 가능한 스타일을 정의하는데 사용되는 선언이다. 

```css
@mixin my-style {
	color: blue;
	margin: 0;
}
```

mixin 내부에서 ``&``나 중첩을 사용할 수도 있다.

#### @include
@mixin으로 정의된 스타일을 불러와서 사용할 때는 @include를 붙인다.

```css
div {
	@include my-style;
}
```
다음과 같이 처리된다.

```css
div {
	color: blue;
	margin: 0;
}
```

#### 인수(파라미터) 처리
스타일 property와 값을 인수로 받아서 처리할 수 있다.

```css
@mixin myMixin($props, $value) {
	#{$props}: $value;
}

.box1 {
	@include myMixin(width, 100px);
	@include myMixin(height, 50px);
	border: 1px solid black;
}
```
인수가 property로 사용될 때는 ``#{}``로 감싸줘야 한다. props는 동적으로 변경되는 속성 이름이기 때문에 문자열로 변환하여 속성으로 처리하기 위해 ``#{}``을 사용한다.

다음과 같이 변환된다.
```css
.box1 {
	width: 100px;
	height: 50px;
	border: 1px solid black;
}
```

##### 인수의 기본값 설정
인수는 기본값을 설정할 수 있다. 변수 뒤에 ``: 기본값`` 형식으로 작성한다.

```css
@mixin myMixin($props, $value: 100px) {
	#{$props}: $value;
}

.box1 {
	@include myMixin(width);
	@include myMixin(height, 50px);
	border: 1px solid black;
}
```
``$value`` 값을 넣지 않으면 기본값인 ``100px``이 적용된다.

##### 키워드 인수
인수가 들어갈 변수의 이름을 ``@inclue``에서 사용하여 순서에 구애받지 않고 사용할 수 있는데 이것을 키워드 인수라고 한다.

```css
@mixin myMixin($props, $value: 100px) {
	#{$props}: $value;
}

.box1 {
	@include myMixin(width);
	@include myMixin($value: 50px, $props: height);
	border: 1px solid black;
}
```

##### 가변 인수
인수 뒤에 ``...``을 붙임으로서 가변 인수로 만들 수 있다.
```css
@mixin myPadding($size...) {
	padding: join($size, (), $separator: space);
}

.box1 {
	@include myPadding(10px, 20px, 30px, 40px);
}
.box2 {
	@include myPadding(10px, 20px, 30px);
}
.box3 {
	@include myPadding(10px, 20px);
}
.box4 {
	@include myPadding(10px);
}
```

##### Content Blocks
mixin으로 정의된 스타일 외에 고유 스타일을 지정하기 위해 사용하는 것이 content block이다.

``@content;`` 키워드를 사용하여 content block을 처리할 수 있다.

```css
@mixin myBox($size) {
	width: $size;
	height: $size;
	@content;
}

/* content block을 사용 안함 */
.box1 {
	@include myBox(100px);
}

/* content block을 사용함 */
.box2 {
	@include box-style(200px) {
		border: 1px solid red;
	};
}
```

``box1``의 경우 ``@content;``부분에 들어갈 속성을 지정하지 않았기 때문에 크기만 표현되고, ``box2``는 크기와 함께 고유 스타일인 테두리가 나타난다.

#### 연산자
Scss는 연산자를 사용하여 값을 변경할 수 있다.

|연산자|내용|
|---------|-------------|
|+, -, *, /, %|산술 연산자|
|==, !=, >, >=, <, <=|비교 연산자|
|and, or, not|논리 연산자|

Scss의 연산자에는 몇가지 주의사항이 있다.
1. 연산은 ``px``로만 수행하며, ``px``가 아닌 다른 단위의 경우 css의 ``calc()`` 함수를 사용해야 한다.
```css
	padding: 10px + 20px;
	margin: calc(10vw - 5vw);
```
2. ``/`` 연산자는 다음 조건에 만족할 때만 나누기 연산을 수행한다.
 - 변수에 저장된 값이거나 함수의 반환값이어야 한다.
 - 수식을 ``()``로 묶어야 한다.
 - 다른 산술 식과 함께 사용해야 한다.
```css
	padding: $size / 2;
	padding: (10 / 2);
	padding: 3 * 8 / 4;
```
3. 문자열을 결합하는 ``+`` 연산자는 왼쪽의 피연산자에 따라 결과를 다르게 연산한다.
 - "str1" + str2 => "str1str2" : 왼쪽 값이 ``"``로 묶여 있기 때문에 결과값도 ``"``로 묶인다.
 - str1 + "str2" => str1str2 : 왼쪽 값이 ``"``로 묶여 있지 않기 때문에 결과값이 ``"``로 묶이지 않는다.   
4. ``-``와 ``/``는 문자열 앞에 붙으면 단항 연산자로 처리되는데, 해당 값 앞에 붙게된다.
 - $str: / someUri => /someUri
 - $str: - someValue => -someValue

##### 색상 연산
``%`` 연산자를 제외한 나머지 산술 연산자로 색상을 조절할 수 있다.
1. 덧셈 연산자를 사용해 색상을 더 밝게할 수 있다.
2. 뺄셈 연산자를 사용해 색상을 어둡게할 수 있다.
3. 곱셈 연산자를 사용해 색상의 밝기나 채도를 조절할 수 있다.
4. 나눗셈 연산자를 사용해 색상의 밝기나 채도를 조절할 수 있다.

색상 연산식은 2항 연산식으로만 작성할 수 있다.

또 scss는 밝기 조절을 위한 ``lighten()``과 ``darken()``, 채도 조절을 위한 ``saturate()``와 ``desaturate()`` 함수를 제공한다.
```css
$base-color: #3498db; // 파란색

// 색상의 채도를 20% 증가시킴
$saturated-color: saturate($base-color, 20%);
```

이 4가지 함수는 모두 ``(색상, 비율)`` 형식으로 인자를 작성한다.
