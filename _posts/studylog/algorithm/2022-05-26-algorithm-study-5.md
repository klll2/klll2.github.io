---
layout: post
title: "ex [Inflearn #5] 10부제"
subtitle: "[Inflearn #5] 10부제 "
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

> 10부제
>
> 서울시는 6월 1일부터 교통 혼잡을 막기 위해서 자동차 10부제를 시행한다.  
> 자동차 10부제는 자동차 번호의 일의 자리 숫자와 날짜의 일의 자리 숫자가 일치하면  
> 해당 자동차의 운행을 금지하는 것이다.
>
> 예를 들어, 자동차 번호의 일의 자리 숫자가 7이면 7일, 17일, 27일에 운행하지 못한다.  
> 또한, 자동차 번호의 일의 자리 숫자가 0이면 10일, 20일, 30일에 운행하지 못한다.
>
> 여러분들은 일일 경찰관이 되어 10부제를 위반하는 자동차의 대수를 세는 봉사활동을 하려고 한다.  
> 날짜의 일의 자리 숫자가 주어지고 7대의 자동차 번호의 끝 두 자리 수가 주어졌을 때  
> 위반하는 자동차의 대수를 출력하는 프로그램을 작성하세요.

<br>

## 문제 예제

▣ 입력설명  
첫 줄에는 날짜의 일의 자리 숫자가 주어지고 두 번째 줄에는 7대의 자동차 번호의 끝 두 자 리 숫자가 주어진다.

▣ 출력설명  
주어진 날짜와 자동차의 일의 자리 숫자를 보고 10부제를 위반하는 차량의 대수를 출력합니다.

▣ 입력예제 1  
 day : 3  
 arr = [25 23 11 47 53 17 33]  
▣ 출력예제 1  
 3

▣ 입력예제 2  
 day : 0  
 arr = [12 20 54 30 87 91 30]  
▣ 출력예제 2  
 3

## 풀이

```js
// file: "solution.js"
function solution(day, arr) {
  let answer = 0;
  for (let x of arr) {
    if (x % 10 === day) answer++; // #1
  }
  return answer;
}
```

## 설명

1. for문을 배열만큼 돌리면서 10으로 나눈 나머지가 day와 같다면 answer을 한개씩 올린다.
   1. 어떠한 숫자를 10으로 나누면 무조건 한자리의 나머지만 남는다. 그것을 이용
