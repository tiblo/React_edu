# key를 사용하는 이유
동일한 코드로 동적 생성된 요소의 안정적인 고유성을 부여하기 위해 권장하는 속성값.

html로 변환되었을 때 표시되지 않지만, react 내부적으로 요소를 명확하기 구분하는데 활용.

없어도 작동이 잘 되지만, 문제가 발생할 수도 있다.(경고로 처리)

# React strict 모드
애플리케이션 내의 잠재적인 문제를 알아내기 위한 모드. (2회 반복하는 결과를 확인할 수 있음)

개발 중일 때 사용하는 모드로 렌더링을 두번 진행하는 것은 아니다.

react는 렌더링 단계(변경사항 탐지)와 커밋 단계(실제 변경사항 반영)로 나눠서 진행하는데

두 단계가 동시에 진행되지 않는다(커밋 단계는 빠르고 렌더링 단계는 느림).

자식 컴포넌트를 두번 실행하여 시차에 따른 값의 오류 등을 파악할 수 있게 도와주는 모드.

# CORS
Cross Origin Resource Sharing. 2개 이상의 서버에 하나의 사이트가 운영되는 경우

CDN 방식으로 라이브러리를 불러오거나, 파일서버와 웹서버를 따로 운영하는 경우, 또는 2개 회사가 하나의 사이트를 공동으로 제공하는 경우 등

한 서버의 허용된 권한을 악용하여 다른 서버를 공격하는 방식으로 악용될 수 있어서 대부분의 브라우저에서 제한됨.

이를 해제하여야 정상적으로 서비스 제공이 가능하기 때문에 보안 이슈가 발생되는 상황이 아닌 부분에서는 cors를 허용하도록 코드를 작성.

# CSRF
Cross-Site Request Forgery

한 서버에서 운영되는 형태. 허용된 권한을 중간에 가로채서 위조된 내용을 전송하거나 서버를 공격하는 방식. 

<img src="https://github.com/tiblo/React_edu/assets/34559256/fced97c3-4f88-4328-9e3a-2e15a148bbfb" width=600>

보안 토큰을 주고받아서 예방하는 방식으로 해결.

<img src="https://github.com/tiblo/React_edu/assets/34559256/a32e4fa0-da1a-40d2-b70b-91323db7c25b" width=800>
