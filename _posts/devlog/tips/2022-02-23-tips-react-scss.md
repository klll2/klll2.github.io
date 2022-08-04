---
layout: post
title: '[React] 리액트 SCSS(SASS) 적용하는 법'
subtitle: '[React] 리액트 SCSS(SASS) 적용하는 법'
category: devlog
tags: tips react scss
image:
  path:    /assets/img/sasslogo.png
---

프론트엔드 개발자라면 필수적으로 CSS 작업을 해야 할 일이 생긴다.  
그리고, React와 같은 라이브러리를 쓴다고해도 마찬가지이다.  

요즘은 많은 개발자들이 CSS 전처리기를 많이쓰고 있는데, 그중에 SCSS(SASS)와  
리액트를 연동하는 방법을 설명하고자 한다.  

<!-- more -->

1. this ordered seed list will be replaced by the toc 
{:toc}  

## 설치방법  
---  

우선 터미널로 컴파일러를 설치해줘야 한다.  
* SCSS를 적용하고 싶은 리액트 앱 폴더로 이동한다.  
* 컴파일러를 설치한다.  
  * yarn 일 경우 `yarn add node-sass`  
  * npm 일 경우 `npm install node-sass`  

* 끝이다. 아주 간단하다.  
* 당연하겠지만 scss를 사용할 해당 리액트 앱 마다 따로 해줘야 한다.  

![json](/assets/img/tips/2022-02-23-react-scss/2022-02-23-react-scss.png){:.centered} package.json 파일  
{:.figcaption}  

* package.json 에 node-sass 가 있는지 확인하자!  

## 사용방법  
---  

* 지금까지 작업 하던 CSS의 확장자를 scss(sass) 로 변경  
  * 새로 작업 할 예정이라면 파일명.scss 으로 파일 생성
* 적용할 컴포넌트의 Import를 scss(sass) 로 변경 해준다.  
  * 예) `import "./App.scss"`
* 저장 하고 페이지 화면을 보면 아주 잘 적용되어 있는 것을 볼 수 있다!  