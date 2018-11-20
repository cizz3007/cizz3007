---
title: 바벨 설정(babel 7.0, babel.config.js) 
date: 2018-11-20 18:56:00
description: <center>새로운 바벨 환경설정, babel.config.js</center>

categories:
- babel
- webpack
- front
- config
tags:
- webpack
- babel
---

>  ======================================================================<br>
babel docs [https://babeljs.io/docs/en/configuration](https://babeljs.io/docs/en/configuration)
   ======================================================================

우리회사는 .babelrc에 babel에 관한 설정을 해왔는데, 한 참 신경을 놓고 있다가 보니
babel의 빌드가 벌써 7.1.6까지 나왔다.    
현재 프로젝트의 babel 버전이 6이었기에 업그레이드로 하기로 하였고 업그레이드 하면서 기존의 바벨과 다른 점과 설치과정을 포스팅해보겠다.    
업그레이드 하면서 느낀 점은 babel은 항상 또 항상, 최신버전으로 웬만하면 유지해주자.

### NPM으로 먼저 바벨부터 깔자
___

> 7이전 버전이랑은 npm 스트링이 좀 다르다. 예전에는 babel babel-core babel-cli였던 것 같았는데?    

```javascript
npm install -D @babel/core @babel/cli @babel/preset-env @babel/polyfill

```
![https://user-images.githubusercontent.com/32691294/48762013-6cb4e980-eced-11e8-8a76-e92d48c331e1.jpg](https://user-images.githubusercontent.com/32691294/48762013-6cb4e980-eced-11e8-8a76-e92d48c331e1.jpg)


### 이제 .babelrc 보다는 babel.config.js를 쓰자.
___
그다음에는 babel.config.js를 설정해주면 된다. webpack.config.js처럼 root에 위치시켜두자.

공식홈에서도 babel.config.js를 쓰기를 적극 권장하고 있다.    
babelrc보다 babel.config.js가 플러그인과 프리셋을 좀 더 프로그래밍틱하게 관리할 수 있게 해준다.
만들어 주자.

```javascript
//babel.config.js설정
module.exports = (api) =>{
    const babelEnv = api.env();
    const babelVer = api.version;
    console.log(` -- 바벨(${babelVer})모드 : ${babelEnv} --`);
    const presets = ['@babel/preset-env'];
    // const plugins = [...];

    return {
        presets,
        // plugins
    };
};
```
> 현재 폴더 구조

![https://user-images.githubusercontent.com/32691294/48764335-bf44d480-ecf2-11e8-8477-a1c144fd02c4.jpg](https://user-images.githubusercontent.com/32691294/48764335-bf44d480-ecf2-11e8-8477-a1c144fd02c4.jpg)

이런식이라고 가정하고,
index.js에 es6이상의 문법을 작성해보자

```javascript
const a = 'babel';

let sum = (a,b)=> a+b;

console.log(sum);
```

```javascript
//터미널에 경로에 맞춰서 입력하자.
npx babel index.js --out-dir outputfolder
```
> 결과

![https://user-images.githubusercontent.com/32691294/48764618-82c5a880-ecf3-11e8-9a3a-bd4fe0f6bdd7.jpg](https://user-images.githubusercontent.com/32691294/48764618-82c5a880-ecf3-11e8-9a3a-bd4fe0f6bdd7.jpg)
![https://user-images.githubusercontent.com/32691294/48764647-91ac5b00-ecf3-11e8-9884-9f534a5f0545.jpg](https://user-images.githubusercontent.com/32691294/48764647-91ac5b00-ecf3-11e8-9884-9f534a5f0545.jpg)

```javascript
//트랜스컴파일된 결과물
"use strict";

var a = 'babel';

var sum = function sum(a, b) {
  return a + b;
};

console.log(sum);
```





