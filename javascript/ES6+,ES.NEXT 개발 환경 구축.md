# Babel과 Webpack을 이용한 ES6+/ES.NEXT 개발 환경 구축



[자바스크립트 Deep Dive] 책의 49장 ES6+/ES.NEXT 개발 환경 구축을 통해 Babel와 Webpack, Polyfill을 공부해보자.

## Babel

### 필요성

- 크롭, 사파리, 파이어폭스, 엣지 같은 에버그린 브라우저(별도의 재설치 없이 업데이트가 가능한 브라우저)의 ES6 지원률은 98%로 거의 대부분 지원
- IE의 경우 ES6 지원률을 11% 정도로 최신 문법의 경우 IE에서 실행되지 않아 ES5 수순으로 트랜스 파일링이 필요함

### 설명

- ES6+/ES.NEXT로 구현된 최신 사양의 소스코드를 IE 같은 구형 브라우저에서도 동작하는 ES5 사양의 소스코드로 변환(트랜스파일링)해주는 트랜스파일러

### 설치

- npm을 이용해 설치

```bash
# 프로젝트 폴더 생성
$ mkdir esnext-project && cd esnext-project
# npm init -y
$ npm init -y
# babel-core, bable-cli 설치
$ npm install --save-dev @babel/core @babel/cli
```

- package.json 파일의 “devDependencies”에 “@babel/core”와 “@babel/cli” 확인
  - npm install 은 항상 최신 버전을 설치함

### Babel 프리셋

- @babel/preset-env
- 함께 사용되어야 하는 Babel 플러그인을 모아 둔 것
- Babel이 제공하는 공식 프리셋 리스트
  - @babel/preset-env
  - @babel/preset-flow
  - @babel/preset-react
  - @babel/preset-typescript
