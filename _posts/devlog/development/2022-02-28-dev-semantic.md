---
layout: post
title: "ex [HTML] Semantic Web 과 Semantic Tag"
subtitle: "[HTML] Semantic Web 과 Semantic Tag"
category: devlog
tags: development html
image:
  path: /assets/img/htmllogo.jpg
---

[semantic - mdn]: https://developer.mozilla.org/ko/docs/Glossary/Semantics

요즘 HTML을 공부하다보면 '시멘틱 웹' '시멘틱 태그' 가 필수적으로 보인다.  
웹을 공부한다면 거의 꼭 알아두면 좋은 내용이므로 간단하게 정리하려한다.

> 시멘틱 웹은 W3C에 의해 세워진 기준으로 WWW의 확장판이다.

<!--more-->

1. this ordered seed list will be replaced by the toc
   {:toc}

# Semantic Web 이란?

---

인터넷이 활성화되고 현대에는 수많은 웹사이트가 존재한다.

내가 원하는 정보를 얻기 위하여 일일이 확인하면서 원하는 사이트에 접근하는 것은 불가능에 가깝다.  
그래서 우리는 검색엔진을 통해 정보를 찾고 검색엔진은 필요한 정보를 추출, 해석 가공하여 우리에게 전달한다.

이와 같이 검색엔진의 잘 검색할 수 있게 최적화를 내기 위해서 문서의 의미에 맞게 구성된 웹이 Semantic Web이다.  
<br>

# Semantic Tag

---

Semantic Tag는 HTML의 구조를 설계하는 데 있어 태그에 의미를 부여함으로써 사이트의 구조를  
브라우저와 개발자가 쉽게 파악할 수 있도록 도와주기 위해 만들어진 태그이다.

- non-semantic Tag : `div` , `span` -> 자신이 무엇인지 설명해주지 않는다.
- semantic Tag : `form` , `table` , `img` -> 자신이 어떤 요소인지 정확히 설명한다.

<br>

![semantic](/assets/img/develop/2022-02-28-develop/2022-02-28-develop.png){:.centered} Semantic Tag의 구조  
{:.figcaption}  
<br>

- **HEADER** : 웹페이지의 머리글, 제목, 헤더를 의미한다.
- **NAV** : 웹페이지의 목차, 리스트 등 네비게이션을 의미한다.
- **ASIDE** : 웹페이지에서 사이드의 공간을 의미한다.
- **SECTION** : 웹페이지에서 주제, 카테고리별로 섹션을 구분하는 용도로 쓰인다.
- **ARTICLE** : 웹페이지에서 본문, 주 내용의 페이지를 구성할떄 사용한다.
- **FOOTER** : 웹페이지에서 바닥글, 문서 하단에 들어가는 부분을 의미한다.

외에도 몇가지가 더 있으니 다음 MDN 공식 문서 링크를 참고하면 좋다.

[Semantic - MDN]
{:.note title="Link"}

# Semantic 요소를 고려하면 좋은점

---

웹페이지를 만들때 무작정 `div` 를 남발하며 사용하기보다는, 적절한 Semantic Tag를  
사용하는 것이 좋은데 그이유는 **웹 접근성** 과 **SEO(Searching Engine Optimiztion)** 때문이다.

- 장애를 가진 사람과 비장애인 모두 웹사이트를 이용할 수 있게 하는 방법이다.
  그림이나 사진등을 제공할때 눈으로 볼 수 없는 경우 그것을 대신해 소리로 알려줄 수 있는 텍스트로 제공해야 한다.
  그럴땐 의미없는 `div` 태그보다 Semantic Tag를 사용하면 음성정보나 문자로 해당 요소를 전달한다.

- 검색 사이트는 주기적으로 전 세계에 있는 웹을 수집하고 분석한다.
  시멘틱 요소는 검색엔진 최적화에도 많은 영향을 준다. 웹을 수집하는데 사람이 직접하지 않고 로봇을 통해  
  이루어 지는데 로봇이 해석 가능한 시멘틱 태그를 활용해야 정확한 내용전달이 가능하다.

**따라서 우리는 페이지의 내용을 잘 파악할 수 있도록 적절한 시멘틱 태그를 활용하여 웹페이지를 알맞게 구성해야한다.**

# 앞으로 HTML 마크업을 할 때에는?

---

말로만 하면 장황하지만 실제 사용할 때는 어렵지 않다.  
마크업을 할 때 의미 없는 div로만 묶는 것이 아니라 머리글, 메뉴, 본문 등 이처럼 의미가  
있는 것들끼리 묶으면 된다.

머리글은 `<header></header>`  
메뉴는 `<nav></nav>`  
본문은 `<main></main>` , `<section></section>` , `<article></article>`

이렇게 묶어서 제작하면 누가 보기에도 이 부분은 어떤 부분인지 알아볼 수 있고 유지 보수에도 용이하다.
