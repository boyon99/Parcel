# [Parcel](https://ko.parceljs.org/)
구성 없는 단순한 자동 번들링으로 소/중형 프로젝트에 적합하다.


## 시작하기

### 설치 및 시작하기

#### 1-1. 설치하기
`npm install -D parcel-bundler`

#### 1-2. package.json의 script 작성하기
```json
"scripts": {
  "dev": "parcel index.html",
  "build": "parcel build index.html"
}
```

> `index.html` `js/main.js` `scss/main.scss` 파일 생성 후 html에 연결한 후 `npm run build`를 하면 html, js, scss 파일을 사용할 수 있다.

<br/>

### 정적 파일 연결
#### 2-1. 정적 파일을 dist 폴더에 자동으로 추가해주는 패키지를 설치한다.
`npm i -D parcel-plugin-static-files-copy`

#### 2-2. package.json의 staticFiles 작성하기
```json
"staticFiles" : {
  "staticPath" : "static" 
  // static 폴더를 dist 폴더에 자동으로 추가함
}
```


> dist 폴더 생성 후 그 폴더에 logo.png 이미지 추가 후 index.html 파일에 연결한 후 `npm run dev`하면 static 폴더 안의 정적 파일과 scss, js 자동으로 연결된다.


<br/>

### autoprefixer
#### 3-1. 브라우저를 의미하는 자동 접두사를 붙여서 적용해주는 패키지를 설치한다.

`npm i -D postcss autoprefixer`
> [npm install 설치시 npm ERR! code ERESOLVE 오류 해결](https://iancoding.tistory.com/154)

#### 3-2. package.json의 browserslist 작성하기
```json
"browserslist" : [
  "> 1%", // 점유율이 1% 이상인 
  "last 2 versions" // 마지막 2개 버전까지는 지원함
]
```

#### 3-3. 루트 폴더에 .postcssrc.js 생성한 후 다음과 같이 작성한다.

```js
// postcssrc.js 
// nodejs에선 CommonJS이기 때문에 import 대신 require()을 export 대신 module.exports을 사용해야 한다.
module.exports = {
  plugins: [
    require('autoprefixer') // 간소화
  ]
}
```

> PostCSS plugin autoprefixer requires PostCSS 에러 시 `npm i -D autoprefixer@9`

<br/>


### babel
#### 4-1. ES6+이상 자바스크립트 코드를 이전 버전과 호환 가능하도록 해주는 트랜스 컴파일러를 설치한다.

`npm i @babel/core @babel/preset-env`

#### 4-2. .babelrc.js 파일 생성 후 내용 작성하기

```js
// .babelrc.js
module.exports = {
  presets:['@babel/preset-env']
}
```

#### 4-3. 이전에 작성한 package.json의 brosweslist의 영향을 받아서 따로 작성할 필요는 없다.


<br/>

### [CLI (커맨드 라인 인터페이스)](https://ko.parceljs.org/cli.html)
