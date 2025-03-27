# React 시작
## 개발 환경
* Node.js (https://nodejs.org/ko) - 권장 버전 설치
* VSCode (https://code.visualstudio.com/)
* Yarn (https://classic.yarnpkg.com/en/docs/install#windows-stable) - npm 대신 사용(안해도 됨)
> yarn을 기준으로 작성

yarn 설치
```
npm install --g yarn
```
> Yarn 사이트의 install 참조

## 프로젝트 생성
VSCode에 작업용 폴더를 열고 Terminal에 다음과 같이 입력한다.
```
yarn create react-app project_name
```

'project_name'으로 폴더가 생성되면서 React에 필요한 라이브러리를 설치하고 프로젝트 관련 파일을 생성한다.

## 프로젝트 실행
Terminal에서 프로젝트 폴더로 이동한 후 실행한다.
```
cd project_name
yarn start
```

![image](https://github.com/tiblo/React_edu/assets/34559256/1515e326-2eaf-4037-a839-89faede62f8e)


## 프로젝트 종료
Terminal에서 'ctrl + c'를 눌러 종료한다.

## 프로젝트 백업 및 복구
node_modules 폴더에는 리액트 프로젝트에 필요한 라이브러리들이 저장되어 많은 용량을 차지한다.

이 폴더를 제거하고 프로젝트 파일만 백업(또는 git 연동)을 수행하는 것이 좋다.

복구 시에는 프로젝트 폴더에서 다음의 명령어로 node_modules을 다시 다운받아서 사용할 수 있다.
```
yarn install
```

package.json 파일에 내용을 기반으로 node_modules을 다시 다운로드하기 때문에 package.json은 반드시 함께 백업해야 한다.

## Port 번호 변경
React는 기본적으로 3000번 port 번호를 사용한다. Port 번호를 변경할 때는 ``package.json`` 파일에서 ``scripts``의 ``start`` 부분을 다음과 같이 수정해야 한다.

```
"scripts": {
    "start": "set PORT=변경할번호 && react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  },
```
``변경할번호`` 부분에 원하는 Port 번호를 입력하면 된다.



