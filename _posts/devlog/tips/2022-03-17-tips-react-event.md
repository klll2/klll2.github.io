---
layout: post
title: "ex [React] 리액트에서 input태그 Enter 키 이벤트 호출하는 방법"
subtitle: "[React] 리액트에서 input태그 Enter 키 이벤트 호출하는 방법"
category: devlog
tags: tips react
image:
  path: /assets/img/reactlogo.png
---

바닐라 자바스크립트에서 로그인 기능이나 검색기 기능 구현을 할때 `Input` 과 `Button`  
태그를 이용해서 엔터를 누르면 따로 마우스로 버튼을 클릭하지 않아도 됐었다.

물론 리액트도 그렇지만 `submit` 옵션이나 `<button>` 태그가 아니라면 되지 않거나,  
그 외에 상황에서 작동이 하지 않을 때가 간혹 있다.

이 포스팅에서는 Enter 키 만으로도 버튼 클릭 이벤트를 구현하는 방법을 소개하겠다.

<!-- more -->

1. this ordered seed list will be replaced by the toc
   {:toc}

## 로그인 페이지

---

- 기본적인 로그인 모양인 인풋 2개, 버튼 하나를 대충 만들어 보았다.
- 아이디, 비밀번호를 입력후 버튼을 누르면 'main' 페이지로 이동되는 구조이다.

```react
// file: "Login.js"
return (
        <form>
          <input
            type="text"
            placeholder="ID 입력"
            onChange={handleInput}
          />
          <input
            type="password"
            placeholder="비밀번호 입력"
            onChange={handleInput}
          />
            <input
            type="button"
            value="로그인"
            onClick={()=>{navigate("/main")}}
          />
        </form>
```

- 이상태로는 비밀번호까지 입력 후 엔터를 눌렀을때 아무런 응답이 없다.
- 마우스로 버튼을 직접 클릭 해주어야 한다.

## KeyPress 이벤트 함수 만들기

---

- 인풋에서 Enter 키를 누르면 자동으로 버튼 클릭 이벤트를 발생하게하는 로직을 만들면 된다.
- Enter 키를 감지하는 함수를 만들고 그 안에 버튼 클릭 이벤트를 넣어
  인붙에 `onKeyPress` 이벤트를 등록해주면 된다.

```react
const handleOnClick = () => {
  navigate('/main');
};
// 버튼에 적용할 클릭 이벤트 함수


const handleOnKeyPress = e => {
  if (e.key === 'Enter') {
    handleOnClick(); // Enter 입력이 되면 클릭 이벤트 실행
  }
};
// 인풋에 적용할 Enter 키 입력 함수
```

## 적용하기

---

```react
return (
        <form>
          <input
            type="text"
            placeholder="ID 입력"
            value={idValue}
            onChange={handleInput}
          />
          <input
            type="password"
            placeholder="비밀번호 입력"
            value={pwValue}
            onChange={handleInput}
            onKeyPress={handleOnKeyPress} // Enter 입력 이벤트 함수
          />
            <input
            type="button"
            value="로그인"
            onClick={handleOnClick}  // 페이지 이동 함수
          />
        </form>
```

- 이렇게 적용하고 나서 아이디와 비밀번호 입력 후 엔터를 누르면 Click 이벤트가 실행되면서
  다음 페이지로 잘 넘어가는 것을 볼 수 있다.
