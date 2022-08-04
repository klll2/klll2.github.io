---
layout: post
title: "ex [Inflearn #9] 가장 짧은 문자거리"
subtitle: "[Inflearn #9] 가장 짧은 문자거리"
category: studylog
tags: algorithm
image:
  path: /assets/img/algorithm/algorithm.jpg
---

<!--more-->

[인프런 : js 알고리즘 문제풀이]: https://www.inflearn.com/course/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4

- this ordered seed list will be replaced by the toc
  {:toc}

[인프런 : JS 알고리즘 문제풀이]  
{:.note title="Link"}

**인프런 코테 대비 알고리즘 문제풀이를 정리해 놓은 것입니다.**

## 문제 설명

> 가장 짧은 문자거리
>
> 한 개의 문자열 s와 문자 t가 주어지면 문자열 s의 각 문자가 문자 t와 떨어진  
> 최소거리를 출력하는 프로그램을 작성하세요.

<br>

## 문제 예제

▣ 입력설명  
첫 번째 줄에 문자열 s와 문자 t가 주어진다.  
문자열과 문자는 소문자로만 주어집니다. 문자열의 길이는 100을 넘지 않는다.

▣ 출력설명  
첫 번째 줄에 각 문자열 s의 각 문자가 문자 t와 떨어진 거리를 순서대로 출력한다.

▣ 입력예제 1  
teachermode  
e

▣ 출력예제 1  
1 0 1 2 1 0 1 2 2 1 0

## 풀이

```java
// file: "solution.js"
function solution(s, t) {
  let answer = [];
  let count = 100;  // #1
  for (i = 0; i < s.length; i++) {  // #2
    if (s[i] === t) {
      count = 0;
    } else {
      count++;
    }
    answer.push(count);  // #3
  }
  count = 100;  // #4

  for (i = s.length - 1; i >= 0; i--) {  // #5
    if (s[i] === t) {
      count = 0;
    } else {
      count++;
    }
    answer[i] = Math.min(answer[i], count);  // #6
  }

  return answer;
}
```

## 설명

1. count는 초기에 얼마나 t와 떨어져있는지 모르니 100으로 설정
2. 반복문을 돌아 t이면 거리가 0이고 t와 떨어져 있는 만큼 count를 ++ 해준다.
3. 결과값을 answer에 push
4. 거꾸로 다시 반복문을 돌아서 비교해야하므로 count를 다시 100으로 세팅
5. 반대로 반복문을 돈다
6. t의 양쪽 문자 거리는 최소거리를 구해야하므로 기존의 answer의 있는 배열과
   비교하여 더 작은 값으로 교체해 준다.
