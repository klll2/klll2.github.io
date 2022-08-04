---
layout:   post
title:    "[Inflearn #4] 1부터 N까지 합 출력하기"
subtitle: "[Inflearn #4] 1부터 N까지 합 출력하기"
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

>1부터 N까지 합 출력하기  
>
>자연수 N이 입력되면 1부터 N까지의 합을 출력하는 프로그램을 작성하세요.  



<br>  

## 문제 예제  

자연수 N이 입력되면 1부터 N까지의 합을 출력하는 프로그램을 작성하세요.

▣ 입력설명  
첫 번째 줄에 20이하의 자연수 N이 입력된다..  

▣ 출력설명  
첫 번째 줄에 1부터 N까지의 합을 출력한다.  

▣ 입력예제 1  
 6
▣ 출력예제 1  
 21

▣ 입력예제 2  
 10
▣ 출력예제 2  
 55


## 풀이  

```js
// file: "solution.js"
function solution(n) {
  let answer = 0;
  for (i = 0; i <= n; i++) { // #1
    answer += i;  // #2
  }
  return answer;
}
```

## 설명  

1. n만큼 반복문을 만들어준다.  
2. 1부터 n만큼을 다 더해주고 리턴!  
