---
layout: post
title: "webpack과 babel로 프로젝트 설정하기"
subtitle: "javascript 프론트엔드 개발환경 구성하는 법"
date:   2019-07-026 09:00:00 +0900
categories: javascript
tags: [webpack, babel]
comments: true
---
프론트엔드 개발을 위한 프로젝트를 설정함에 있어 webpack과 babel을 이용 해 초기 구성하는 순서를 기록으로 남겨놓는다.
<code>vscode</code>와 <code>npm</code>을 사용하여 진행한 설정 순서이다.

먼저 프로젝트로 사용할 폴더의 위치로 이동한 뒤 vscode의 터미널을 열어서 아래의 명령어를 입력 해 준다.

### 1. package.json 파일 만들기. (npm사용 프로젝트로 지정)
```javascript
npm init -y
```
위 명령어를 입력하면 `package.json`파일이 생성되며 아래의 내용으로 작성 되어있을 것이다.
```javascript
{
  "name": "webpack-babel-setting",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "description": ""
}
```
---
### 2. 개발환경에서 쓸 webpack과 babel을 npm으로 설치하기.
```javascript
// babel 설치
npm install --save-dev babel-core babel-loader babel-preset-env
// webpack 설치
npm install --save-dev webpack webpack-dev-server
```
설치를 마치면 1.에서 생성했던 `package.json`파일에 devDependencies가 추가 되었을것이다.
```
// 추가된 devDependencies
...
...
"devDependencies": {
  "babel-core": "^6.26.3",
  "babel-loader": "^8.0.6",
  "babel-preset-env": "^1.7.0",
  "webpack": "^4.37.0",
  "webpack-dev-server": "^3.7.2"
}
```
---
### 3. npm run 명령어 설정하기
프로젝트를 빌드하고 실행시킬 명령어를 설정한다. 
`package.json`파일을 열어 `scripts` 항목을 편집 해 준다.
```javascript
...
...
// 초기 생성된 scripts항목
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
},
...
```
위 소스에 아래와 같은 <code>dev</code>, <code>build</code>, <code>devserver</code>를 추가 해 준다.
```javascript
...
...
// dev, build, devserver 추가
"scripts": {
  "dev": "webpack --mode development",
  "build": "webpack --mode production",
  "devserver": "webpack-dev-server --open --progress"
},
...
```
---
### 4. webpack.config.js 만들기
`package.json`파일이 있는 위치와 같은 곳에 `webpack.config.js`파일을 새로 생성 해 줍니다. 그리고 아래와같이 작성 합니다.
```javascript
const webpack = require('webpack');
const path = require('path');

module.exports = {
    entry: './src/index.js',
    output: {
        path: path.resolve(__dirname, 'dist'),
        publicPath: '/dist/',
        filename: 'bundle.js'
    },
    module: {
        rules: [
            {
                test: /\.js$/,
                include: path.join(__dirname),
                exclude: /(node_modules)|(dist)/,
                use: {
                    loader: 'babel-loader',
                    options: {
                        presets: ['env']
                    }
                }
            }
        ]
    }
};
```
---
이제 프로젝트 실행을위한 설정은 모두 끝났다!🤗
위에서 설정했던 npm 명령어들을 살펴보자.
- `npm run dev`: webpack이 실행되며 webpack4의 development모드로 실행됩니다.
- `npm run build`: webpack4의 production모드로 실행이 됩니다. 이는 uglify되어 압축된 파일이 생성됩니다.
- `npm run devserver`: 로컬환경에 개발서버를 띄웁니다.

개발진행을 할때 쓰일 명령어인 `npm run devserver`을 실행 해 보면 웹 브라우저에 <code>http://localhost:8080/</code>가 띄워지며 빈 화면이 보인다.

웹 브라우저는 열리지만 터미널 창에 아래와 같은 에러가 출력되었을 것이다.
```javascript
ERROR in Entry module not found: Error: Can't resolve './src/index.js' in '개발환경 디렉토리'

ERROR in multi (webpack)-dev-server/client?http://localhost ./index.js
Module not found: Error: Can't resolve './src/index.js' in '개발환경 디렉토리'
 @ multi (webpack)-dev-server/client?http://localhost ./index.js main[1]
i ｢wdm｣: Failed to compile.
```
---
### 5. js파일과 html 추가하기
`webpack.config.js` 파일의 <code>entry: './src/index.js'</code>에 해당하는 경로로 파일을 생성 해 준다.
- src 폴더 생성
- 생성한 src 폴더 안에 index.js 파일 생성
index.js 파일에는 아래의 샘플을 작성한다.
```javascript
console.log('setting!');
```  
브라우저에 출력할 html파일을 `webpack.config.js`의 위치와 같은 곳에 생성한다
```html
<!doctype html>
<html lang="ko">
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
        <meta name="description" content="javascript 프론트엔드 개발환경 구성하는 법">
        <title>webpack과 babel로 프로젝트 설정하기</title>
    </head>
    <body>
        브라우저 console창을 확인 해 보세요.
        <script type="text/javascript" src="/dist/bundle.js"></script>
    </body>
</html>
```
---
이제 `npm run devserver` 명령어를 실행하고 브라우저 창에서 화면을 확인하며 개발을 진행 하면 된다.  
`npm run build` 명령어를 입력하면 자동으로 `/dist/bundle.js` 가 생성되는것을 확인 할 수 있다.


---
Link  
https://beomi.github.io/2017/10/18/Setup-Babel-with-webpack/  
https://github.com/FEDevelopers/tech.description/wiki/(ES6)-webpack%EA%B3%BC-Babel%EC%9D%84-%EC%9D%B4%EC%9A%A9%ED%95%98%EC%97%AC-ES6-%EA%B0%84%EB%8B%A8%ED%95%9C-%EC%82%AC%EC%9A%A9%ED%99%98%EA%B2%BD-%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0
