# Component
React는 SPA(Single Page Application) 방식의 View 라이브러리이다.

다양한 화면의 처리를 위해 다수의 HTML 페이지를 작성하는 방식이 아닌 하나의 HTML 페이지에 Contents를 바꾸는 방식으로 동작한다.

이러한 Contents를 컴포넌트(Component)라고 한다.

컴포넌트는 하나의 페이지가 될 수 있으며, ``<button>``이나 ``<div>``와 같은 하나의 element가 될 수도 있다. 즉, 여러 컴포넌트로 하나의 컴포넌트를 구성할 수 있다.

## Class Component vs. Function Component
컴포넌트는 클래스형 컴포넌트와 함수형 컴포넌트로 작성하는 방법이 있다.

### Class Component
클래스형 컴포넌트는 Component class를 상속하여 작성하며, 화면에 출력할 element를 render() 함수에 작성하는 방식이다.

```javascript
import React, { Component } from 'react';
 
class MyComponent extends Component {
  render() {
    const name = '홍길동';
    return <div className="react">{name}</div>;
  }
}
 
export default MyComponent;
```

#### Class Component의 장단점
클래스 내장 변수인 state를 생성하여 활용할 수 있으며, 라이프사이클의 각 단계에 해당하는 기능을 사용할 수 있고 임의 메서드를 정의하여 활용할 수 있다.

반면 가독성이 함수형에 비해 떨어지며 작성이 어렵다.

### Function Component
함수형 컴포넌트는 첫글자를 대문자로 하여 javascript 함수 형태로 작성하는 방식이다.

```javascript
import React from 'react';
 
function MyComponent {
  const name = '홍길동';

  return <div className="react">{name}</div>;  
}
 
export default MyComponent;
```

또는

```javascript
import React from 'react';
 
const MyComponent = () => {
  const name = '홍길동';

  return <div className="react">{name}</div>;  
}
 
export default MyComponent;
```

#### Function Component의 장단점
클래스형 컴포넌트에 비해 작성이 쉽지만 stat와 같은 내장 변수를 사용할 수 없다. 이 단점은 React 16.8 버전부터 React Hook이 도입되면서 함수에서도 state와 라이프사이클 메소드도 사용할 수 있게 되면서 해결되었다.

현재는 함수형 컴포넌트 작성 방식을 권장하고 있다.

함수형 컴포넌트의 장점
- 클래스형 컴포넌트보다 선언하기가 편하고, 작성 코드가 더 적다.
    - 클래스 형은 Class 선언, render()함수 선언, Component 상속을 해야하고, 상태관리를 위해 constructor, 생성자 메소드 전언 등이 필요하다.
- 클래스형 컴포넌트보다 메모리 자원을 적게 사용한다.
- 클래스형 컴포넌트보다 빌드 후 파일 크기가 더 작다.
- 함수형 컴포넌트는 render()함수가 필요 없어서 컴포넌트 마운트 속도가 더 빠르고, 가독성이 좋다.

따라서 본 강의에서는 함수형 컴포넌트를 활용한다.

### 함수형 컴포넌트 작성법
함수형 컴포넌트의 기본적인 형식은 다음과 같다.

MyComponent.js
```javascript
import React from 'react';
 
const MyComponent = (prop) => {
  return <div>나의 컴포넌트</div>;  
}
 
export default MyComponent;
```

- 기본적으로 React를 import한다.
- 파일명과 동일한 함수명으로 컴포넌트를 작성한다. 이 때 함수명 및 파일명의 첫글자를 ``대문자``로 작성한다.
- function 키워드를 사용하여 작성하거나 화살표 함수(함수 표현식)로 작성할 수 있다.
- 부모 컴포넌트로 부터 받는 prop가 있을 경우 함수의 인자로 작성한다.
- useState, useEffect 등의 hook을 함수 내부 또는 외부의 필요한 위치에 작성한다.
    - 마찬가지로 필요한 변수 또는 상수를 작성한다.
- return 문에 jsx 문법으로 화면에 보여질 html 요소를 작성한다.
- 마지막 문장으로 다른 파일에서 MyComponent 파일을 import해올 때 MyComponent로 불러올 수 있도록 export를 작성한다.

## 컴포넌트 활용
작성한 컴포넌트는 App.js나 다른 컴포넌트에서 활용할 수 있다.
```javascript
import './App.css';
import MyComponet from './components/MyComponent';

function App() {
  return (
    <div className="App">
      <MyComponent />
    </div>
  );
}

export default App;
```

