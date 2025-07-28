# React Router
React는 SPA(Single Page Applicationi)이기 때문에, html을 변경하는 방식으로 페이지를 변경하지 않는다.

링크(메뉴)에 따라서 내부 컴포넌트를 변경하는 방식을 취한다. 이것을 리액트 라우팅이라고 한다.

- 필요 패키지 : react-router-dom
- 설치 : yarn add react-router-dom@6.26.1

react 19.9.0 버전에 맞는 react-router-dom 버전(6.26.1) 설치

## react router dom에서 제공하는 컴포넌트(또는 함수)
### BrowserRouter
html5의 history api를 사용하여 페이지를 새로고침 하지 않아도 주소를 변경하고, 현재 주소에 관련된 정보를 props로 쉽게 조회하거나 사용할 수 있게 해주는 컴포넌트.

라우팅과 관련된 컴포넌트는 BrowserRouter 하위에 위치해야 한다.

```jsx
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);
```
index.js에 App 컴포넌트를 감싼 형태로 작성하면 하위 페이지 이동을 쉽게 처리할 수 있다.

### Route
현재 경로에 따라 다른 컴포넌트를 보여주는 컴포넌트로 페이지 변경을 처리한다.

사용법>
```jsx
<Route path="uri" element={<보여줄컴포넌트 />} />
```

### Routes
Route를 하나로 묶어주는 컴포넌트(페이지 영역)로 이 컴포넌트 내에서 페이지가 변경되게 된다.

### Link
클릭하면 다른 주소로 이동시켜 주는 컴포넌트.(```<a>``` 태그는 사용할 수 없다!!)

렌더링을 하게 되면 Link 컴포넌트가 <a>로 변환된다.

사용법>
```jsx
<Link to="uri">이동메뉴</Link>
```

to는 Route 컴포넌트의 path와 연계되어 해당 컴포넌트로 화면을 변경시킨다.

```jsx
import { Link, Route, Routes } from "react-router-dom";
import "./App.css";
import Home from "./components/Home";
import About from "./components/About";

function App() {
  return (
    <div className="App">
      <div className="Nav">
        <ul>
          <li>
            <Link to="/">HOME</Link>
          </li>
          <li>
            <Link to="/about">ABOUT</Link>
          </li>
        </ul>
      </div>
      <hr />
      <div className="Content">
        <Routes>
          <Route path="/" element={<Home title="My HOME" />} />
          <Route path="/about" element={<About />} />
        </Routes>
      </div>
    </div>
  );
}

export default App;
```

### useNavigate()
조건이 필요한 곳에서 navigate 함수를 호출하여 경로를 이동시킬 때 사용하는 훅(hook)이다..

Link는 <a> 태그와 같은 동작을 수행하는 컴포넌트로 클릭 시 바로 이동을 시키지만, 페이지 전환 시 추가로 처리해야 하는 로직이 있을 경우, 또는 조건부 페이지 이동에서 useNavigate를 사용한다.

예를 들어, 사용자 로그인과 관리자 로그인으로 구분된 경우 로그인 아이디에 따라 전환되는 화면을 다르게할 때 사용하게 된다.

```jsx
const nav = useNavigate();
nav("uri"[, option]);
```

option
1. replace : 뒤로가기를 허용할지 여부를 설정<br>
        nav("uri", { replace:true }); 뒤로 가기를 허용하지 않음.
2. state : 일종의 쿼리스트링을 넘길 때 사용.<br>
        페이지 전환 시 데이터를 넘길 수 있음.

```jsx        
nav("uri", { state: object });
//object - 변수, 객체{data1: value1, data2: value2}
//쿼리스트링 : http://localhost/somepage?data1=v1&data2=v2
```

```jsx
  const nav = useNavigate();

  const clickHandle = () => {
    alert("로그인 성공");
    if (userId === "admin") {
      //관리자 로그인
      nav("/admin");
    } else {
      //일반 사용자 로그인
      nav("/user", {state: userId});
    }
  };
```

로그인을 성공할 경우 사용자의 id로 구분하여 전환될 페이지를 다르게 처리하며, 이 때 데이터를 보낼 수 있게 된다.
        
### useLocation()
```useLocation()```은 현재 uri의 정보를 저장하고 있는 훅(hook)으로 state 값을 꺼낼 때 사용한다. 

