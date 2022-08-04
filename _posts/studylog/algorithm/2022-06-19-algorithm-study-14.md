---
layout: post
title: "ex [Inflearn #14] 괄호문자 제거"
subtitle: "[Inflearn #14] 괄호문자 제거"
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

> 괄호문자 제거
>
> 입력된 문자열에서 소괄호 ( ) 사이에 존재하는 모든 문자를 제거하고  
> 남은 문자만 출력하는 프로그램을 작성하세요.

<br>

## 문제 예제

▣ 입력설명  
첫 줄에 문자열이 주어진다. 문자열의 길이는 100을 넘지 않는다.

▣ 출력설명  
남은 문자만 출력한다.

▣ 입력예제 1  
(A(BC)D)EF(G(H)(IJ)K)LM(N)

▣ 출력예제 1  
EFLM

## 풀이

```java
// file: "solution.js"
function solution(s) {
  let answer;
  let stack = [];  // #1
  for (x of s) {  // #2
    if (x === ')') {  // #3
      while (stack.pop() !== '(');  // #4
    } else stack.push(x);  // #5
  }
  answer = stack.join('');  // #6
  return answer;
}
```

## 설명

1. 스택을 넣어줄 빈 배열을 생성합니다.
2. 매개변수로 들어온 문자열 s 를 `for of` 를 사용해 반복문을 돌립니다.
3. 문자열에서 ')' 를 만나면
4. '(' 를 만날때 까지 배열을 하나씩 `pop()` 해줍니다.  
   그렇게되면 '()' 사이의 문자열이 다 삭제 될 것입니다.
5. '(' 가 아니라면 스택에 다 넣어 줍니다. (괄호와 문자열 다)
6. 지워지지 않고 남은 스택을 `join()` 하여 리턴 합니다.
