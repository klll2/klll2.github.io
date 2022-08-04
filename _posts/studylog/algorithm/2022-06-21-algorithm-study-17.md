---
layout: post
title: "ex [Inflearn #16] 교육과정 설계"
subtitle: "[Inflearn #16] 교육과정 설계"
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

> 교육과정 설계
>
> 현수는 1년 과정의 수업계획을 짜야 합니다.  
> 수업중에는 필수과목이 있습니다. 이 필수과목은 반드시 이수해야 하며,  
> 그 순서도 정해져 있 습니다.  
> 만약 총 과목이 A, B, C, D, E, F, G가 있고, 여기서 필수과목이 CBA로  
> 주어지면 필수과목은 C, B, A과목이며 이 순서대로 꼭 수업계획을 짜야 합니다.  
> 여기서 순서란 B과목은 C과목을 이수한 후에 들어야 하고, A과목은 C와 B를  
> 이수한 후에 들 어야 한다는 것입니다.
> 현수가 C, B, D, A, G, E로 수업계획을 짜면 제대로 된 설계이지만  
> C, G, E, A, D, B 순서로 짰다면 잘 못 설계된 수업계획이 됩니다.  
> 수업계획은 그 순서대로 앞에 수업이 이수되면 다음 수업을 시작하다는 것으로  
> 해석합니다. 수업계획서상의 각 과목은 무조건 이수된다고 가정합니다.  
> 필수과목순서가 주어지면 현수가 짠 N개의 수업설계가 잘된 것이면 “YES",  
> 잘못된 것이면 ”NO“를 출력하는 프로그램을 작성하세요.

<br>

## 문제 예제

▣ 입력설명  
첫 줄에 한 줄에 필수과목의 순서가 주어집니다. 모든 과목은 영문 대문자입니다.  
두 번 째 줄부터 현수가 짠 수업설계가 주어집니다.(수업설계의 길이는 30이하이다)

▣ 출력설명  
수업설계가 잘된 것이면 “YES", 잘못된 것이면 ”NO“를 출력합니다.

▣ 입력예제 1  
CBA  
CBDAGE

▣ 출력예제 1  
YES

## 풀이

```java
// file: "solution.js"
function solution(need, plan) {
  let answer = 'YES';  // #1
  let queue = need.split('');  // #2
  for (x of plan) {  // #3
    if (queue.includes(x)) {  // #4
      if (x !== queue.shift()) return 'NO';  // #4
    }
  }
  if (queue.length > 0) return 'NO';  // #5
  return answer;
}
```

## 설명

1. 기본적으로 'YES'라는 답이 나오게 answer 변수에 설정해줍니다.
2. 필수과목을 `split()` 함수를 써서 문자열에서 배열로 만들어 줍니다.
3. 수업설계를 반복문을 돌려줍니다.
4. 필수과목안에 수업설계를 하나씩 돌면서 수업이 존재할때 필수과목을 `shift()` 해서  
   두개의 값이 같은지 확인하고 아니라면 "NO"를 리턴해줍니다.  
   `shift()` 한값과 반복문을 돌린 값이 다르면 우선적으로 설계해야하는것과 다르므로
5. 모든반복문을 돌았는데 필수과목 queue에 수업이 남아있다면 "NO"를 리턴합니다.
