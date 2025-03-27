# React Router
React는 SPA(Single Page Applicationi)이기 때문에,
    html을 변경하는 방식으로 페이지를 변경하지 않는다.

    링크(메뉴)에 따라서 내부 컴포넌트를 변경하는 방식을 취한다.
    이것을 리액트 라우팅이라고 한다.

    필요 패키지 : react-router-dom
    설치 : yarn add react-router-dom

    react router dom에서 제공하는 컴포넌트(또는 함수)
    1) BrowserRouter
        html5의 history api를 사용하여 페이지를 새로고침 하지 않아도
        주소를 변경하고, 현재 주소에 관련된 정보를 props로 쉽게 조회하거나
        사용할 수 있게 해주는 컴포넌트.
        라우팅과 관련된 컴포넌트는 BrowserRouter 하위에 위치해야 한다.

    2) Route
        현재 경로에 따라 다른 컴포넌트를 보여주는 컴포넌트
        사용법>
        <Route path="uri" element={<보여줄컴포넌트 />} />
    3) Routes
        Route를 하나로 묶어주는 컴포넌트(페이지 영역)
    4) Link
        클릭하면 다른 주소로 이동시켜 주는 컴포넌트
        (<a> 태그는 사용할 수 없다!!)
        Link 컴포넌트가 <a>로 변환됨.
        사용법>
        <Link to="uri">이동메뉴</Link>
        to는 Route 컴포넌트의 path와 연계되어 해당 컴포넌트로 이동시킴.
    5) useNavigate()
        조건이 필요한 곳에서 navigate 함수를 호출하여 경로를 이동.
        Link는 <a> 태그와 같은 동작을 수행하는 컴포넌트로 클릭 시 
        바로 이동을 시키지만, 페이지 전환 시 추가로 처리해야 하는 로직이
        있을 경우, 또는 조건부 페이지 이동에서 useNavigate를 사용.
        예를 들어, 사용자 로그인과 관리자 로그인으로 구분된 경우
        로그인 아이디에 따라 전환되는 화면을 다르게할 때 사용.

        const nav = useNavigate();
        nav("uri"[, option]);

        option
        (1) replace : 뒤로가기를 허용할지 여부를 설정
            nav("uri", { replace:true }); 뒤로 가기를 허용하지 않음.
            뒤로가기를 허용하지 않는 경우에만 사용.
        (2) state : 일종의 쿼리스트링을 넘길 때 사용.
            페이지 전환 시 데이터를 넘길 수 있음.
            nav("uri", { state: object });
            object - 변수, 객체{data1: value1, data2: value2}

            쿼리스트링 : http://localhost/somepage?data1=v1&data2=v2
            
        useLocation() : 위 state 값을 꺼낼 때 사용하는 훅(hook).
            지정해서 꺼내는 방식이 아니라 다 꺼내는 방식.