- 프로젝트 지원환경은 Browserlist 형식 [(참조)](https://github.com/browserslist/browserslist)
  - .browserlistrc 파일에서 설정가능(기본값 있음)
- 설치

```bash
# @babel/preset-env 설치
$ npm install --save-dev @babel/preset-env
```

- 최종 설치 완료 후 babel.config.json 파일 생성 후 다음과 같이 작성. 방금 설치한 @babel/preset-env를 사용하겠다는 의미

```bash
{
    "presets": ["@babel/preset-env"]
}
```

### 트랜스파일링

- Babel CLI를 이용함
- 매번 하기 번거로우니 package.json 파일에 scripts를 추가

```tsx
"scripts": {
    "build": "babel src/js -w -d dist/js"
}
```

- 코드 설명
  - 타겟 폴더(srs/js)에 있는 모든 자바스크립트 파일을 트랜스 파일링 후 dist/js 폴더에 저장
  - -w: 타깃 폴더에 있는 모든 자바스크립트 파일들의 변경을 감지해 자동으로 트랜스파일링 (—watch 옵션의 축약형)
  - -d: 트랜스파일링 된 결과물이 저장될 폴더를 지정. 폴더가 존재하지 않을 시 자동으로 생성 (—out-dir 옵션의 축약형)
  - 터미널에 npm run build 시 트랜스파일링

### Babel 플러그인 설치

- Babel 홈페이지 상단 메튜의 Search란에 제안 사양의 이름을 입력해 필요한 플러그인을 검색할 수 있음.
- 지금은 클래스 필드 정의 제안 플러그인을 검색하기 위해 “class field’를 입력
- 검색된 플러그인 중 public/private 클래스 필드를 지원하는 @bable/plugin-proposal-class-properties를 설치

```bash
$ npm install --save-dev @babel/plugin-proposal-class-properties
```

- 설치한 플러그인을 babel.config.json 설정 파일에 추가

```tsx
{
    "presets": ["@babel/preset-env"],
    "plugins": ["@babel/plugin-proposal-class-properties"]
}
```

### 문제점

- 위 방법으로 트랜스파일리 시 Node.js 가 기본 지원하는 CommonJS 방식의 모듈 로딩 시스템에 따름
- 따라서 트랜스파일링 된 js 파일에 require 함수가 생기는 데 여기서 문제가 발생함
- 브라우저는 CommonJS 방식의 require 함수를 지원하지 않아서 에러가 발생

```bash
Uncaught ReferenceError: require is not defined
```

### 해결 방법

- **Webpack**을 통해 문제 해결
  - Webpack이 자바스크립트 파일을 번들링하기 전에 Babel을 로드해 ES6+/ES.NEXT 사양의 소스코드를 ES5 사양의 소스코드로 트랜스파일링하는 작업을 실행하도록 설정(아래로 계속 설명)

## Webpack

### 설명

- 의존 관계에 있는 자바스크립트, CSS, 이미지 등의 리소스들을 하나(또는 여러개 개)의 파일로 번들링하는 모듈 번들러
- 사용시 의존 모듈이 하나의 파일로 번들링되므로 별도의 모듈 로더가 필요 없음.
- 또한 여러 개의 자바스크립트 파일을 하나로 번들링해서 HTML 파일에서 script 태그로 여러 개의 자바스크립트 파일을 로드해야 하는 번거로움도 사라짐

### Webpack 설치

- 터미널에 다음 명령어 입력

```bash
$ npm install --save-dev webpack webpack-cli
```

### babel-loader 설치

- Webpack이 모듈을 번들링할 때 Babel을 사용해 ES6+/ES.NEXT 사양의 소스코드를 ES5 사양의 소스코드로 트랜스파일링하도록 babel-loader를 설치

```bash
$ npm install --save-dev babel-loader
```

- 설치 후 npm scripts에 build를 변경

```tsx
"scripts": {
    "build": "webpack -w"
}
```

### webpack.config.js 설정 파일 작성

- 프로젝트 루트 폴더에 작성

```jsx
const path = require('path');

module.exports = {
    // entry file
    // <https://webpack.js.org/configuration/entry-context/#entry>
    entry: './src/js/main.js',
    // 번들링된 js 파일의 이름(filename)과 저장될 경로(path)를 지정
    // <https://webpack.js.org/configuration/output/#outputpath>
    // <https://webpack.js.org/configuration/output/#outputfilename>
    output: {
        path: path.resolve(__dirname, 'dist'),
        filname: 'js/bundle.js'
    },
    // <https://webpack.js.org/configuration/module>
    module: {
        rules: [
            {
                test: ^.js$/,
                include: [
                    path.resolve(__dirname, 'src/js')
                ],
                exclude: /node_modules/,
                use: {
                    loader: 'babel-loader',
                    options: {
                        presets: ['@babel/preset-env'],
                        plugins: ['@babel/plugin-proposal-class-properties']
                    }
                }
            }
        ]
    },
    devtool: 'source-map',
    // <https://webpack.js.org/configuration/mode>
    mode: 'development'
};
```

- npm run build로 트랜스파일링(babel) 및 번들링(Webpack) 실행하기 ⇒ dist/js 폴더에 bundle.js가 생성됨

### babel-polyfill 설치

- Babel을 사용해도 브라우저가 지원하지 않는 코드가 남아있을 수 있음.
  - 예) Promis, Object.assign, Array.from 등은 ES5 사양에 대체할 기능이 없음 ⇒ 트랜스파일링 불가
- 이를 위해 @babel.polyfill을 설치

```bash
$ npm install @babel/polyfill
```

- 설치 후 package.json 파일의 dependencis에 추가됨

### 주의할 점

- @babel-polyfill은 개발 환경에서만 사용하는게 아니라 실제 운영 환경에서 사용하므로 개발의존성(devDependencies)로 설치하는 —save-dev 옵션을 지정하지 않는다.

### 사용

- ES6의 import를 사용하는 경우 import 위에 polyfill을 로드해야함

```jsx
import "@babel/polyfill";
import ...
```

- Webpack을 사용하는 경우 webpack.config.js 파일의 entry 배열에 추가

```jsx
const path = require('path');

module.exports = {
    // entry file
    // <https://webpack.js.org/configuration/entry-context/#entry>
    entry: ['@babel/polyfill', './src/js/main.js'],
...
```

- Webpack을 다시 실행하면 dist/js/bundle.js 에 polyfill이 추가된 것 확인 가능
