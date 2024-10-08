# Event Handling
HTML 이벤트와 인터페이스가 동일하기 때문에 사용법이 꽤 비슷하다.

## 이벤트를 사용할 때 주의 사항

1. 이벤트 이름은 카멜 표기법으로 작성한다.

onclick, onchange, onkeydown 등 이벤트 처리용 속성 -> onClick, onChange, onKeyDown 등으로 표기

2. 이벤트에 실행할 자바스크립트 코드를 전달하는 것이 아니라, 함수 형태의 값을 전달한다.

HTML에서 이벤트를 설정할 때는 큰따옴표 안에 실행할 코드를 넣었지만, 리액트에서는 함수 형태의 객체를 전달한다.

```javascript
onclick="func()" -> onClick={func}
```

3. DOM 요소에만 이벤트를 설정할 수 있다.

즉 div, button, input, form, span 등의 DOM 요소에는 이벤트를 설정할 수 있지만, 우리가 직접 만든 컴포넌트에는 이벤트를 자체적으로 설정할 수 없다.

```javascript
<MyComponent onClick={handleClick}/>
```

예를 들어 MyComponent에 onClick 값을 설정한다면 MyComponent를 클릭할 때 handleClick 함수를 실행하는 것이 아니라, 그냥 이름이 onClick인 props를 MyComponent에게 전달해 줄 뿐이다.

## 인자가 없는 이벤트 함수 처리

## 인자가 있는 이벤트 함수 처리

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

## ``input`` 태그의 입력 이벤트 처리

