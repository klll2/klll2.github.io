---
layout: post
title: "[HTML] 메타데이터 요소"
subtitle: "[HTML] 메타데이터 요소"
date: 2022-08-20 03:30
categories:
  - devlog
tag: [html, zerobase, frontend]
image:
  path: ../../../assets/img/htmllogo.png
---

# [HTML] 메타데이터 요소

## 메타데이터의 역할

💡 **메타데이터**

데이터를 설명하는 데이터, 데이터를 위한 데이터

검색엔진에서 분류할 때 메타데이터를 참조한다.

---

## title

💡 **title: 문서 제목 요소**

제목을 가리키는 요소

- 텍스트만 포함할 수 있으며 태그를 포함하더라도 무시한다.
- 페이지 제목은 SEO에 큰 영향을 준다.
    
    → 검색할 때의 정보 수집에 영향을 미친다. **title**의 중요성
    
    → 단순한 키워드의 나열은 피하자. 검색 알고리즘이 광고라고 판단하여 중요도 순위에서 미룬다.
    
```html
<title>This is title</title>
```

---

## meta

### 문서 정보

💡 **meta: 문서 레벨 메타데이터 요소**

**base**, **link**, **script**, **style**, **title** 과 같은 다른 메타관련 요소로 나타낼 수 없는 메타데이터를 나타낸다.

- **name**, **content** 속성을 사용할 수 있고, **name** 속성은 이름, **content** 속성은 값을 담당한다.
- **name** 속성은 사용할 수 있는 이름이 지정되어 있다.
    
    → 개인 프로젝트의 경우라면 상관이 없지만, 팀 프로젝트나 회사 내에서는 규칙을 지켜서 지정해야 한다.
    
- **application-name**: 웹 페이지에서 구동 중인 애플리케이션의 이름
- **author**: 문서 저작자
- **description**: 페이지에 대한 짧고 정확한 요약
- **generator**: 페이지를 생성한 소프트웨어의 식별자
- **keywords**: 페이지의 콘텐츠와 관련된, 쉼표로 구분한 키워드 목록. like 인스타그램 해시태그
- **referrer**: 문서에서 시작하는 요청의 HTTP Referer 헤더
    
    → 링크를 타고 넘어갈 때 어디서 왔는지 흔적을 남기는데 이에 대한 제어
    
```html
<meta name="" content="" />
```

### 문자 인코딩, 뷰포트

💡 **meta: 문서 레벨 메타데이터 요소**

- **charset**: 페이지의 문자 인코딩을 선언한다.
- **head**의 **첫 번째 정보**로 넣거나 **title 전**에 넣는 것을 권장한다.
- **viewport**: **meta** 태그의 **name** 속성에 넣어주고, 뷰포트의 초기 사이즈에 대한 힌트를 제공하며, 모바일 장치에서만 사용한다.
    - 여러 개를 사용하는 경우에는 쉼표(”**,**”)로 구분한다.
    - **width**, **height**, **initial-scale**, **maximum-scale**, **minimum-scale**, **user-scalable**(웹 페이지 확대 여부), **viewport-fit**이 존재한다.

```html
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

---

## link

💡 **link: 외부 리소스 연결 요소**

현재 문서와 외부 리소스의 관계를 명시한다.

- 스타일 시트를 연결할 때 제일 많이 사용하며, 이외에도 사이드 아이콘 연결 등 여러가지로 쓰일 수 있다.
- **href** 속성에 파일 경로를 입력하고, **rel** 속성에 어떠한 관계인지에 대해 입력한다.
- **rel** 속성에 기입할 수 있는 키워드는 지정되어 있는데 가장 많이 사용되는 키워드가 **stylesheet**이다.
    
    이외에도 **icon** 키워드도 많이 쓰인다.
    

```html
<link href="style/main.css" rel="stylesheet">
<link rel="icon" href="favicon.ico">
```

---

## MIME 타입

💡 **MIME 타입**

클라이언트에게 전송된 문서의 다양성을 알려주기 위한 매커니즘

- **HTML**에서는 **href** 속성에 명시된 경로를 통해 파일을 가져오지만, 어떠한 파일인지에 대해서는 알지 못한다. 이러한 때에 어떠한 타입인지에 대해 명시하는 것이 **MIME 타입**이라고 보면 된다.
- **일반적인 구조**: **type/subtype**
- **text**: 텍스트를 포함하는 모든 문서. **text/**~
- **image**: 모든 종류의 이미지. **image/**~
- **audio**: 모든 종류의 오디오 파일. **audio/**~
- **video**: 모든 종류의 비디오 파일. **video/**~
- **application**: 모든 종류의 이진 데이터. **application/**~

```html
<link href="style/main.css" rel="stylesheet" type="text/css">
```

---

## style

💡 **style: 스타일 정보 요소**

문서나 문서 일부에 대한 스타일 정보를 포함한다.

- **head** 태그 내부에 **style** 태그를 이용하여 스타일을 지정할 수 있지만, **link** 태그를 통해 외부 파일을 불러오는 것을 권장한다.
- 겹치는 속성이 존재하면 아래에 있는 코드가 적용된다.

```html
<!doctype html>
<html>
	<head>
		<style>
			p { color: red; }
		</style>
	</head>
	<body>
		<p>안녕하세요. 반갑습니다.</p>
	</body>
</html>
```

---

## script

💡 **script: 스크립트 요소**

데이터와 실행 가능한 코드를 문서에 포함할 때 사용하며 보통 **JavaScript** 코드와 함께 쓴다.

- **script** 요소를 통해 외부 스크립트를 가져올 수도 있고, **script** 요소 내부에 인라인 스크립트를 작성하는 것도 가능하다.
- **script**의 위치는 **head**에 있어도 되고, **body**에 위치해도 상관없다. 하지만, script 요소를 맞닥뜨리면 **script** 내부 코드를 먼저 해석하기 때문에 코드가 길다면 렌더링에 시간이 걸리기 때문에 가급적 **body**의 마지막 하단에 위치시키는 것을 권장한다!

```html
<!-- 외부에서 가져오기 -->
<script src="thisisjavascript.js"></script>

<!-- 내부에서 작성하기 -->
<script>
	alert("Hello World!");
</script>
```

---

## 관련 링크

- **head** : [https://developer.mozilla.org/ko/docs/Web/HTML/Element/head](https://developer.mozilla.org/ko/docs/Web/HTML/Element/head)
- **title** : [https://developer.mozilla.org/ko/docs/Web/HTML/Global_attributes/title](https://developer.mozilla.org/ko/docs/Web/HTML/Global_attributes/title)
- **meta** : [https://developer.mozilla.org/ko/docs/Web/HTML/Element/meta](https://developer.mozilla.org/ko/docs/Web/HTML/Element/meta)
- **link** : [https://developer.mozilla.org/ko/docs/Web/HTML/Element/link](https://developer.mozilla.org/ko/docs/Web/HTML/Element/link)
- **MIME 타입** : [https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types)
- **style** : [https://developer.mozilla.org/ko/docs/Web/HTML/Element/style](https://developer.mozilla.org/ko/docs/Web/HTML/Element/style)
- **script** : [https://developer.mozilla.org/ko/docs/Web/HTML/Element/script](https://developer.mozilla.org/ko/docs/Web/HTML/Element/script)