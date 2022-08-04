---
layout: post
title: "ex [Inflearn #7] 격자판 최대합"
subtitle: "[Inflearn #7] 격자판 최대합"
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

> 격자판 최대합
>
> 5*5 격자판에 아래롸 같이 숫자가 적혀있습니다.  
> N*N의 격자판이 주어지면 각 행의 합, 각 열의 합, 두 대각선의 합 중  
> 가 장 큰 합을 출력합니다.

![](https://images.velog.io/images/rladpwl0512/post/4c918d46-7cbb-4caa-8a25-a6b18feb8631/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-08-26%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.46.05.png){: width="50%" height="50%"}

<br>

## 문제 예제

▣ 입력설명  
첫 줄에 자연수 N이 주어진다.(1<=N<=50)  
두 번째 줄부터 N줄에 걸쳐 각 줄에 N개의 자연수가 주어진다.  
각 자연수는 100을 넘지 않는 다.

▣ 출력설명  
최대합을 출력합니다.

▣ 입력예제 1  
5  
10 13 10 12 15  
12 39 30 23 11  
11 25 50 53 15  
19 27 29 37 27  
19 13 30 13 19

▣ 출력예제 1  
155

## 풀이

```js
// file: "solution.js"
function solution(arr) {
  let answer = 0;
  let sum1 = 0; // #1
  let sum2 = 0;
  for (i = 0; i < arr.length; i++) {
    sum1 = 0;
    sum2 = 0;
    for (j = 0; j < arr.length; j++) {
      // #2
      sum1 += arr[i][j];
      sum2 += arr[j][i];
    }
    answer = Math.max(answer, sum1, sum2); // #3
  }
  sum1 = 0;
  sum2 = 0;

  for (i = 0; i < arr.length; i++) {
    // #4
    sum1 += arr[i][i];
    sum2 += arr[i][arr.length - i - 1];
  }

  answer = Math.max(answer, sum1, sum2); // #5

  return answer;
}
```

## 설명

1. 행과 열의 총 합을 저장하기 위한 변수를 설정한다.
2. 2중 반복문을 돌려서 행과 열의 합을 sum1과 sum2에 저장한다.
3. answer에 가장 큰 값을 저장한다.
4. 이번엔 대각선에 해당하는 반복문을 돌린다.
5. 대각선의 합과 기존의 answer의 합을 비교해서 저장한다. 결국엔 제일 큰 값만 저장된다.
