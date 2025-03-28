# Event Handling
HTML 이벤트와 인터페이스가 동일하기 때문에 사용법이 꽤 비슷하다.

## 이벤트를 사용할 때 주의 사항

1. 이벤트 이름은 카멜 표기법으로 작성한다.

onclick, onchange, onkeydown 등 이벤트 처리용 속성 -> onClick, onChange, onKeyDown 등으로 표기


2. 이벤트에 실행할 자바스크립트 함수를 호출하는 것이 아니라, 호출될 함수의 참조값을 전달하는 것이다.

HTML에서 이벤트를 설정할 때는 큰따옴표 안에 실행할 코드를 넣었지만, 리액트에서는 함수의 참조(reference)를 전달한다.

```javascript
onclick="func()" -> onClick={func}
```

일반 자바스크립트에서와 같이 HTML에 ```onClick={func()}``` 형식으로 작성하게 되면 ```func()```함수가 클릭이 발생한 시점에 호출되는 것이 아니라 렌더링되는 시점에 호출되어 클릭하지 않아도 실행되는 문제가 발생한다.


3. DOM 요소에만 이벤트를 설정할 수 있다.

즉 div, button, input, form, span 등의 DOM 요소에는 이벤트를 설정할 수 있지만, 우리가 직접 만든 컴포넌트에는 이벤트를 자체적으로 설정할 수 없다.

```javascript
<MyComponent onClick={handleClick}/>
```

예를 들어 MyComponent에 onClick 값을 설정한다면 MyComponent를 클릭할 때 handleClick 함수를 실행하는 것이 아니라, 그냥 이름이 onClick인 props를 MyComponent에게 전달해 줄 뿐이다.


## 인자가 없는 이벤트 함수 처리

```javascript
const func = function(){
  ...
}

return (
  <div>
    <button onClick={func}>클릭</button>
  </div>
)
```

위의 예제와 같이 인자가 없는 이벤트 함수를 호출할 때는 함수명(식별자)만을 사용한다.

## 인자가 있는 이벤트 함수 처리
이벤트가 발생했을 때 함수에 값을 전달하는 경우는 다음과 같이 처리해야 한다.

```javascript
const func = function(val){
  ...
}

return (
  <div>
    <button onClick={() => func("어떤값")}>클릭</button>
  </div>
)
```

위의 예제와 같이 화살표 함수를 사용하여 렌더링 시에는 함수가 호출되지 않도록 한다. 만일 ```onClick={func("어떤값")}``` 처럼 화살표 함수를 사용하여 작성하지 않으면 클릭과 상관없이 함수가 호출되어 정상적으로 동작하지 않는다.

## props로 부모의 이벤트 함수를 자식 컴포넌트에 전달
자식 컴포넌트는 props를 통해 전달받은 이벤트 함수를 실행할 수 있다. 예제는 다음과 같다.

```javascript
import React from 'react';
import ChildComp from './ChildComp';

const ParentComp = () => {
  // 이벤트 핸들러 함수 정의
  const handleClick = () => {
    alert('버튼이 눌렸다!');
  };

  return (
    <div>
      <h1>Parent Component</h1>
      {/* 자식 컴포넌트에 이벤트 함수를 props로 전달 */}
      <ChildComp onBtnClick={handleClick} />
    </div>
  );
}

export default ParentComp;
```

```javascript
import React from 'react';

// 화살표 함수로 자식 컴포넌트 정의
const ChildComp = ({ onBtnClick }) => {
  return (
    <div>
      <h2>Child Component</h2>
      {/* props로 전달받은 클릭 함수를 버튼의 onClick에 설정 */}
      <button onClick={onBtnClick}>Click me</button>
      {/* 이 onClick은 DOM의 이벤트 처리 속성이다. */}
    </div>
  );
};

export default ChildComp;
```

이벤트의 발생은 자식 컴포넌트(ChildComp)지만 이벤트를 통한 데이터의 활용이나 모양의 변화는 부모쪽에서 발생해야 하는 경우에 이 방법을 활용한다.

자식 컴포넌트에서 실행하는 클릭 이벤트 처리용 ```onBtnClick```은 부모 컴포넌트의 ```handleClick```이 된다.

자식 컴포넌트들이 발생시키는 메시지의 내용은 다르지만, 동일한 기능이 처리되어야 하는 경우에 활용한다.

```javascript
import React from 'react';
import ChildComp1 from './ChildComp1';
import ChildComp2 from './ChildComp2';

const ParentComp = () => {
  // 이벤트 핸들러 함수 정의
  const handleClick = (msg) => {
    alert(msg);
  };

  return (
    <div>
      <h1>Parent Component</h1>
      {/* 자식 컴포넌트에 이벤트 함수를 props로 전달 */}
      <ChildComp1 onBtnClick={handleClick} />
      <ChildComp2 onBtnClick={handleClick} />
    </div>
  );
}

export default ParentComp;
```

```javascript
import React from 'react';

// 화살표 함수로 자식 컴포넌트 정의
const ChildComp1 = ({ onBtnClick }) => {
  return (
    <div>
      <h2>Child Component1</h2>
      {/* props로 전달받은 클릭 함수를 버튼의 onClick에 설정 */}
      <button onClick={() => onBtnClick("1이다.")}>Click me</button>
      {/* 이 onClick은 DOM의 이벤트 처리 속성이다. */}
    </div>
  );
};

export default ChildComp1;
```


