# Hooks
Hooks는 클래스형 컴포넌트에서 제공되는 가능을 함수형 컴포넌트에서도 활용할 수 있도록 제공되는 라이브러리이다.

일반적으로 hook은 컴포넌트 함수의 시작 위치에 작성해야 한다.

## useState
컴포넌트의 가변적인 상태(데이터, 속성)값 처리하는 훅이다. 이전 이벤트 핸들링에서 다뤘으므로 [참조](https://github.com/tiblo/React_edu/blob/main/documents/04_event_handling.md#usestate).

## useEffect
컴포넌트가 렌더링될 때마다 특정 작업을 수행하도록 설정하기 위한 훅이다. 또 불필요한 렌더링을 막는데도 사용된다.

주요 특징
- 컴포넌트가 마운트될 때 실행
- 컴포넌트가 업데이트될 때 실행
- 컴포넌트가 언마운트될 때 실행. 이 경우 타이머 등을 제거하는 cleanup 처리에 활용.

### 기본 문법
```jsx
  useEffect(() => {...}, [의존성 배열]);
```

의존성 배열에는 컴포넌트에서 사용하는 state들을 작성하는데 이 state가 변할 때만 useEffect 안에 작성한 함수(```() => {...} 부분```)이 실행된다. 이 부분은 의존성 배열에 작성되지 않은 state의 변경 시에는 실행되지 않는다.

```jsx
useEffect(() => {
  console.log(`count 값이 변경됨: ${count}`);
}, [count]);
```

```jsx
  useEffect(() => {...}, []);
```

의존성 배열을 비워 놓으면 컴포넌트가 처음 화면에 출력될 때만 함수부분이 실행되고 업데이트 시에는 실행되지 않는다.

### Cleanup
```return```을 사용하면 언마운트 시에 처리할 내용을 작성할 수 있다.

```jsx
useEffect(() => {
  const timer = setInterval(() => {
    console.log("1초마다 실행됨!");
  }, 1000);

  return () => {
    clearInterval(timer); //컴포넌트가 사라질 때 실행됨
    console.log("타이머 삭제!");
  };
}, []);
```

위와 같이 작성한 경우 화면이 변경될 때 interval을 제거할 수 있다.


## useReducer
useState와 비슷한 hook으로 컴포넌트의 상황에 따라 다양한 상태를 다른 값으로 업데이트할 때 사용한다.

### 기본 문법
```jsx
const [state, dispatch] = useReducer(reducer, initState);
```

- state : 현재 상태값이자 업데이트 시 사용할 값을 저장한 객체(변수)
- dispatch : action을 발생시키는 함수
- reducer : action에 따라 state를 변경시키는 함수
  - function reducer(state, action) {...} 형식으로 작성.
- initState : state의 초기값.

useReducer를 사용한 카운터 예
```jsx
import React, { useReducer } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "INC":
      return { value: state.value + 1 };
    case "DEC":
      return { value: state.value - 1 };
    default: //아무것도 해당되지 않을 때 기존 상태를 반환
      return state;
  }
}

const MyReducer = () => {
  const [state, dispatch] = useReducer(reducer, { value: 0 });
  return (
    <div>
      <p>
        현재 카운터값은 <b>{state.value}</b>
      </p>
      <button onClick={() => dispatch({ type: "INC" })}>+</button>
      <button onClick={() => dispatch({ type: "DEC" })}>-</button>
    </div>
  );
};

export default MyReducer;
```

예제처럼 하나의 state에 두가지 동작(기능)에 따른 변화를 줄 수 있다. 단점은 reducer 함수의 설계 등 부가적으로 고려할 것이 있다는 점이다.

## useMemo
함수형 컴포넌트 내부에서 발생하는 연산을 최적화하기 위해 사용하는 라이브러리이다.

연산이 필요없는 상황에서도 렌더링할 때마다 재 연산되는 것을 막는 용도로 사용한다.(별도로 작성한 함수의 호출을 제어하는 용도로 사용)

### 기본 문법
```jsx
const variableName = useMemo(Callback, [의존성 배열]);
```

- Callback : 산술 처리 함수를 호출하는 Callback 함수.
- 의존성 배열 : 변경이 발생할 수 있는 state 목록. 이 state들의 변경 시에만 Callback 함수를 실행.

다음은 입력한 값의 평균을 계산하여 출력하는 예제이다.

```jsx
import React, { useState, useMemo, useCallback } from "react";

//평균 계산용 함수
const getAvg = (numbers) => {
  console.log("평균 계산 중...");
  if (numbers.length === 0) {
    return 0;
  }

  const sum = numbers.reduce((a, b) => a + b); //총합 구함
  const avg = sum / numbers.length; //평균

  return avg;
};

const MyMemo = () => {
  const [number, setNumber] = useState(""); //입력 숫자 저장
  const [list, setList] = useState([]); //숫자 배열 저장

  //입력한 숫자를 처리(number에 저장)하는 함수
  const onch = useCallback((e) => {
    setNumber(e.target.value);
  }, []);

  //숫자문자열을 숫자 배열로 변환
  const onck = useCallback(() => {
    const pNum = parseInt(number);
    if (!isNaN(pNum)) {
      const nextList = list.concat(pNum);
      setList(nextList);
      setNumber("");
    }
  }, [number, list]);

  const avg = useMemo(() => getAvg(list), [list]);

  return (
    <div>
      <input type="number" value={number} onChange={onch} />
      <button onClick={onck}>등록</button>
      <ul>
        {list.map((value, index) => (
          <li key={index}>{value}</li>
        ))}
      </ul>
      <div>
        <b>평균값 : </b>
        {avg}
      </div>
    </div>
  );
};

export default MyMemo;
```

```array.reduce(function(a, b))```는 배열을 값들을 하나의 값으로 축소할 때 사용하는 자바스크립트 함수이다.
- a : function의 반환값을 저장하는 변수
- b : 배열의 해당 값

배열의 첫번째 값부터 꺼내와서 b에 저장하고 함수의 연산을 수행한 다음 a에 저장한다. 배열의 값을 누적할 때 주로 사용된다.

새로운 값을 입력하고 등록 버튼을 클릭하면 list에 추가되어 평균을 다시 계산하게 된다. 

렌더링이 발생하는 경우는 두가지로 입력값을 넣을 때와 목록에 값이 추가될 때이다. ```useMemo```를 사용하면 입력값을 넣을 때 발생한 렌더링에서는 평균을 구하지 않고, 목록에 값이 추가될 때만 평균을 다시 계산하도록 최적화할 수 있다.


## useCallback
useMemo와 비슷한 훅으로 렌더링 성능 최적화를 목적으로 한다. 리렌더링 시 동일한 함수가 다시 생성되는 것을 막기 위해 사용 한다.

### 기본 문법
```jsx
const funcName = useCallback(() => {...}, [의존성 배열]);
```
- 의존성 배열의 state들에 변화가 발생할 때만 함수를 다시 생성한다.

함수 내에서 state 값을 활용하지 않을 경우 최소 한 번만 수행하도록 의존성 배열을 비워둠으로써 렌더링 성능을 최적화 하게된다.

하지만, state 값을 활용하는 경우에는 state 변화에 따라 다시 생성되도록 의존성 배열을 작성해야 한다.

위의 useMemo 예제에 useCallback이 포함되어 있다.

```jsx
  //입력한 숫자를 처리(number에 저장)하는 함수
  const onch = useCallback((e) => {
    setNumber(e.target.value);
  }, []);
  //컴포넌트가 최초로 렌더링된 시점에 한번만 생성되면 되기 때문에 []로 설정.

  //숫자문자열을 숫자 배열로 변환
  const onck = useCallback(() => {
    const pNum = parseInt(number);
    if (!isNaN(pNum)) {
      const nextList = list.concat(pNum);
      setList(nextList);
      setNumber("");
    }
  }, [number, list]);
  //onck는 number나 list가 변경될 때 새로 생성되서,
  //변경된 number나 list를 처리해야 하기 때문에
  //[number, list]를 넣어줌.
```

## useRef
Ref(Reference)는 리액트 코드를 통해 생성된 컴포넌트에 접근하는(컴포넌트를 식별하는) 방법을 제공한다.

동적으로 자동 생성되는 컴포넌트에 ref 값을 설정하여 제어 시 사용할 수 있다.

```jsx
import React, { useRef } from "react";

const MyRef = () => {
  const inRef = useRef(null);

  const handleFocus = () => {
    inRef.current.disabled = false; //input 활성화.
    inRef.current.focus(); //input에 포커스를 줌.
  }; //inRef.current는 ref가 설정된 요소(즉, input 태그)

  const handleReset = () => {
    inRef.current.disabled = true;
    inRef.current.value = "";
  };

  return (
    <div>
      <input disabled type="text" ref={inRef} />
      <button onClick={handleFocus}>활성화</button>
      <button onClick={handleReset}>초기화</button>
    </div>
  );
};

export default MyRef;
```

버튼을 통해 input 태그를 제어하기 위한 예제 코드이다. input 태그에 useRef를 사용함으로써 다른 컴포넌트인 버튼의 이벤트를 통해 제어할 수 있게 된다.
