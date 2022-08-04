---
layout: post
title: "ex [CSS] Position: Sticky 가 잘 안될때"
subtitle: "[CSS] Position: Sticky 가 잘 안될때"
category: devlog
tags: tips css
image:
  path: /assets/img/csslogo.jpg
---

[mdn 공식문서 - CSS Position]{:.note title="Link"}

HTML을 마크업하고 CSS를 적용할 때 상단 NAV 메뉴바를 만들었고 스크롤을 내리면  
내가 원하는 위치에서 멈추게 하고 싶을 때가 있다. 자바스크립트로도 구현이 가능하지만,  
아주 간단하게 CSS로도 구현할 수 있다. 바로 `Sticky` 속성이다.

[mdn 공식문서 - css position]: https://developer.mozilla.org/ko/docs/Web/CSS/position

<!-- more -->

1. this ordered seed list will be replaced by the toc
   {:toc}

## 들어가기에 앞서

Sticky 속성이란 원하는 위치의 고정 위치 값을 정해주면 해당 위치에서 자동으로 `fixed`를 해주는  
아주 멋진 놈이다. 기본적으로 `postion: fixed` 와 같다고 볼 수 있다.  
간단히 구현하기 위해 아래와 같이 마크업과 CSS 속성을 주었다.

```html
<!-- file: "index.html"   -->
<body>
  <div class="ul-sticky">
    <div class="ul-sticky__list">
      <ul>
        <li>Home</li>
        <li>About me</li>
        <li>Favorite</li>
        <li>Contact</li>
      </ul>
    </div>
  </div>
</body>
```

```css
/* file: "style-sticky.css" */
.ul-sticky__list {
  position: sticky;
  top: 0px;
}
```

## 발생한 문제점

최상단에 고정하고 싶어 `top: 0px;` 속성을 줘봐도 다른 값으로 아무리 줘봐도 작동이 안 됐다.

![](https://user-images.githubusercontent.com/95746551/151108838-658d0805-a00f-4210-b0fe-b3bf69b6652f.gif){: width="80%" height="80%"}{:.centered}다음과 같이 노란색의 메뉴가 고정이 안된다.  
{:.figcaption}

해결을 위해 구글링을 한 결과 Sticky를 적용 할 태그의 부모태그에는 무조건 `height` 설정이 있어야  
한다는 것을 찾았다. 그래서 상위 부모 태그에 height 를 주었다.

```css
/* file: "style-sticky.css" */
.ul-sticky {
  height: 500px;
}
.ul-sticky__list {
  position: sticky;
  top: 0px;
}
```

이렇게 했더니 됐다! 그런데 이렇게 해도 문제가 있었다.

![](https://user-images.githubusercontent.com/95746551/151110218-7d393ee8-c3af-40a6-9c58-c8f03b636a4e.gif){: width="80%" height="80%"}{:.centered}부모 태그에 높이 값을 준 만큼만 고정되고 이후에는 또 적용이 안된다.  
{:.figcaption}

## 최종 해결책

`Sticky` 를 사용하려면 무조건 부모태그에 높이 값이 있어야 한다고 했었다. 그렇다면?  
마크업한 컨텐츠만큼 자동으로 높이속성이 결정되는 `<body>` 태그가 생각났다.  
그래서 `Sticky` 를 사용해야 한다면 그 부분의 마크업만 똑 떼어내서 `<body>` 태그의  
바로 하위에서 마크업을 하고 CSS에서 `Sticky` 를 적용하자.

```html
<!-- file: "index.html" -->
<body>
  <div class="ul-sticky">
    <div class="ul-sticky__list">
      <ul>
        <li>Home</li>
        <li>About me</li>
        <li>Favorite</li>
        <li>Contact</li>
      </ul>
    </div>
  </div>
</body>
```

```css
/* file: "style-sticky.css" */
.ul-sticky {
  position: sticky;
  top: 0px;
}
```

이전에는 `<body>` 태그의 두단계 자식인 `.ul-sticky-list` 클래스에 적용을 했지만,  
이번에는 바로 밑 자식은 `.ul-sticky` 클래스에 적용을 하였다.

![](https://user-images.githubusercontent.com/95746551/151111081-7c7bbb82-5b6f-4793-8627-0a814c133678.gif){: width="80%" height="80%"}{:.centered}아주아주 잘되는 모습이다.  
{:.figcaption}
