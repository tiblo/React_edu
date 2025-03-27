# Component Loop
한 화면에 동일한 요소가 여러 개 쓰이는 경우 각각의 요소를 컴포넌트로 만들지 않고 하나의 컴포넌트를 반복적으로 활용하는 것이 좋다. 

목록의 항목을 출력하거나 입력 요소가 여러개인 경우 등이 이에 해당된다.

자바스크립트 배열 객체의 내장 함수인 map을 사용하면 컴포넌트를 반복적으로 렌더링 할 수 있다.

## map 함수
map 함수는 파라미터로 전달된 함수를 사용하여 배열 내 각 요소를 처리하고 그 결과값으로 새로운 배열을 생성한다.

```javascript
array.map(function, [thisArg])
````

- function : callback 함수로 배열의 각 원소를 처리하기 위한 코드를 작성한다. 이 함수는 세가지 파라미터를 가질 수 있다.
  - currentValue : 현재 순번에 처리해야 하는 원소
  - index : 현재 처리해야하는 원소의 순번
  - array : 현재 처리하고 있는 원본 배열(특별한 경우 외에는 사용하지 않는다.)
- thisArg : 선택 옵션으로 callback을 사용할 때 this로 사용되는 값.

```js
const obj = { mul: 2 };

const numbers = [1, 2, 3];

const doubled = numbers.map(function (num) {
  return num * this.mul; // this를 obj로 설정
}, obj);

console.log(doubled); // [2, 4, 6]
```

위 예제는 1, 2, 3의 세 원소를 갖는 배열에서 하나씩 값을 꺼내와 ```* 2``` 연산을 수행하여 2, 4, 6을 원소로 하는 ```doubled```라는 새로운 배열을 생성한 것이다.

이 때 thisArg는 obj가 되며, this.mul은 obj의 mul을 나타낸다. 즉 ```return num * 2;```가 되어 실행된다.(일반적인 경우 thisArg는 사용하지 않는다.)

위 예제의 함수는 화살표 함수로 작성할 경우 다음과 같이 간단하게 작성할 수 있다.

```js
const doubled = numbers.map(num => num * this.mul, obj);
```

## HTML 요소 반복 생성
다음은 비순서 목록 ```<ul>```에 ```<li>```을 추가하는 예제이다.
```jsx
import React from "react";

const MyList = () => {
  const menus = ["아메리카노", "카페라떼", "카페모카", "카푸치노", "딸기라떼"];
  const menuList = menus.map((menu, index) => <li key={index}>{menu}</li>);
  console.log(menuList);
  return <ul>{menuList}</ul>;
};

export default MyList;
```

반복적으로 생성된 항목을 구별하기 위해 key를 사용한다.

key를 사용하지 않을 경우 warning이 발생되지만 실행에 문제는 없다.

이 key는 컴포넌트 배열을 렌더링 했을 때 변동된 요소를 찾아서 관리하기 위한 값으로 react 내부적으로 사용하며, 렌더링된 후의 HTML에서는 보이지 않는다.

데이터 배열의 값으로 컴포넌트를 반복적으로 생성하는 경우 index를 간단히 사용한다.(하지만, react에서 배열의 index 사용을 권장하지는 않는다. 왜냐면 배열의 원소가 추가/삭제되면 원래 있던 원소의 index가 변화되기 때문.)