```useLocation```이 저장하는 주요 정보는 ```pahtname```과 ```state```이다.

```pathname```현재 보여지는 화면의 uri를 저장하고 있으며, ```state```는 ```useNavigate()```로 보낸 데이터를 저장하고 있다.

사용자 페이지에서의 예는 다음과 같다.
```jsx
const User = () => {
  const location = useLocation();  //useLocation 생성
  const st = location.state;       //state 가져오기
  
  return (
    <div>
      <h1>사용자 페이지</h1>
      <p>{st}님 환영합니다.</p>
      <p>일반 사용자가 보는 화면입니다.</p>
    </div>
  );
};
```

## 중첩 레이아웃
프로그램에서 메인 메뉴와 하위 메뉴로 나뉘는 것처럼 전체 사이트의 구조가 상위 페이지 내에서 하위 페이지들이 변경되는 상황을 처리하는 것을 중첩 레이아웃이라고 한다.

사이트 전체를 고려할 때 헤더나 풋터와 같이 모든 페이지에 동일한 내용이 출력되는 부분은 ```Routes``` 컴포넌트의 바깥쪽에 작성하면 해결된다. 

보통 헤더에 메인 메뉴에 해당하는 링크가 존재하고 각 페이지별 하위 메뉴의 링크가 있을 경우, 페이지별로 하위 메뉴의 링크를 작성하지 않고, 중첩 레이아웃으로 해결한다.

다음과 같은 구조를 가진 사이트가 있다고 가정한다.

```
root
  ├─ Main
  │   ├─ SubMain (사이트 첫페이지)
  │   ├─ Sub1
  │   └─ Sub2
  └─ Second
```

```Main```과 ```Second``` 페이지를 전환하는 메뉴는 ```Header``` 컴포넌트에 있으며, ```SubMain```과 ```Sub1```, ```Sub2``` 페이지를 전환하는 메뉴는 ```Main``` 컴포넌트에 작성한다.

App 컴포넌트는 다음과 같다.
```jsx
import "./App.css";
import Header from "./components/Header";
import Footer from "./components/Footer";
import { Route, Routes } from "react-router-dom";
import Main from "./components/Main";
import Sub1 from "./components/Sub1";
import Sub2 from "./components/Sub2";
import SubMain from "./components/SubMain";
import Second from "./components/Second";

function App() {
  return (
    <div className="App">
      <Header />
      <Routes>
        <Route element={<Main />}>
          <Route path="/" element={<SubMain />} />
          <Route path="/sub1" element={<Sub1 />} />
          <Route path="/sub2" element={<Sub2 />} />
        </Route>
        <Route path="/second" element={<Second />}/>
      </Routes>
      <Footer />
    </div>
  );
}

export default App;
```

```Main```의 하위 컴포넌트는 ```<Route element={<Main />}>```의 자식 컴포넌트로 작성한다.

### Outlet
> An ```<Outlet>``` should be used in parent route elements to render their child route elements. This allows nested UI to show up when child routes are rendered. If the parent route matched exactly, it will render a child index route or nothing if there is no index route.<br><br>
> ```<Outlet>```은 부모 경로 요소에서 자식 경로 요소를 렌더링하는 데 사용해야 합니다. 이렇게 하면 자식 경로가 렌더링될 때 중첩된 UI가 표시됩니다. 부모 경로가 정확히 일치하면 자식 인덱스 경로를 렌더링하거나 인덱스 경로가 없으면 아무것도 렌더링하지 않습니다.

```Outlet```은 부모 컴포넌트의 일부 화면에 자식 컴포넌트를 넣는데 사용하는 컴포넌트이다.

예제에서 ```Main```의 하위 요소가 되는 ```SubMain```과 ```Sub1```, ```Sub2```를 ```Main``` 컴포넌트의 화면 안에서 전환되도록 해준다.

```Main``` 코드는 다음과 같다.
```jsx
import React from "react";
import { Link, Outlet } from "react-router-dom";

const Main = () => {
  return (
    <div>
      <h1>Main</h1>
      <nav>
        <Link to="/">[submain]</Link>
        <Link to="/sub1">[sub1]</Link>
        <Link to="/sub2">[sub2]</Link>
      </nav>      
      <hr></hr>
      <Outlet/>
    </div>
  );
};

export default Main;
```

```<Outlet />```의 위치에 하위 컴포넌트의 화면이 나오게 된다.




