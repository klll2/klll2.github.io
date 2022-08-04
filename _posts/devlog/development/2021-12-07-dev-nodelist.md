---
layout: post
title: "ex [JavaScript] NodeList? HTMLCollection? 비슷한듯 다른 차이점"
subtitle: "[JavaScript] NodeList? HTMLCollection? 비슷한듯 다른 차이점"
category: devlog
tags: development javascript
image:
  path: /assets/img/jslogo.jpeg
---

초심자 입장에서 자바스크립트를 공부하다 보면 배열과 객체에 관련된 건 항상 헷갈리는 일이 많다.  
그중에 배열에 관련된 Method를 사용할 때면 적용이 안 되고, 에러를 내뿜는 일을 겪었을 것이다.

정확한 개념을 정리해놓은 곳은 인터넷에 널려있으니 이해할 수 있는 정도의 개념만 설명하겠다.  
초심자의 입장에서 이 포스팅을 본다면 어느 정도 궁금증은 해소되리라본다.

<!--more-->

1. this ordered seed list will be replaced by the toc
   {:toc}

## 유사배열

JavaScript에서 DOM 조작하기 위해 흔히 쓰는 Document 메소드 중 모든 요소를 가져오는  
메소드는 배열을 반환한다. 사실 반은 맞고 반은 틀리다. 아래는 우리가 흔히 쓰는 메소드이다.

```js
// file: "DOM.js"
const nodeList = document.querySelectorAll(".list");
const htmlCollection = document.getElementByClassName("list");
```

우리가 자주 쓰는 Documnet 메소드 nodeList(위), htmlCollector(아래)를 반환한다.  
{:.figcaption}

<br>
두 메소드 모두 HTML에서 해당하는 모든 요소를 가져오는 데 쓰인다. 그리고 그 모든 요소를 배열로  
반환하는데 정확하게 말하면 배열과 비슷한, 즉 **유사 배열** 을 반환한다.

<br>
정말 그런지 궁금하면 해당 변수를 `console.log` 로 찍어보자

<br>
![](https://images.velog.io/images/sunny_afterrain/post/a2776946-f424-404a-85bb-99776fbe2945/213.JPG)  
순서대로 NodeList, HTMLCollection, Array  
{:.figcaption}

NodeList 객체는 일반적으로 element.childNodes와 같은 속성과  
document.querySelectorAll 같은 메소드에 의해 반환되는 노드의 컬렉션입니다.
{:.note}

HTMLCollection 인터페이스는 요소의 문서 내 순서대로 정렬된 일반 컬렉션을 나타내며 리스트에서  
선택할 때 필요한 메서드와 속성을 제공합니다.  
{:.note}

## 유사배열의 차이

그렇다면 배열과 유사 배열은 무슨 차이일까?  
말그대로 유사한 배열이기때문에 배열에 적용할 수 있는 메소드가 제한된다.

- `NodeList 의 적용 가능한 메소드`

  - `entries()`
  - `forEach()`
  - `item()`
  - `keys()`
  - `values()`

- `HTMLCollection 의 적용 가능한 메소드`
  - `item()`

실제 배열에 적용가능한 메소드의 일부밖에 적용되지 않는걸 볼수 있다.  
지금도 초심자지만 불러들인 DOM요소가 왜 `forEach()` 가 안되는건지 한참 고생했는데  
이제 이해가 간다. 자세한 것은 [MDN] 공식문서를 참조바란다.

[mdn]: (https://developer.mozilla.org/ko/docs/Web/API/HTMLCollection)

> - **Live, Static Collection**  
>   대체로 _NodeList가_ Live Collection 으로 DOM 의 변경사항을 실시간으로 반영하지만  
>   `querySelectorAll` 으로 반환한 NodeList 는 Static Collection 이어서 실시간으로  
>   반영하지 않는다. 즉 중간에 `append` 로 DOM을 추가하는 함수가 있어도 반영되지 않는다.  
>   그에반해 _HTMLCollection_ 은 Live Collection 으로 문서의 변경사항이 실시간으로 반영된다.

## 일반 배열로 만들 순 없을까?

유사 배열이지만 배열의 모든 메소드를 사용하고싶다면? 아주 간단하다.  
`Array.from()` 을 사용 해 배열로 바꾸어 주면 된다.

```js
// file: "DOM.js"
const htmlCol = document.getElementByClassName("list");
htmlCollection.forEach(list => list.addEventListener("click", func);
// 사용 불가

Array.from(htmlCol).forEach(list => list.addEventListener("click", func);
// 사용 가능
```
