---
layout: post
title: '[React] 라우터 페이지 이동시 스크롤 맨 위로 이동하는 방법'
subtitle: '[React] 라우터 페이지 이동시 스크롤 맨 위로 이동하는 방법'
category: devlog
tags: tips react
image:
  path:    /assets/img/tips/2022-03-15-react-router/2022-03-15-router.svg
---

리액트 라우터로 라우팅하여 페이를 이동할때 페이지가 이미 밑에 있는 상태에서  
라우팅을 하면 이전 스크롤의 위치에서 그대로 라우팅이 되어 다시 스크롤이 맨위로 가지않는  
현상이 일어났다. 구글링을 해보니 라우터문서에도 나온 해결법이 있어서 공유한다.  

<!-- more -->

* this ordered seed list will be replaced by the toc
{:toc}  

## 컴포넌트를 하나 만들자!  
---  
root에 컴포넌트를 다음과 같은 내용으로 만들어 놓자. 
```js
// file: "ScrollToTop.js"
import { useEffect } from "react";
import { useLocation } from "react-router-dom";

export default function ScrollToTop() {
  const { pathname } = useLocation();

  useEffect(() => {
    window.scrollTo(0, 0);
  }, [pathname]);

  return null;
}
```

## 최상위 컴포넌트에 다음과 같이 묶어주자  
---  
예시는 `index.js`에 적용하였지만 라우터를 다른곳에 적용하였으면 그곳에 적용해준다.  
중요한것은 `Router`를 선언한 곳 밑에 넣어주어야 한다는 것이다.  

```js  
// file: "index.js"
ReactDOM.render(
  <BrowserRouter>
  <ScrollTop />
    <App />
  </BrowserRouter>,
  document.getElementById('root')
);
```  


## 테스트 해보자  
---  

다 하고 나서 한번 테스트 해보자. 페이지를 이동할때 마다 스크롤이 최상단으로 위치 한다.