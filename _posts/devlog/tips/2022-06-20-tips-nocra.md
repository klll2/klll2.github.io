---
layout: post
title: "ex [React] CRA 없이 바벨과 웹팩으로 React 개발환경 만들기"
subtitle: "[React] CRA 없이 바벨과 웹팩으로 React 개발환경 만들기"
category: devlog
tags: tips aws
image:
  path: /assets/img/reactlogo.png
---

<!-- more -->

- this ordered seed list will be replaced by the toc
  {:toc}

# CRA 없이 React 개발환경 만들기

---

우리는 흔히 리액트 개발 환경을 세팅할 때 CRA를 쓰곤 합니다.  
설치 명령어 단 한 줄로 웹 팩과 바벨로 이루어진 프로젝트 환경을 구성해 주기 때문이죠.

번거로운 작업들을 다 해주니 아주 편하지만 내가 개발하고자 하는 리액트 프로젝트가  
어떻게 이루어져 있는지는 알고는 있어야 하지 않을까요?

그리고 우리가 어떤 기업에서 프로젝트를 한다고 했을때 꼭 필요한 것들 외에는 클린하고  
프로젝트 만의 규칙과 커스터마이징이 필요하다면?  
그렇다면 정말 필요한 라이브러리와, 플러그인, 로더를 만 적용해야 할 것입니다.

이번 포스팅을 통해서 웹팩으로는 어떠한 플러그인이 적용되는지, 바벨을 통해서  
어떻게 리액트 초기세팅이 이루어지고 커스터마이징이 어떻게 되는지 알아봅시다!

## 노드 초기화와 리액트 설치

- 프로젝트를 시작할 빈 폴더를 만들어 줍니다.

- 만든 폴더에서 터미널을 열어 노드 초기화를 해줍니다.

```
npm init -y
```

- 리액트 코어와 리액트를 웹에서 UI를 표시해줄 리액트 돔을 설치 합니다.

```
npm install react react-dom
```

- 만약 타입스크립트를 적용하고자 한다면 같이 설치해 줍니다.

```
npm install typescript
npm install @types/react @types/react-dom
```

- 타입스크립트를 하시는 분은 `tsconfig.json` 파일도 도 만들어 줍시다.

```
tsc --init
```

## 웹팩과 바벨 설치

- 웹팩과 바벨 관련 파일을 설치 하겠습니다.

  - webpack : 웹팩 코어
  - webpack-cli: 웹팩을 CLI에서 사용
  - webpack-dev-server : 실시간 개발 서버 환경을 구동가능

```
npm install -D webpack webpack-cli webpack-dev-server
```

- css-loader : CSS 코드를 JS가 이해할 수 있게 변환
- style-loader : 변환된 CSS 파일을 index.html의 `<style>` 태그에 삽입
- babel-loader : ES6+, JSX 문법을 트랜스파일링

```
npm install -D css-loader style-loader babel-loader
```

- 브라우저 별로 서로 다른 자바스크립트를 이해할 수 있도록 통합해 줄 babel을 설치 합니다.
- 바벨의 모듈은 @ 마크가 붙는 특징이 있습니다.

  - babel/core : 바벨코어
  - babel/preset-react : 리액트의 JSX 코드를 트랜스파일링
  - babel/preset-env : ES6 코드를 ES5로 트랜스파일링

```
npm install -D @babel/core @babel/preset-react @babel/preset-env
```

- 플러그인을 설치 하겠습니다.

  - html-webpack-plugin : HTML 파일에 번들링된 JS 코드를 삽입하고, dist 폴더에 번들링된 결과를 옮겨줌
  - clean-webpack-plugin : 번들링 할 때 마다 이전의 번들링 결과를 제거

```
npm install -D html-webpack-plugin clean-webpack-plugin
```

이제 npm으로 설치해야 할 것은 다 설치 했습니다. 이제 설정으로 가봅시다.

- 타입스크립트를 하신다면 추가로 설치해 줍니다.
- `npm i @types/node @types/webpack @babel/preset-typescript`

## 웹팩과 바벨 설정

- 웹팩 먼저 설정 하겠습니다.

- root 경로에 `webpack.config.js` 파일을 만들고 프리셋을 설정합니다.

```java
const webpack = require('webpack');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const { CleanWebpackPlugin } = require('clean-webpack-plugin');

module.exports = {
  mode: 'development', // 개발모드인지 프로덕션모드인지 설정해줍니다. env도 가능
  entry: './src/index.js',  // 웹팩 번들링을 할 파일
  output: {  // 번들링이 완료되면 저장될 경로와 번들링 파일 이름
    path: __dirname + '/dist',
    filename: 'bundle.[hash].js',
    publicPath: '/',
  },
  resolve: {  // 번들링의 대상이 될 파일 확장자
    // path.resove 형태로 사용할 수도 있다.
    // 그러면 node의 기본 모듈 'path'를 불러와야 한다.
    extensions: ['.js', '.jsx'],
  },
    module: {
    rules: [
      {
        test: /\.(js|jsx)$/,  // js와 jsx의 확장자를 가진 것은 바벨 로더를 거침
        exclude: '/node_modules/',
        // 노드 모듈은 제외
        loader: 'babel-loader'
      },
      {
        test: /\.css$/,
        use: [{ loader: 'style-loader' }, { loader: 'css-loader' }]  // 순서가 중요합니다.
      }
    ]
  },
  plugins: [
    new CleanWebpackPlugin(),  // 이전에 번들링 됐던 파일을 삭제
    new HtmlWebpackPlugin({
      // index.html에 번들링된 파일을 link 와 script 태그에 추가
      template: 'public/index.html'
    }),
    new webpack.DefinePlugin({
      mode: process.env.mode,
      port: process.env.port
    })
  ],
  devServer: {
    host: 'localhost',
    port: process.env.port,
    open: true,
    historyApiFallback: true,
    hot: true
  }
};
```

- 바벨을 설정 하겠습니다.
- root 폴더에 `babel.config.js`를 만들고 다음과 같이 프리셋을 넣어줍니다.

```java
module.exports = {
  presets: ['@babel/preset-env', '@babel/preset-react']
};
// babel/preset-env : ES6 이상의 문법을 ES5 이하로 변환해 준다.
// babel/preset-react : jsx 문법을 js 코드로 변환해준다.
```

## 리액트 실행 환경 만들기

- `package.json` 을 열어 리액트 실행 스크립트를 등록합니다.

```java
"scripts": {
  "start": "webpack serve --progress --mode development",
  "build": "webpack"
}
// start 명령어를 등록해서 리액트 스크립트가 제대로 동작 할 수 있도록 설정합니다.
```

- 리액트 컴포넌트를 만듭니다.
- root 폴더에 public 폴더를 만들고 `index.html` 을 만들고 아래의 내용을 입력합니다.

```html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=divice-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>title</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
```

- root 폴더에 src 폴더를 만들고 `index.js`를 만들고 아래의 내용을 입력합니다.
- React 18 버전 기준입니다.

```java
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App'

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
```

- root 폴더의 src 폴더 안에 `App.js`를 만들고 아래의 내용을 입력합니다.

```java
const App = () => {
  return <div>hello :)</div>;
};

export default App;
```

## 리액트 실행

이제 `npm start`를 해보세요.
실행이 잘 될 것입니다.

이제 prettier나 eslint 등 프로젝트에 필요한 라이브러리들을 설치하면 됩니다.

웹 팩과 바벨의 설정, 플러그인 등은 구글을 검색하면 더욱 많이 나올 것입니다.
