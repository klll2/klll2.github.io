---
layout:   post
title:    "[Inflearn #1] 세 수 중 최소값 구하기"
subtitle: "[Inflearn #1] 세 수 중 최소값 구하기"
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
>세 수 중 최소값 구하기  
>  
>100이하의 자연수 A, B, C를 입력받아 세 수 중 가장 작은 값을 출력하는 프로그램을   작성하 세요.  
>(메소드를 사용하면 안됩니다)  



<br>  

## 문제 예제  

▣ 입력설명  
첫 번째 줄에 100이하의 세 자연수가 입력된다.  
▣ 출력설명  
첫 번째 줄에 가장 작은 수를 출력한다.  
▣ 입력예제 1 6 5 11  
▣ 출력예제 1 5  


## 풀이  

```js
// file: "solution.js"
  function solution(a, b, c) {
        let answer;
        if (a < b) answer = a; // #1
        else answer = b; 
        if (answer > c) answer = c; // #2

        return answer;
      }
```

## 설명  

1. a와 b를 비교해서 더 작은 값을 answer에 담아준다.  
2. answer와 나머지 c를 비교해서 더 작은 값을 담아준다.  


