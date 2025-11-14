# 프로젝트 생성

## Vite로 React 프로젝트 생성
```
> yarn create vite project_name
```

- ```Select a framework:```는 ```React``` 선택
- ```Select a variant:```는 ```TypeScript``` 선택
- ```Use rolldown-vite (Experimental)?:```는 ```No``` 선택
- ```Install with yarn and start now?```는 ```Yes``` 선택

```rolldown-vite``` vite 팀에서 개발중인 새로운 실험용 번들러로 아직까지는 테스트 중임

> 번들러란? React나 TypeScript 프로젝트를 개발할 때, 코드는 보통 여러 파일(.tsx, .ts, .css 등)로 나뉘어 있어요.
브라우저는 모듈화된 파일을 그대로 이해하지 못할 수도 있기 때문에, 배포용으로 한두 개의 파일로 합치고 최적화해야 합니다.
이 역할을 하는 도구가 바로 **번들러(Bundler)**입니다.
