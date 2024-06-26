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

