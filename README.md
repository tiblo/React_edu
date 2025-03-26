# React
메타(메타 플랫폼, 페이스북)에서 개발한 오픈 소스 자바스크립트 라이브러리.

SPA(Single Page Application)를 전제로 하는 라이브러리.

기본적으로 모듈형 개발이기 때문에 생산성 또한 상당히 높은 라이브러리라서 현재 대세..(?)

전체 페이지를 분할하여 조합하는 방식. 분할된 조각을 컴포넌트(Component)라고 함.

일반적인 Web 개발에서 사용하는 패턴인 MVC에서 View만을 처리하는 라이브러리.

DB 연동 등을 처리하기 위해서는 Controller 역할을 담당하는 서버가 필요하다.(Spring, Express 등)

## React 동작 구조(원리)
### Rendering
브라우저는 html 코드를 다운로드하면 DOM(Document Object Model)을 생성하고 이를 화면에 출력한다. 이 작업을 Rendering이라고 한다.

Javascript로 element를 제어하는 것은 실제로는 이 DOM을 제어하여 화면에 다시 Rendering되는 것을 의미한다.

브라우저는 javascript에 의해 DOM이 변경되면 해당 Element의 변경 사항을 화면에 출력하기 위해 Reflow와 Repaint를 수행하게 된다.

### Virtual DOM
React는 DOM을 바로 제어하지 않고 Virtual DOM을 생성하여 변경 사항을 처리한다.

변경 사항 처리를 위해 브라우저는 CSS를 다시 연산하고, 레이아웃을 구성하고(Reflow), 페이지를 다시 칠(Repaint)하게 되는데 시간이 많이 소요된다.

React는 DOM에 바로 변경 사항을 처리하지 않고 복제본인 Virtual DOM에 먼저 반영하여 기존 DOM과 비교를 통해 변경할 부분을 최소화함으로써 소요 시간을 줄인다.

![image](https://github.com/tiblo/React_edu/assets/34559256/2cf6fb96-0084-4b76-a1d3-6aa434c9e541)
[이미지출처 : React-동작-원리](https://velog.io/@leitmotif/React-%EB%8F%99%EC%9E%91-%EC%9B%90%EB%A6%AC)

## 개발환경 설정
### Node.js 설치
https://nodejs.org/ko

### Yarn 설치
node 설치 후 VSCode 터미널에서 npm으로 설치
```
npm install -g yarn
```

### 설치 확인
node 확인
```
node -v
```

yarn 확인
```
yarn -v
```

## React Components Styling
React Components Styling 방식
* CSS(기존 방식)
* SCSS
* CSS Module
* Styled-Components
* React Bootstrap

# VScode에서 React 디버깅

https://velog.io/@chori/React-%EA%B0%9C%EB%B0%9C%EC%A4%91-vsCode-%EB%94%94%EB%B2%84%EA%B9%85-%EB%B0%A9%EB%B2%95

디버그 아이콘 클릭 > create a launch.json file 클릭
> .vscode 폴더와 launch.json 파일이 생성됨<br>
  다음과 같이 입력
```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "chrome",
            "request": "launch",
            "name": "Launch Chrome against localhost",
            "url": "http://localhost:3000",
            "webRoot": "${workspaceFolder}"
        }
    ]
}
```
터미널에서 먼저 npm start로 서버를 구동해야 함.

# VSCode Extentions
* Auto Rename Tag
* Auto Close Tag
* Reactjs code snippets
  * rsc(React Stateless Component)로 함수형 컴포넌트 자동 생성
* vscode-styled-components
  * Styled component 안에서 css property 자동 완성 기능 제공
* styled-components-snippets
  * ``imsc`` : 	``import styled from 'styled-components';``
  * ``sc`` : ``const ${1} = styled.${2}``
  * ``scp`` : ``${props => props.${1}};``

# React 프로젝트 복사 및 이동 후
node_modules의 용량이 많기 때문에 제외하고 압축하여 옮기게 된다.

새로운 환경에서 다시 프로젝트를 실행할 경우 다음과 같이 node_modules을 설치해야 한다.
```
> npm install
또는
> yarn install
```
package.json의 내용을 확인하여 필요한 node_modules을 설치한다.

# 터미널에 글자가 깨지는 경우 해결법
![image](https://github.com/tiblo/React_edu/assets/34559256/b0da1558-e0ee-48b0-9c72-cf364cc963e1)

setting.json에 다음을 추가
```
{
    ...
    "[powershell]": {
        "files.encoding": "utf8bom",
        "files.autoGuessEncoding": true
    }
}
```

안되면(안된다..) 다음 코드를 터미널에서 실행
```
chcp 65001
```

- chcp : CHange Code Page. cmd(커멘드 창)에서의 글자 코드를 변경하는 명령어.
- 65001 : utf-8 문자셋의 코드번호.

> 이렇게 해도 다시 문자가 깨질 수도 있는데, 위의 코드를 다시 실행하거나 최종적으로는 registry를 편집해야 함.

![image](https://github.com/tiblo/React_edu/assets/34559256/70bcf883-99e9-4850-bb55-acb5943073fd)

해결~

## settings.json 여는 방법
![image](https://github.com/tiblo/React_edu/assets/34559256/8560465f-08b3-4e21-bd32-dd3a553dca2e)

``F1`` 누르고 위와 같이 타이핑하여 실행

