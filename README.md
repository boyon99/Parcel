# Parcel
구성 없는 단순한 자동 번들링으로 소/중형 프로젝트에 적합하다.
- https://ko.parceljs.org/


## 시작하기
`npm init`
`npm i`
`npm install -D parcel-bundler`

```json
"scripts": {
  "dev": "parcel index.html",
  "build": "parcel build index.html"
}
```

- index.html & js/main.js & scss/main.scss 파일 생성하기
- index.html 파일에 js와 css 연결하기

`npm run build`
> 여기까지 하면 html, js, scss 파일을 사용할 수 있음



### 정적 파일 연결

// 새로운 파일을 추가할 경우 index.html에 연결되지 않는다. 그 이유는 dist 폴더에 없기 때문으로 자동으로 dist 폴더에 추가해주는 패키지를 설치한다.

`npm i -D parcel-plugin-static-files-copy`

```json
"staticFiles" : {
  "staticPath" : "static" 
  // static 폴더를 dist 폴더에 자동으로 추가함
}
```
// package.json에 해당 내용 추가

- dist 폴더 생성 후 그 폴더에 logo.png 이미지 추가 후 index.html 파일에 연결하기

`npm run dev`
> static 폴더 안의 정적 파일과 scss, js 자동으로 연결됨.


### autoprefixer
// 브라우저를 의미하는 자동 접두사를 붙여서 적용해주도록 하는것

`npm i -D postcss autoprefixer`

> [npm install 설치시 npm ERR! code ERESOLVE 오류 해결](https://iancoding.tistory.com/154)

```json
"browserslist" : [
  "> 1%", // 점유율이 1% 이상인 
  "last 2 versions" // 마지막 2개 버전까지는 지원함
]
```
// package.json에 위와 같이 작성한다.


- 루트 폴더에 .postcssrc.js 생성하기 
// .은 구성파일 또는 숨김파일을 나타내며 마지막에 rc는 구성파일을 의미


> ESM, (nodejs환경) CommonJS이기 때문에 import 대신 require()을 export 대신 module.exports()사용해야 한다.

```js
// postcssrc.js 
module.exports = {
  plugins: [
    require('autoprefixer') // 간소화
  ]
}
```
> PostCSS plugin autoprefixer requires PostCSS 8.에러 시 `npm i -D autoprefixer@9`

`npm run dev`



### babel
// ES6+이상 자바스크립트 코드를 이전 버전과 호환 가능하도록 해주는 트랜스 컴파일러이다.

`npm i @babel/core @babel/preset-env`

- .babelrc.js 파일 생성하기
```js
// .babelrc.js
module.exports = {
  presets:['@babel/preset-env']
}
```

// 이전에 작성한 package.json의 brosweslist의 영향을 받음, 따로 작성할 필요 없음

- test를 위해 js/main.js에 신버전 문법 작성

> 추가적으로 `npm i -D @babel/plugin-transform-runtime` 작성해도 좋음 (강의 영상에서는 최신버전이 적용안되는 문제로 작성했으나 실제 환경에서는 오류 없음)

`npm i -D @babel/plugin-transform-runtime`

```js
// .babelrc.js
  plugins: [
    ['@babel/plugin-transform-runtime']
  ]
```

6. CLI (커맨드 라인 인터페이스)
- https://ko.parceljs.org/cli.html
