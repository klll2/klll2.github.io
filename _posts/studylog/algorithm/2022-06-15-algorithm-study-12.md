---
layout: post
title: "ex [Inflearn #12] K번째 큰 수"
subtitle: "[Inflearn #12] K번째 큰 수"
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

> K번째 큰 수
>
> 현수는 1부터 100사이의 자연수가 적힌 N장의 카드를 가지고 있습니다.  
> 같은 숫자의 카드가 여러장 있을 수 있습니다.  
> 현수는 이 중 3장을 뽑아 각 카드에 적힌 수를 합한 값을 기록하려고 합니다.  
> 3장을 뽑을 수 있는 모든 경우를 기록합니다.  
> 기록한 값 중 K번째로 큰 수를 출력 하는 프로그램을 작성하세요.  
> 만약 큰 수부터 만들어진 수가 25 25 23 23 22 20 19......이고  
> K값이 3이라면 K번째 큰 값 은 22입니다.

<br>

## 문제 예제

▣ 입력설명  
첫 줄에 자연수 N(3<=N<=100)과 K(1<=K<=50) 입력되고,  
그 다음 줄에 N개의 카드값이 입력 된다.

▣ 출력설명  
첫 줄에 K번째 수를 출력합니다. K번째 수는 반드시 존재합니다.

▣ 입력예제 1  
10 3  
13 15 34 23 45 65 33 11 26 42

▣ 출력예제 1  
143

## 풀이

```java
// file: "solution.js"
function solution(n, k, card) {
  let answer;
  let set = new Set();  // #1
  let cardSum = 0;
  let tempArry = [];
  for (i = 0; i < n; i++) {  // #2
    for (j = i + 1; j < n; j++) {
      for (s = j + 1; s < n; s++) {
        cardSum = card[i] + card[j] + card[s];  // #3
        set.add(cardSum);  // #4
        tempArry = Array.from(set).sort((a, b) => b - a);  // #5
      }
    }
    answer = tempArry[k - 1];  // #6
  }
  return answer;
}
```

## 설명

1. 답을 리턴시킬 answer, card 3장을 뽑았을때 합을 더할 변수 cardSum  
   카드들의 합을 모을 tempArry 그리고 중복되는 값을 없애기위해 set을 성정합니다.
2. 3장의 카드를 뽑을 수 있는 모든 수를 계산해야 하기에 반복문을 3개 만들어줍니다.  
   이미 뽑은 카드는 뽑지 않도록 반복문마다 시작점을 +1씩 해줍니다.
3. card를 3장씩 뽑아서 cardSum에 3장의 합계를 저장하고
4. 만들어준 set에 추가해줍니다.
5. Array 생성자로 set을 배열로 만들어서 tempArry에 저장한 후 내림차순 해줍니다.
6. 3장의 카드 합중 3번째로 큰값을 뽑아 리턴합니다.
