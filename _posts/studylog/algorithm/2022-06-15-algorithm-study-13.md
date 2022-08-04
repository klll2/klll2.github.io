---
layout:   post
title:    "[Inflearn #13] 최대 매출"
subtitle: "[Inflearn #13] 최대 매출"
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

>최대 매출  
>
>현수의 아빠는 제과점을 운영합니다.  
>현수 아빠는 현수에게 N일 동안의 매출기록을 주고 연속 된 K일 동안의 최대  
>매출액이 얼마인지 구하라고 했습니다.  
>만약 N=10이고 10일 간의 매출기록이 아래와 같습니다.  
>이때 K=3이면 12 15 **11 20 25** 10 20 19 13 15  
>연속된 3일간의 최대 매출액은 11+20+25=56만원입니다. 여러분이 현수를 도와주세요.  



<br>  

## 문제 예제  

▣ 입력설명  
첫 줄에 N(5<=N<=100,000)과 M(2<=K<=N)가 주어집니다.  
두 번째 줄에 N개의 숫자열이 주어집니다. 각 숫자는 500이하의 음이 아닌 정수입니다.  

▣ 출력설명  
첫 줄에 최대 매출액을 출력합니다.  


▣ 입력예제 1  
10 3  
12 15 11 20 25 10 20 19 13 15  


▣ 출력예제 1  
56  




## 풀이  

```java
// file: "solution.js"
function solution(k, arr) {
  let answer = 0;  // #1
  let sum = 0;
  for (let i = 0; i < k; i++) sum += arr[i];  // #2
  answer = sum;
  for (let i = k; i < arr.length; i++) {  // #3
    sum += arr[i] - arr[i - k];  // #4
    answer = Math.max(answer, sum);  // #5
  }

  return answer;
}
```

## 설명  

1. 답을 리턴시킬 answer, 연속 k일의 매출액을 더할 sum 변수를 선언해줍니다.  
2. 우선 제일 첫번째 연속 k일간의 매출기록을 구해줍니다.  
3. 모든 매출기록을 반복문으로 돌려줍니다. 여기서 이미 첫 3일 매출기록은  
이미 구했기 때문에 시작값을 k로 해줍니다.  
4. 다음 하루 더하고 맨 첫날 하루 빼주고 하는식으로 옆으로 한칸씩 슬라이드하여  
매출기록을 구하고  
5. 기존의 answer와 비교하여 더 큰값을 구합니다.  