# Component Loop
한 화면에 동일한 요소가 여러 개 쓰이는 경우 각각의 요소를 컴포넌트로 만들지 않고 하나의 컴포넌트를 반복적으로 활용하는 것이 좋다. 

목록의 항목을 출력하거나 입력 요소가 여러개인 경우 등이 이에 해당된다.

자바스크립트 배열 객체의 내장 함수인 map을 사용하면 컴포넌트를 반복적으로 렌더링 할 수 있다.

## map 함수
map 함수는 파라미터로 전달된 함수를 사용하여 배열 내 각 요소를 처리하고 그 결과값으로 새로운 배열을 생성한다.

```javascript
array.map(function, [thisArg])
````

- function : callback 함수로 배열의 각 요소를 처리하기 위한 코드를 작성한다. 이 함수는 세가지 파라미터를 가질 수 있다.
  - currentValue : 현재 순번에 처리해야 하는 요소
  - index : 현재 처리해야하는 요소의 순번
  - array : 현재 처리하고 있는 원본 배열(특별한 경우 외에는 사용하지 않는다.)
- thisArg : 선택 옵션으로 callback을 사용할 때 this로 사용되는 값.

```js
const obj = { multiplier: 2 };

const numbers = [1, 2, 3];

const doubled = numbers.map(function (num) {
  return num * this.multiplier; // this를 obj로 설정
}, obj);

console.log(doubled); // [2, 4, 6]
```