```javascript
import React from 'react';

// 화살표 함수로 자식 컴포넌트 정의
const ChildComp2 = ({ onBtnClick }) => {
  return (
    <div>
      <h2>Child Component2</h2>
      {/* props로 전달받은 클릭 함수를 버튼의 onClick에 설정 */}
      <button onClick={() => onBtnClick("2다.")}>Click me</button>
      {/* 이 onClick은 DOM의 이벤트 처리 속성이다. */}
    </div>
  );
};

export default ChildComp2;
```

두 자식 컴포넌트는 서로 다른 메시지를 부모 컴포넌트로 전달할 수 있게 된다. 즉 부모 컴포넌트의 한 이벤트 처리 함수로 두 자식 컴포넌트의 메시지를 출력할 수 있게 된다.

## ``input`` 태그의 입력 이벤트 처리
input 태그를 통해 사용자의 입력값을 받기 위해서는 onchange 이벤트를 사용해야 하며 이 때 입력값을 받아서 저장하기 위한 state를 사용해야 한다.

### state(상태값)
state는 컴포넌트에서 변화된 내용을 유지 관리하기 위해 사용하는 일종의 변수이다. 

JSX는 HTML 코드를 사용하고 있지만, 이것은 HTML 코드의 형태를 빌어온 것이지 실제 HTML은 아니다.(JSX는 babel이라는 컴파일러가 JS로 변환하여 처리해준다.)

```JSX의 HTML``` -> ```JS 코드``` -> ```HTML```의 변환 단계를 거친다.

예를 들어 HTML의 input 태그는 사용자가 입력하는 값을 value에 저장하면 동시 화면에 한 글자씩 출력해 주는 기능(에코)을 제공한다. JSX에 작성된 input 태그는 실제 HTML이 아니기 때문에 저장공간 및 에코 출력을 위한 기능이 작성되어야 한다.

즉, 빈 공간이었던 input 태그에 사용자의 입력이 발생(이벤트 발생)한다는 것은 컴포넌트가 변화된다는 것을 의미하는 것이며, 이 변화된 내용을 위한 저장 공간 및 에코 출력 기능을 제공하기 위해 state를 활용한다.

## useState
useState는 React Hooks에 포함된 상태 처리 기능을 제공하는 객체이다.
- React Hooks는 클래스형 컴포넌트에서 제공하는 기능을 함수형 컴포넌트에서도 활용할 수 있도록 제공되는 라이브러리

useState는 상태값을 저장하는 변수와 변수의 값을 변경하는 함수로 구성되어 있으며, 상태값을 바로 변경할 수 없다는 제약을 갖는다.

state가 변경되면 react는 해당 컴포넌트를 다시 렌더링하여 처리해야 하는데 상태값이 바로 변경될 경우 이를 감지할 수 없게 된다. 그래서 상태값을 반드시 변경 함수를 활용하여 처리하도록 하고 있다. 

useState를 생성하는 문법은 다음과 같다.

```javascript
const [useValue, setUseValue] = useState("초기값");
```

이 문법을 자바 코드로 작성한다면 다음과 같다.(예는 예일 뿐)

```java
private String useValue;

public void setUseValue(useValue){
    this.useValue = useValue;
}
```

- useState 객체에게 '초기값'을 갖는 `useValue`라는 변수를 생성하고, `setUseValue`라는 setter 함수를 만들어라라고 명령하는 문장이다.
- `useValue`에 저장된 값을 사용할 때는 일반 변수처럼 사용한다.

입력값을 출력하는 예
```jsx
import { useState } from "react";

function App() {
  const [text, setText] = useState("");

  const handleChange = (event) => {
    setText(event.target.value);
  };

  return (
    <div>
      <input type="text" value={text} onChange={handleChange} />
      <p>입력값: {text}</p>
    </div>
  );
}

export default App;
```

## 다중 입력 처리
Event 객체를 파라미터로 받을 경우 하나의 이벤트 처리 함수로 여러개의 입력값을 함께 처리 할 수 있다. 

### Event 객체
브라우저에서 발생하는 이벤트(클릭, 키 입력 등)에 대한 정보를 담고 있는 객체이다.

주요 속성은 다음과 같다.
- target : 이벤트가 발생한 html요소를 나타낸다.
- type : 이벤트의 종류(click, keydown 등)를 나타낸다.
- key : 키 입력 이벤트 발생 시 입력된 키 값을 저장한다.

event.target으로 어떤 html 요소에서 이벤트가 발생했는지를 파악할 수 있게 되며, 해당 요소의 value와 같은 html 속성값을 가져올 수 있다.

### 다중 입력 처리를 위한 useState
여러 값을 함께 저장할 수 있는 객체 형식으로 useState를 작성한다.

로그인 폼을 위한 useState

```jsx
  const [form, setForm] = useState({
    userId: "",
    userPwd: "",
  });
```

```userId```나 ```userPwd```를 출력할 때는 다음과 같이 사용한다.
```jsx
  <input type="text" value={form.userId}>
```

각 state 앞에 ```form.```을 붙이고 사용하면 되지만, 입력의 개수가 많아지면 불편하게 될 수도 있으니 다음과 같이 구조 분해 할당하여 사용하자.

```jsx
const {userId, userPwd} = form;
```

이 후부터는 ```form.```을 붙이지 않고 ```userId```나 ```userPwd```로 작성하면 된다.

### 이벤트 처리 함수
이벤트 객체를 파라미터로 받아서 처리





