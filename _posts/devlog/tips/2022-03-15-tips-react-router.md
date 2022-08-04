---
layout: post
title: '[React] 리액트 Router V5 와 V6의 차이, 변경부분'
subtitle: '[React] 리액트 Router V5 와 V6의 차이, 변경부분'
category: devlog
tags: tips react router
image:
  path:    /assets/img/tips/2022-03-15-react-router/2022-03-15-router.svg
---
[Router 공식문서]:https://v5.reactrouter.com/core/api/Router  

리액트를 공부하면서 리액트 라우터도 필수적으로 하게된다. 여기서 문제점이 하나 있는데,  
자주 version 업이 되는 라이브러리 특성상 옛날 강의를 보면 어쩔수 없이 지난 버전으로  
공부를 하게 된다.  

물론 버전업이 되도 특별히 문법이 바뀌지 않으면 다행이지만, 이번에 다루어 볼 리액트 라우팅은  
조금의 함수 변동이 있다.

<!-- more -->

1. this ordered seed list will be replaced by the toc 
{:toc}  


## Exact 옵션의 삭제  
---  

* 기존에는 설정한 루트 ('/) 에 정확한 접근을 위하여 `exact` 속성을 썼다. 하지만 v6 에서는  
기본적으로 제일 비슷한 것을 매칭해 주기에 기본 설정으로 바뀌게 되면서 삭제됐다.  

```react
// file: "Router.js"
// v5
<Route exact path="/Login"... />;

// v6
<Route path="/Login"... />;
```

## Switch 는 이제 잊어라!  
---  

* 이전에는 라우터 페이지 등록을 위한 `<Route />` 를 감싸는 태그가 `<Switch />` 였다면  
v6 에서는 `<Routes />`로 바뀌었다.  

```react
// file: "Router.js"
// v5
<Switch>
  <Route path="/Login"... />;
  <Route path="/Main"... />;
</Switch>

// v6
<Routes>
  <Route path="/Login"... />;
  <Route path="/Main"... />;
</Routes>
```  

* 그리고 중요한 점은 `Switch`를 사용 할때는 `Route`를 감싸지 않아도 되었지만, v6 에서는  
무조건 `Routes` 로 감싸주어야 한다.  

## Route 에 자식 컴포넌트와 component 속성 삭제  
---  
```react
// file: "Router.js"
// v5
<Route path="/Login" component={Login} />;
//or
<Route path="/Main"/>
  <Login />
</Route>

// v6
<Route path="/Login" element={<Login />} />;
```  

## useHistory 도 잊자, useNavigate 를 기억할 것!
---  

* 기존의 페이지 이동위한 `useHistory` hook이 `useNavigate`로 대체 되었다.  

* 이전이 객체형이었다면 이번엔 함수형으로 바뀜  

```react
// file: "Router.js"
// v5
const history = useHistory();

onClick={()=>{history.push('/login')}}
onClick={()=>{history.goback()}}

// v6
onClick={()=>{navigate('/login')}}
onClick={()=>{navigate(-1)}}
```  

## 마무리  
---  

<br>  

[Router 공식문서]{:.note title="Link"}  

기본적이고 문법이 바뀌어 에러가 제일 많이 나오는 것들 몇개만 알아보았다.  
이외에도 중첩 라우팅, 상대경로 지정 등 바뀌거나 추가된 것이 많으니 공식문서를 참고하면 좋겠다.  

