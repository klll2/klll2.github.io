---
layout: post
title: "[CSS] CSS 개요"
subtitle: "[CSS] CSS 개요"
date: 2022-08-23 13:00
categories:
  - devlog
tag: [css, zerobase, frontend]
image:
  path: ../../../assets/img/csslogo.png
---

# [CSS] CSS 개요

**CSS(Cascading Style Sheets)**

## CSS는 어떻게 생겼을까

```html
<h1>Welcome!</h1>
<ul>
	<li>Toy Story</li>
	<li>Zootopia</li>
	<li>Inside Out/li>
</ul>
```

- **CSS**는 룰 기반(**Rule-based**)의 언어이다.
- **CSS**를 통해 특정 요소, 혹은 특정 요소들의 집합의 스타일 규칙을 정의할 수 있다.

```html
h1 {
	color: red;
	font-size: 12px;
}
```

1. **선택자** (**Selector**): 스타일을 지정할 **HTML** 요소를 선택
2. **선언 블록** (**declaration block**): 중괄호 **{}** 내부의 여러 선언들을 작성
3. **선언** (**declaration**): 프로퍼티와 값으로 이루어진 쌍
4. **선택자 { 하나 이상의 선언 }** 의 형태로 이루어진 하나의 **Rule** (혹은 **Rule Set**)

**주석(Comments)**

→ **/* 내용 */** 의 형식으로 작성

---

## CSS를 적용하는 방법

1. 내부 스타일 (**embedded**)
2. 인라인 스타일 (**inline**)
3. 외부 스타일 (**external**)

### 1. 내부 스타일 (embedded)

```html
<!DOCTYPE html>
<html>
	<head>
		<style>
			h1 { 
				color: red; 
			}
		<style>
		<title>CSS</title>
	</head>
	<body>
		<h1>Welcome!</h1>
	</body>
</html>
```

### 2. 인라인 스타일 (inline)

```html
<body>
	<h1 style="color:red">Welcome!</h1>
</body>
```

→ 사용 지양

### 3. 외부 스타일 (external)

```html
<!DOCTYPE html>
<html>
	<head>
		<title>CSS</title>
		<link rel="stylesheet" href="style/main.css" />
	</head>
	<body>
		<h1>Welcome!</h1>
	</body>
</html>
```

---

## 캐스캐이딩 원칙

1. 스타일 **우선순위**
2. 스타일 **상속**

### 1. 스타일 우선순위

- 동일한 스타일이라도 **선언된 곳**에 따라 우선순위가 정해진다.
    - 브라우저에 의해 정의된 스타일 < 개발자가 선언한 스타일 < 사용자가 구성한 스타일

- 적용 범위가 적을 수록 우선시 된다.
    - **tag** 스타일 < **class** 스타일 < **id** 스타일 < 인라인 스타일
        
        → 인라인 스타일을 지양하는 이유
        
- 소스코드의 순서가 뒤에 있으면 덮어쓴다.

### 2. 스타일 상속

- 부모 요소에 있는 스타일 속성들이 자식 요소로 전달된다.
    - 자식 요소에서 재정의 할 경우, 부모의 스타일을 덮어쓴다.

- 상속이 되지 않는 속성도 있다. (예: 배경 이미지, 배경 색 등)

---

## MDN 활용하기

**키워드 + css + mdn 구글링**

**MDN 참고를 생활화하자!**

---

## 관련 링크

- **CSS** : [https://developer.mozilla.org/ko/docs/Web/CSS](https://developer.mozilla.org/ko/docs/Web/CSS)