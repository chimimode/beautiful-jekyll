---
layout: post
title: "webpack과 babel로 프로젝트 설정하기"
subtitle: "javascript 프론트엔드 개발환경 구성하는 법"
date: 2019-07-026 09:00:00 +0900
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
