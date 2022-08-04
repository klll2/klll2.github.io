---
layout: post
title: "ex [프로그래머스 #12922] 수박수박수박수박수박수?"
subtitle: "[프로그래머스 #12922] 수박수박수박수박수박수?"
category: studylog
tags: algorithm
image:
  path: /assets/img/algorithm/algorithm.jpg
---

[프로그래머스 #12922 : 수박수박수박수박수박수?]: https://programmers.co.kr/learn/courses/30/lessons/12922

<!--more-->

- this ordered seed list will be replaced by the toc
  {:toc}

[프로그래머스 #12922 : 수박수박수박수박수박수?]
{:.note title="Link"}

# 수박수박수박수박수박수?

---

**알고리즘을 푸는 스타일은 사람마다 다 다르므로 이것 또한 저의 주관적인 풀이 입니다.**

## 문제 설명

> 길이가 n이고, "수박수박수박수...."와 같은 패턴을 유지하는 문자열을 리턴하는 함수,
> solution을 완성하세요. 예를들어 n이 4이면 "수박수박"을 리턴하고 3이라면
> "수박수"를 리턴하면 됩니다.

## 제한 조건

> - n은 길이 10,000이하인 자연수입니다.

## 입출력 예

|  n  |   return   |
| :-: | :--------: |
|  3  |  "수박수"  |
|  4  | "수박수박" |

## 풀이 1

```js
// file: "solution.js"
function solution(n) {
  let result = "";
  for (let i = 1; i <= n; i++) {
    if (i % 2 === 0) {
      result += "박";
    } else {
      result += "수";
    }
  }
  return result;
}
```

## 설명

- result에 빈문자열을 변수에 담는다.
- 반복문을 사용하여 인자 n 만큼 반복하게 한다.
- `i % 2 === 0`으로 짝수면 `result`에 "박"을 담고 홀수면 "수"를 담는다.
- `result`를 리턴한다.

<br>

## 풀이 2

```js
// file: "solution.js"
function solution(n) {
  return "수박".repeat(n).substring(0, n);
}
```

## 설명

풀이 1보다 더 간략하게 만든 풀이이다.

- `repeat` 를 사용하여 인자 n 만큼 "수박"을 반복한다.
- `substring`을 사용 하여 지정된 문자 열까지만 반환한다.
  - (시작인덱스, 종료인덱스) substring(0, n) -> 0번 인덱스부터 n까지 반환
