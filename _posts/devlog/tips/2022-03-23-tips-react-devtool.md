---
layout: post
title: "ex [React] 크롬 React Developer Tools 를 활용하자!"
subtitle: "[React] 크롬 React Developer Tools 를 활용하자!"
category: devlog
tags: tips react
image:
  path: /assets/img/reactlogo.png
---

프론트엔드 개발자라면 뗄라야 뗄수 업는 크롬 개발자 도구!  
리액트 개발자들을 위한 리액트 개발자 도구도 있다는 것을 알고 계신가?!  
리액트를 처음 접하는 초급 주니어 개발자중에는 간혹 이것을 모르는 경우도 있다.

아주 가볍게 이것을 알아보자.

<!-- more -->

- this ordered seed list will be replaced by the toc
  {:toc}

## 크롬 확장프로그램 설치

---

- 크롬브라우저의 설정에 가면 좌측 메뉴에 확장 프로그램이 있다. "React Develop Tools" 검색
- 귀찮다면 여기로 -> [React Develop Tools 다운로드](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=ko)

![사진1](/assets/img/tips/2022-03-23-react-devtool/2022-03-23-react-tool_1.png)

## 기본 기능들

---

![사진1](/assets/img/tips/2022-03-23-react-devtool/2022-03-23-react-tool_2.png)

- 우측 상단에 'Components'와 'Profiler'가 생긴 것을 볼 수 있다.
- 사진은 'Components' 화면이다.
- 우리가 요소 탭에서 HTML의 구조를 보듯이 Component 구조를 볼 수 있다.  
  물론 컴포넌트 외에 전달되는 props도 확인 할수 있고 직접 값을 수정해 볼 수도 있다.

- 'Component' 탭 밑의 톱니를 누르면 다음과 같은 화면이 뜬다.

![사진1](/assets/img/tips/2022-03-23-react-devtool/2022-03-23-react-tool_3.png)

- 'Highlight updates when components render.' 를 체크 하면 리액트로 만든 사이트들이  
  어떻게 렌더링이 되고 있는지 확인할 수 있다. 직접 눈으로 확인하면서 최적화 할 수 있다.
- 밑의 사진 처럼 체크 한 후에 웹페이지의 기능들을 작동을 렌더링 되고있는곳을 알려준다.

![사진1](/assets/img/tips/2022-03-23-react-devtool/2022-03-23-react-tool_4.gif)

### 이제 리액트도 개발자 도구를 보며 개발 하자!!
