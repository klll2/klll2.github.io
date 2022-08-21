---
layout: post
title: "[HTML] 전역 속성"
subtitle: "[HTML] 전역 속성"
date: 2022-08-21 15:15
categories:
  - devlog
tag: [html, zerobase, frontend]
image:
  path: ../../../assets/img/htmllogo.png
---

# [HTML] 전역 속성

## class와 id

**class와 id는 식별자 역할을 한다.**

💡 **id**

문서 전체에서 고유식별자를 정의한다. → 문서 내에서 1개만 존재할 수 있다.

- 공백( )이 들어가면 안된다.
- 숫자나 특수문자(’**_**’, ‘**-**’, ‘**.**’ 제외)로 시작해선 안된다.

```html
<div>안녕하세요.</div>
<div>안녕하세요.</div>
<div id="hello">안녕하세요.</div>
<div>안녕하세요.</div>
<div>안녕하세요.</div>
```

💡 **class**

**id**와 다르게 중복이 가능하다. → 다수의 속성에 부여할 수 있다.

- 공백( )을 사용할 수 있다. → 하지만, 클래스명을 작성할 때가 아니라 다수의 **class**를 부여하기 위함이다.
- **id**와 마찬가지로 숫자나 특수문자(’**_**’, ‘**-**’, ‘**.**’ 제외)로 시작해선 안된다.

```html
<div class="hello">안녕하세요.</div>
<div class="hi">안녕하세요.</div>
<div>안녕하세요.</div>
<div class="hi hello">안녕하세요.</div>
<div>안녕하세요.</div>
```

---

## style

💡 **style**

**head**에서 사용하는 **style** 태그와는 다른 태그로 하나의 태그에만 스타일을 적용할 때 사용한다.

- 외부 스타일시트보다 우선적으로 스타일을 적용시킨다.
- 외부에서 CSS 파일을 끌어오는 것을 권장한다.

```html
<div style="background: ##ffe7e8; border: 2px solid #e66465;">
 <p style="margin: 15px; line-height: 1.5; text-align: center;">
  because there aren't wings
  human being finds the way to fly.
 </p>
</div>
```

---

## title

💡 **title**

**head**의 **title** 태그와는 관련 없는 요소로 추가적인 정보를 툴팁으로 제공해준다.

- **title** 속성에 값을 넣고, 해당 태그에 **onClick**하게 되면 **title** 속성값이 나온다.
- 공백( )이나 개행(엔터값)도 인식한다.
- 아래 코드와 같이 중복되는 부분이 존재한다면 가장 하위 자식의 **title** 값이 적용된다.

```html
<div title="바깥쪽 박스">
 <div title="첫번째 요소">안녕하세요.</div>
 <div>반갑습니다.</div>
</div>
```

---

## lang

💡 **lang**

컴퓨터에게 언어를 알려주는 charset 태그와 다르게 lang 태그는 유저에게 알려준다.

- 웹 접근성을 높이기 위한 수단이다.
- 어떠한 언어로 이루어져 있는지 명시해줌으로서 이에 알맞은 대응을 할 수 있게 된다.
- 상속이 가능하므로 하위 박스에도 적용된다.
- 물론 내부에 다른 언어가 존재할 경우 부분적으로 다른 언어를 적용할 수도 있다.

```html
<!DOCTYPE html>
<html lang="ko">
<head>
 <meta charset="UTF-8">
 <meta name="viewport" content="width=device-width, initial-scale=1.0">
 <title>Document</title>
</head>
<body>
 <div title="바깥쪽 박스" lang="ko">
  <div title="첫번째 요소">안녕하세요.</div>
  <div>반갑습니다.</div>
 </div>
</body>
</html>
```

---

## data

💡 **data**

**HTML**에 존재하는 속성이 아니라 사용자가 속성을 지정해줄 수 있다.

- **data-** 로 시작하는 속성은 HTML에 존재하는 속성이 아니다.
- **JavaScript**를 사용할 때 **HTML** 태그로부터 정보를 읽어서 가져오려고 할 때 활용한다.

```html
<article id="electriccars" data-columns="3" data-index-number="1234" data-parent="cars">
...
</article>
```

---

## draggable

💡 **draggable**

드래그 가능 여부를 명시한다.

- **boolean** 속성은 아니지만, **true** / **false** 로 명시해줘야 한다.
- **img** 태그의 경우, 기본값이 **auto**(**true** 처럼 드래그 가능) 주어져 있다.
- **JavaScript**를 사용할 때 클릭하거나 드래그하거나 할 때 이벤트 발생 조건으로 인식할 수 있기에 이를 제어한다.

```html
<img src="images/example.png" draggable="false">
```

---

## hidden

💡 **hidden**

시각적 방식 외에도 스크린 리더 등 다른 모든 방식에서 숨겨진다.

- **boolean** 값으로 작성하면 true, 작성하지 않으면 기본값으로 false로 적용된다.
- 개발자 도구에서 드러나므로 보안상의 목적으로 가리고자 할 때 사용하면 안된다.
- **hidden** 속성을 줌으로서 가린 태그를 **CSS** 속성으로 다시 드러내는 것도 있다. (**display** 속성 활용)

```html
<img src="images/example.png">
<img src="images/example.png" hidden>
```

---

## 관련 링크

- **id** : [https://developer.mozilla.org/ko/docs/Web/HTML/Element/head](https://developer.mozilla.org/ko/docs/Web/HTML/Global_attributes/id)
- **class** : [https://developer.mozilla.org/ko/docs/Web/HTML/Global_attributes/class](https://developer.mozilla.org/ko/docs/Web/HTML/Global_attributes/class)
- **style** : [https://developer.mozilla.org/ko/docs/Web/HTML/Global_attributes/style](https://developer.mozilla.org/ko/docs/Web/HTML/Global_attributes/style)
- **title** : [https://developer.mozilla.org/ko/docs/Web/HTML/Global_attributes/title](https://developer.mozilla.org/ko/docs/Web/HTML/Global_attributes/title)
- **lang** : [https://developer.mozilla.org/ko/docs/Web/HTML/Global_attributes/lang](https://developer.mozilla.org/ko/docs/Web/HTML/Global_attributes/lang)
- **data** : [https://developer.mozilla.org/ko/docs/Learn/HTML/Howto/Use_data_attributes](https://developer.mozilla.org/ko/docs/Learn/HTML/Howto/Use_data_attributes)
- **draggable** : [https://developer.mozilla.org/ko/docs/Web/HTML/Global_attributes/draggable](https://developer.mozilla.org/ko/docs/Web/HTML/Global_attributes/draggable)
- **hidden** : [https://developer.mozilla.org/ko/docs/Web/HTML/Global_attributes/hidden](https://developer.mozilla.org/ko/docs/Web/HTML/Global_attributes/hidden)