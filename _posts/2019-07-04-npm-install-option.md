---
layout: post
title: "npm install 명령어에 있는 option들"
subtitle: "--save와 --save-dev의 차이"
date:   2019-07-04 09:01:00 +0900
categories: npm
tags: [npm]
comments: true
---

```javascript
npm install [package]
```
javascript로 개발을 하면서 npm관련하여 사용하는 명령어 중에서도 가장 많이 활용하는 명령어가 <mark>npm install</mark>이 아닐까 생각한다. 습관처럼 자주쓰는 몇가지 옵션만 사용하지만 다른 것 들은 어떤것이 있는지 찾아 보았다.🧐  


npm install --save와 npm install --save-dev의 차이점과 함께 다른 옵션들도 확인 해 보았다.

---

<mark>npm install</mark>이란 `./node_modules`폴더에 패키지를 다운받아 설치하기 위한 명령어이다.  

```javascript
npm install
// package.json의 dependencies에 있는 모든 패키지를 설치한다.
// 처음 프로젝트를 세팅했다면 이 명령어로 패키지를 설치하고 개발을 시작하면 된다.

npm i
// npm install 의 줄인 명령어. 

npm install [package]
// 현재 작업중인 디렉토리 내에 있는 ./node_modules에 [package]를 설치한다. 
// (예: npm install moment) -> ./node_modules에 moment 패키지를 설치 함

npm install [package] --save
// [package]를 설치 하면서 package.json파일에 있는 dependencies 객체에 지금 설치한 패키지 정보를 추가한다.

npm install [package] --save -dev
// --save옵션과 같이 package.json파일에 의존성 내용을 추가하지만 dependencies가 아닌 devDepenencies 객체에 추가한다.
```

--save와 --save-dev의 차이는 의존성을 기본으로 추가할지, 개발용으로 추가할지의 차이이다.  
`--production`로 빌드할 경우 devDepenencies에 있는 패키지들은 설치되지 않는다!  

그 외에도 문서를 찾아보니 사용 해 본적은 없지만(?) 다른 옵션들이 많이 있었다.
```javascript
npm install [package] --no-save
// dependencies에 패키지 정보를 추가하지 않는다.

npm install [package] --save-exact
// 정확히 일치하는 버전의 패키지를 추가한다.

npm install [package] --save-bundle
// 해당 패키지를 bundleDependencies에 추가한다.

npm install [package] --force
// 해당 패키지가 존재하더라도 원격 저장소에 있는 패키지를 가져온다.

..
..

```

위에 모든 옵션을 적진 않았지만 제공하는 옵션을 통해 원하는 설정으로 패키지를 설치하는데에 무리가 없을것으로 보인다.  


---
**참고 사이트**  
https://docs.npmjs.com/cli/install  
https://stackoverflow.com/questions/22891211/what-is-the-difference-between-save-and-save-dev/31358981