## 컴포넌트로 데이터 전달
### props
props(properties)는 부모 컴포넌트에서 자식 컴포넌트의 속성을 설정할 때 사용하는 요소이다.

예를 들어,
```html
<input type="text" name="data">
```
html 요소에서 ``type``이나 ``name``과 같은 속성을 설정하여 사용한다.

React에서 ``input`` 요소를 위한 컴포넌트를 만들었다고 한다면, 부모 컴포넌트에서 ``input`` 컴포넌트에 ``type`` 속성을 설정할 때 props를 사용하게 된다.

```javascript
const MyInput = (props) => {
  return <input type={props.type} name={props.name} />
}
```
부모 컴포넌트에서 ``MyInput``을 사용하면 다음과 같다.
```javascript
function App() {
  return (
    <MyInput type="text" name="data" />
  );
} 
```

부모 컴포넌트인 ``App``의 ``MyInput``에서 설정한 ``type`` 속성과 ``name`` 속성의 값은 ``props``로 묶여 ``MyInput`` 컴포넌트로 전달되고, ``MyInput``의 ``<input>`` 태그에서 ``props.type``과 ``props.name``으로 사용된다.

props의 원래 목적은 자식 컴포넌트의 속성을 설정하는 것이지만, 이를 활용하여 부모 컴포넌트에서 자식 컴포넌트로 데이터를 보낼 때 사용할 수 있다.
```javascript
function App() {
  return (
    <MyComponet data="hello world" />
  );
}
```
```javascript
const MyComponent = (props) => {
  return <div>{props.data}</div>;
};
```

### props.children
부모 컴포넌트에서 자식 컴포넌트의 시작 태그와 종료 태그 사이에 작성하는 내용(content)은 ``porps.children``으로 전달할 수 있다.
```javascript
function App() {
  return (
    <MyComponet data="hello world">안녕하세요.</MyComponent>
  );
}
```
```javascript
const MyComponent = (props) => {
  return (
    <>
      <div>data : {props.data}</div>
      <div>{props.children}</div>
    </>
  );
};
```

### Destructing을 활용한 props 데이터 추출
여러 개의 property 값을 넘기는 경우 각 property 마다 ``props.``을 붙이는 것은 불편하다.

이 부분은 ES6 문법의 Destructing을 활용하면 좀 더 편하게 할 수 있다.
```javascript
const MyComponent = (props) => {
  const { data, children } = props;

  return (
    <>
      <div>data : {data}</div>
      <div>{children}</div>
    </>
  );
};
```

Destructing은 매개변수 부분에서 처리하는 것도 가능하다.
```javascript
const MyComponent = ({ data, children }) => {
  return (
    <>
      <div>data : {data}</div>
      <div>{children}</div>
    </>
  );
};
```
Property에 기본값을 설정하지 않는다면 위와 같은 방식이 좀더 유용하다.

### props 기본값 설정
최신 React 문법에서 ``defaultProps``가 ``deprecated`` 됨으로써 props의 기본값을 설정하기 위해 ``Default parameters``를 사용한다.

``props``의 Destructing을 수행하면서 기본값을 설정하는 방식이다.
```javascript
const MyComponent = (props) => {
  const {
    data = 'hi~',
    children
  } = props;

  return (
    <>
      <div>data : {data}</div>
      <div>{children}</div>
    </>
  );
};
```
위와 같이 선택적으로 기본값을 설정하여 사용한다.

물론 매개변수 부분에서 처리하는 것도 가능하다.
```javascript
const MyComponent = ({ data = 'hi~', children }) => {
  return (
    <>
      <div>data : {data}</div>
      <div>{children}</div>
    </>
  );
};
```

### props 검증
``propTypes``라는 함수를 사용하여 컴포넌트에서 props로 넘어오는 값의 자료형과 필수 전달 속성 등을 설정할 수 있다.

```javascript
const MyComponent = ({ data, children, reqProps }) => {
  return (
    <>
      <div>data : {data}</div>
      <div>{children}</div>
      <div>number : {reqProps}</div>
    </>
  );
};

MyComponent.propTypes = {
  data: PropTypes.string,
  reqProps: PropTypes.number.isRequired,
};
```
``data`` props는 String 이어야 하며, 다른 자료형일 경우 console에 경고가 뜨게 된다.

``reqProps``가 넘어오지 않을 경우 마찬가지로 경고가 뜬다.

