---
layout:   post
title:    "[Inflearn #3] 연필 개수"
subtitle: "[Inflearn #3] 연필 개수"
category: studylog
tags:     algorithm
image:
  path:    /assets/img/algorithm/algorithm.jpg
---

<!--more-->

[인프런 : JS 알고리즘 문제풀이]:https://www.inflearn.com/course/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4

* this ordered seed list will be replaced by the toc
{:toc}  

[인프런 : JS 알고리즘 문제풀이]  
{:.note title="Link"}  

__인프런 코테 대비 알고리즘 문제풀이를 정리해 놓은 것입니다.__  

## 문제 설명  

>연필 개수
>
>연필 1 다스는 12자루입니다.   
>학생 1인당 연필을 1자루씩 나누어 준다고 할 때 N명이 학생수 를 입력하면  
>필요한 연필의 다스 수를 계산하는 프로그램을 작성하세요.  



<br>  

## 문제 예제  

* 입력설명  
첫 번째 줄에 1000 이하의 자연수 N이 입력된다.  

* 출력설명  
첫 번째 줄에 필요한 다스 수를 출력합니다.  

* 입력예제 1  
25  
* 출력예제 1  
3  

* 입력예제 2  
178  
* 출력예제 2  
15  


## 풀이  

```js
// file: "solution.js"
function solution(n) {
  let answer;
  answer = n / 12;
  return Math.ceil(answer);
}
```

## 설명  

1. 학생수 / 12(연필 한다스)를 해준다.  
2. 소숫점 부분을 반올림 해주면 학생수에 대한 필요한 연필다스 수가 나온다.  
