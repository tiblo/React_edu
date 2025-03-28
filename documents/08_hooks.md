# Hooks
Hooks는 클래스형 컴포넌트에서 제공되는 가능을 함수형 컴포넌트에서도 활용할 수 있도록 제공되는 라이브러리이다.

여기에서는 다음의 hook들에 대해서 다룬다.
- useState
- useEffect
- useReducer
- useMemo
- useCallback
- useRef

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




