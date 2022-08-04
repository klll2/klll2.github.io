---
layout:   post
title:    "[프로그래머스 #12919] 서울에서 김서방 찾기"
subtitle: "[프로그래머스 #12919] 서울에서 김서방 찾기"
category: studylog
tags:     algorithm
image:
  path:    /assets/img/algorithm/algorithm.jpg
---
[프로그래머스 #12919 : 서울에서 김서방 찾기]:https://programmers.co.kr/learn/courses/30/lessons/12919
<!--more-->
* this ordered seed list will be replaced by the toc
{:toc}  

[프로그래머스 #12919 : 서울에서 김서방 찾기]
{:.note title="Link"}  
# 서울에서 김서방 찾기
---  
__알고리즘을 푸는 스타일은 사람마다 다 다르므로 이것 또한 저의 주관적인 풀이 입니다.__
## 문제 설명
> String형 배열 seoul의 element중 "Kim"의 위치 x를 찾아,  
> "김서방은 x에 있다"는 String을 반환하는 함수, solution을 완성하세요.  
> seoul에 "Kim"은 오직 한 번만 나타나며 잘못된 값이 입력되는 경우는 없습니다.  


## 제한사항
>* seoul은 길이 1 이상, 1000 이하인 배열입니다.  
>* seoul의 원소는 길이 1 이상, 20 이하인 문자열입니다.  
>* "Kim"은 반드시 seoul 안에 포함되어 있습니다.

## 입출력 예  

| seoul |    return     |
| :-------: | :---------: |
| ["Jane", "Kim"] | "김서방은 1에 있다" |

## 풀이  

```js
// file: "solution.js"  
function solution(seoul) {
    var answer = `김서방은 ${seoul.indexOf("Kim")}에 있다`
    return answer;
}
```  

## 설명  

* `indexOf()` 는 객체에서 주어진 값과 일치하는 첫 번째 인덱스를 반환한다.  
* seoul 이라는 배열 안에 "Kim" 이라는 문자열의 인덱스를 찾으면 된다.
   * `seoul.indexOf("Kim")`  
* 배열 seoul 안에 "Kim" 인덱스는 1이니 "김서방은 1에 있다" 라고 출력된다.