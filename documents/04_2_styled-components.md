# CSS-in-JS
자바스크립트 안에 스타일을 선언하는 방식을 CSS-in-JS 방식이라고 한다. 

스타일 정의를 위한 css 파일을 따로 작성하는 것이 아니라 JS 컴포넌트에 바로 삽입하는 방식이다.

## styled-components
CSS-in-JS 방식에서 현재 가장 많이 사용되고 있는 styled-components이다. 

### 패키지 설치
React에서 styled-components를 사용하기 위해서는 패키지를 설치해야 한다.
```
> yarn add styled-components
```

컴포넌트에서 styled-components를 위한 확장을 사용하면 편하게 작업할 수 있다.
- vscode-styled-components
- styled-components-snippets

### 기본 문법
설치한 styled-components 패키지의 ``styled``를 import 해야 한다.
```javascript
...
import styled from "styled-components";
...
```

알려진 html 태그에 대해서 이미 정의되어 있기 때문에 해당 태그명으로 속성을 작성한다.
```javascript
styled.div`
  // div 요소에 대한 css 속성을 작성.
`'
```
css 속성은 `` ` ``(백틱)을 사용하는 Template Literal로 작성한다.

보통 컴포넌트 함수 정의 부분보다 위쪽에 컴포넌트에서 사용할 html 요소에 대한 styled-components를 정의한다.(<b>작성 순서는 상관없다.</b>) 

변수를 사용하여 styled-components를 저장하고 컴포넌트에서 사용하는 방식이 일반적이다.

```javascript
import React from "react";
import styled from "styled-components";

const MyDiv = styled.div`
  width: 200px;
  height: 100px;
  padding: 5px;
  border-radius: 5px;
  font-size: 1rem;
  border: 1px solid blue;
`;

function MyStyledComponet({ props }) {
  return <MyDiv>{props.children}</MyDiv>;
}

export default MyStyledComponet;
```

프로젝트를 실행하여 브라우저에서 html 요소를 확인하면 styled-components는 css 클래스로 처리되며, 이때 클래스명은 자동으로 생성된다.

### 자바스크립트 표현식 활용
Styled-components는 Template Literal로 작성하는데 그 안에 자바스크립트의 표현식을 활용할 수 있다. 즉, 변수나 조건연산식 등을 ``${}``로 감싸서 작성하면 동적인 처리가 가능해 진다.

### 가변 스타일링
styled-components는 일종의 컴포넌트이기 때문에 react 컴포넌트로부터 props를 사용하여 값을 받을 수 있으며, props에 따라 스타일을 변경하도록 작성할 수 있다.

```javascript
import React from "react";
import styled from "styled-components";

const MyDiv = styled.div`
  width: 200px;
  height: 100px;
  padding: 5px;
  border-radius: 5px;
  font-size: 1rem;
  border: 1px solid blue;

  background-color: ${(props) => props.bgcolor || "white"};
`;

function MyStyledComponet({ props }) {
  return <MyDiv bgcolor="gray">{props.children}</MyDiv>;
}

export default MyStyledComponet;
```

``||``를 사용하여 기본값을 설정할 수 있다. react 컴포넌트에서 ``bgcolor``를 작성하지 않으면 div는 배경색이 흰색으로 표현된다.

### ``css``함수를 활용한 가변 스타일링
React 컴포넌트로부터 넘어오는 props의 유무에 따라 다수의 css 속성을 변경해야 할 때는 ``css`` 함수를 사용하여 스타일을 정의한다.

``css``함수를 사용하려면 먼저 import 해야한다.
```javascript
...
import styled, { css } from "styled-components";
...
```
```javascript
import React from "react";
import styled from "styled-components";

const MyDiv = styled.div`
  width: 200px;
  height: 100px;
  padding: 5px;
  border-radius: 5px;
  font-size: 1rem;
  border: 1px solid blue;

  ${(props) =>
    props.reverse &&
    css`
      color: white;
      background-color: black;
      border-color: red;
    `}
`;

function MyStyledComponet({ props }) {
  return <MyDiv reverse>{props.children}</MyDiv>;
}

export default MyStyledComponet;
```
먼저 ``reverse``가 있는지의 여부를 확인하고 있으면 ``css``로 묶여있는 css 속성이 표현되는 형식이다.


### 전역 스타일링
Styled-components는 사이트의 모든 컴포넌트에서 공통으로 적용할 스타일을 정의할 수 있는 ``createGlobalStyle``함수를 제공한다.

전역 스타일용 styled-components를 하나의 파일로 작성하여 다른 컴포넌트에서 import하여 사용할 수 있다.

먼저 createGlobalStyle을 import 한 후 모든 사이트에 적용될 css 속성을 작성한다.

```javascript
import { createGlobalStyle } from "styled-components";

const MainStyle = createGlobalStyle`
  * {
    padding: 0;
    margin: 0;
  }
  ...
`;

export default MainStyle;
```

App.js에 작성한 전역 스타일 컴포넌트를 최상위 컴포넌트로 추가한다.
```javascript
import MainStyle from './MainStyle';
...

function App() {
  return (
    <div className="App">
      <MainStyle />
      ...
    </div>
  );
}
```

### 변수 활용
#### props를 활용
위의 [가변 스타일링](#가변-스타일링)과 같이 props로 변수를 전달하는 방식으로 활용한다. 

```javascript
import styled from 'styled-components';

const StyButton = styled.button`
  background-color: ${props => props.pri ? 'blue' : 'gray'};
  color: ${props => props.pri ? 'white' : 'black'};
  padding: 10px;
  border: none;
  border-radius: 5px;
`;

function MyButton() {
  return (
    <div>
      <StyButton pri>Primary Button</StyButton>
      <StyButton>Secondary Button</StyButton>
    </div>
  );
}

export default MyButton;
```

#### CSS 변수 활용
CSS는 ``--``로 변수를 선언하고 ``val()``로 변수의 값을 사용할 수 있다. 이것을 styled-components에서도 활용할 수 있다.

```javascript
import styled from 'styled-components';

const StyButton = styled.button`
  --bg-color: ${props => props.primary ? 'blue' : 'gray'};
  --text-color: white;

  background-color: var(--bg-color);
  color: var(--text-color);
  padding: 10px;
  border: none;
  border-radius: 5px;
`;

function MyButton() {
  return (
    <div>
      <StyButton pri>Primary Button</StyButton>
      <StyButton>Secondary Button</StyButton>
    </div>
  );
}

export default MyButton;
```

#### JS 변수 활용
자바스크립트 변수(상수)를 사용하여 동적인 스타일을 처리할 수도 있다.

```javascript
import styled from 'styled-components';

const padding-size = '15px';  //변수에 패딩 크기를 저장

const StyButton = styled.button`
  background-color: blue;
  color: white;
  padding: ${padding-size};  //변수 활용 
  border: none;
  border-radius: 5px;
`;

function MyButton() {
  return (
    <div>
      <StyButton>Button</StyButton>
    </div>
  );
}

export default MyButton;
```

변수의 값을 불러올 때는 ``${}``를 사용한다.

### Polished
styled-components는 lighten(), darken() 같은 함수는 제공되지 않는다. 대신 ``polished`` 패키지를 함께 활용하면 같은 상황을 처리할 수 있다.

먼저 Polished 패키지를 설치해야 한다.

```
yarn add polished
```

lighten(), darken()


