# Components Styling
컴포넌트 스타일링이란 HTML에서 엘리먼트를 CSS로 스타일을 적용하는 것처럼 리액트의 컴포넌트로 생성될 엘리먼트에 스타일을 적용하는 것이다.

스타일링의 방식은 다음과 같다.
- 일반적인 CSS 방식
- CSS 전처리기 방식
- CSS-in-JS 방식

## 일반적인 CSS 방식
HTML에서 사용하는 CSS를 그대로 적용하는 방식이다. 주로 HTML의 class 속성을 사용하며, 외부 CSS파일에 스타일을 작성하여 리액트 js에서 불러와서 사용한다.

```javascript
import './App.css';

function App() {
  return (
    <div className="App">
	
    </div>
  );
}
```
App.css 파일은 리액트 프로젝트를 생성하면 함께 생성된다.

```css
.App {
  text-align: center;
}
```

리액트의 ``className``은 HTML에서 class와 같다.

```html
<div class="App">

</div>
```
위와 같이 처리된다.

CSS를 활용할 때는 일반적인 front-end 프로젝트처럼 모든 스타일을 하나의 CSS 파일이나 몇 개의 파일로 분할하여 작성하는 방법을 활용한다.

하지만 리액트의 경우 컴포넌트별로 따로 작성하는 경우가 많다. 각 컴포넌트별로 적용할 스타일을 따로 작성함으써 class 명이 중복되는 상황을 피할 수 있으며, 이 후 유지보수나 리뉴얼 시에 해당 부분만을 처리할 수 있는 점, 또 컴포넌트를 재활용하는 등의 유리한 장점을 얻을 수 있기 때문이다.

전체적으로 통일성있는 사이트 디자인을 위한 공통의 CSS를 작성하고 개별적인 컴포넌트를 위한 스타일링을 따로 하는 방식이 주된 방식이다.

### Inline Styling
컴포넌트에 개별적인 Inline styling을 적용할 수 있다. 이때 css 속성들은 js 객체 형식으로 ``style`` 속성에 작성한다.
```javascript
const MyComponent = () => {
	return (
		<div style={{color: "red", backgroundColor: "black"}}>BOX</div>
	);
}
```

또는 스타일을 작성한 변수를 활용할 수 있다.
```javascript
const MyComponent = () => {
	const divStyle = {color: "red", backgroundColor: "black"};

	return (
		<div style={divStyle}>BOX</div>
	);
}
```

Css 속성을 작성할 때는 kebab case를 camel case로 변환하면 된다.(font-size -> fontSize)


## 참고. CSS 변수활용
CSS도 변수를 선언하고 사용할 수 있는 기능을 제공한다.

CSS 변수도 전역와 지역으로 구분하여 사용할 수 있으며, HTML 요소의 계층구조에 따라 상속하여 사용할 수도 있다.

### 변수 선언
``--``와 ``:``을 사용하여 변수을 작성할 수 있다.

작성 문법은 ``--식별자: 값;``이다.

```css
:root {
	--main-color: #007bff;
	--sub-color: #17a2b8;
	--basic-size: 200px;
	--long-size: 500px;
}
```

``:root``는 변수의 범위를 전역으로 선언하는 의사 클래스이다. ``:root``는 문서 트리 구조의 최상위 요소에 해당하는 것으로 <html>과 같다고 볼 수 있다.

즉, 문서 전체에서 사용할 수 있는 변수가 됨을 나타낸다.

``:root``가 아닌 특정 요소를 선택한 스타일 범위에 변수를 작성하면 지역 변수가 된어, 그 범위 내에서만 사용할 수 있다.
