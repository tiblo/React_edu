# 프로젝트 생성

## Vite로 React 프로젝트 생성
```
> yarn create vite project_name
```

- ```Select a framework:```는 ```React``` 선택
- ```Select a variant:```는 ```TypeScript``` 선택
- ```Use rolldown-vite (Experimental)?:```는 ```No``` 선택
- ```Install with yarn and start now?```는 ```Yes``` 선택

```rolldown-vite``` vite 팀에서 개발중인 새로운 실험용 번들러로 아직까지는 테스트 중이라 사용하지 않는다.

> 번들러란? React나 TypeScript 프로젝트를 개발할 때, 코드는 보통 여러 파일(.tsx, .ts, .css 등)로 나뉘어 있어요.
브라우저는 모듈화된 파일을 그대로 이해하지 못할 수도 있기 때문에, 배포용으로 한두 개의 파일로 합치고 최적화해야 합니다.
이 역할을 하는 도구가 바로 **번들러(Bundler)**입니다.(by. chatgpt)

```Install with yarn and start now?```를 ```Yes```로 선택하면 필요한 패키지를 자동으로 설치하면서 바로 실행하게 된다.

## ESLint와 Prettier 설정

먼저 서버를 중단(```ctrl + c```)하고 프로젝트 폴더로 이동(```> cd project_name```)한 다음 진행한다.

- ESLint는 코딩 규칙/버그 방지 도구
- Prettier는 코드 포맷팅 도구

Prettier를 사용하는 주된 이유는 코드 스타일의 일관성을 유지하고 가독성을 높여 협업의 효율을 극대화하기 위해서이다.

작업순서는 ESLint가 Prettier 규칙을 이해하도록 먼저 설치/연동하는 것이 좋다.

### ESLint

ESLint의 설치는 다음과 같다.

```bash
> yarn add -D eslint
```




