---
layout: post
title: "ex [Inflearn #15] 공주 구하기"
subtitle: "[Inflearn #15] 공주 구하기"
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

> 공주 구하기
>
> 정보 왕국의 이웃 나라 외동딸 공주가 숲속의 괴물에게 잡혀갔습니다.  
> 정보 왕국에는 왕자가 N명이 있는데 서로 공주를 구하러 가겠다고 합니다.  
> 정보왕국의 왕은 다음과 같은 방법으로 공주를 구하러 갈 왕자를 결정하기로 했습니다.  
> 왕은 왕자들을 나이 순으로 1번부터 N번까지 차례로 번호를 매긴다.  
> 그리고 1번 왕자부터 N 번 왕자까지 순서대로 시계 방향으로 돌아가며 동그랗게  
> 앉게 한다. 그리고 1번 왕자부터 시 계방향으로 돌아가며 1부터 시작하여 번호를  
> 외치게 한다. 한 왕자가 K(특정숫자)를 외치면 그 왕자는 공주를 구하러 가는데서  
> 제외되고 원 밖으로 나오게 된다. 그리고 다음 왕자부터 다시 1부터 시작하여  
> 번호를 외친다.  
> 이렇게 해서 마지막까지 남은 왕자가 공주를 구하러 갈 수 있다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FoYdpL%2FbtriUFryJlR%2FRhFiXGeieXEqEDv7xyuSxK%2Fimg.jpg)

> 예를 들어 총 8명의 왕자가 있고, 3을 외친 왕자가 제외된다고 하자.  
> 처음에는 3번 왕자가 3 을 외쳐 제외된다. 이어 6, 1, 5, 2, 8, 4번 왕자가  
> 차례대로 제외되고 마지막까지 남게 된 7 번 왕자에게 공주를 구하러갑니다.  
> N과 K가 주어질 때 공주를 구하러 갈 왕자의 번호를 출력하는 프로그램을 작성하시오.

<br>

## 문제 예제

▣ 입력설명  
첫 줄에 자연수 N(5<=N<=1,000)과 K(2<=K<=9)가 주어진다.

▣ 출력설명  
첫 줄에 마지막 남은 왕자의 번호를 출력합니다.

▣ 입력예제 1  
8 3

▣ 출력예제 1  
7

## 풀이

```java
// file: "solution.js"
function solution(n, k) {
  let answer;
  let queue = Array.from({ length: n }, (value, idx) => idx + 1);  // #1

  while (queue.length) {  // #2
    for (i = 1; i < k; i++) queue.push(queue.shift());  // #3
    queue.shift();  // #4
    if (queue.length === 1) answer = queue.shift();  // #5
  }
  return answer;
}
```

## 설명

1. queue를 변수로 유사객체의 배열을 만들어줍니다. idx를 이용하여 1부터 8까지의  
   왕자를 만들어 줍니다.
2. 조건이 false가 될 때까지 while 반복문을 돌립니다. queue.length가 0이 되면  
   멈춥니다. 0은 false 이기에
3. k만큼 반복문을 돌려주고 1부터 시작해 2까지는 큐를 하나씩 빼서 맨뒤로 넣어줍니다.
4. 다음 3번쨰의 왕자는 바로 빼서 제외해 줍니다.
5. 큐의 길이가 1이면 1명만 남은 것이기에 남은 왕자 한명을 빼서 answer에 넣습니다.
