# 프로젝트 생성

## Vite로 React 프로젝트 생성

```bash
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

프로젝트 생성 시 프로젝트 이름 뒤에 ```--template react-ts```를 붙이면 ```Select a framework:```와 ```Select a variant:``` 잘문을 넘겨서 프로젝트를 생성할 수 있다.

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

다음은 ESLint의 초기화 과정을 수행한다.

```bash
> npx eslint --init
```

이 과정에서 설정을 위해 몇가지 질문이 나타나는데 질문과 해당 선택은 다음과 같다.

```bash
Ok to proceed? (y) y

What do you want to lint? · javascript
How would you like to use ESLint? · To check syntax and find problems
What type of modules does your project use? · JavaScript modules (import/export)
Which framework does your project use? · react
Does your project use TypeScript? · Yes
Where does your code run? · browser
Which language do you want your configuration file be written in? · ts

Would you like to install them now? · Yes
Which package manager do you want to use? · yarn
```

프로젝트 루트에 ```eslint.config.ts``` 파일이 생성된다.

### Prettier

Prettier의 설치는 다음과 같다.

```bash
yarn add -D prettier
```

다음 프로젝트 루트에 ```.prettierrc``` 파일을 생성하여 다음과 같이 작성한다.

```
{
  "semi": true,
  "singleQuote": true,
  "printWidth": 100,
  "tabWidth": 2,
  "trailingComma": "es5"
}
```

다음으로 ```eslint.config.ts``` 파일을 다음과 같이 수정한다.
```ts
...
//추가
import prettierPlugin from "eslint-plugin-prettier";
import prettierConfig from "eslint-config-prettier";

export default defineConfig([
  { 
    files: ["**/*.{js,mjs,cjs,ts,mts,cts,jsx,tsx}"], 
    plugins: { 
      prettier: prettierPlugin,  //수정
     },
    //////////추가
    rules: {
      ...js.configs.recommended.rules,
    },
    //////////////
    extends: ["js/recommended"], 
    languageOptions: { globals: globals.browser } 
  },
  tseslint.configs.recommended,
  pluginReact.configs.flat.recommended,
  prettierConfig, //추가
]);
```

### VSCode 확장

```ESLint```와 ```Prettier - Code formatter```를 설치한다.





