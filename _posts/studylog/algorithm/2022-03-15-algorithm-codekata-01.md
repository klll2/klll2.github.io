---
layout: post
title: "ex [CodeKata #2] Reverse Integer"
subtitle: "[CodeKata #2] Reverse Integer"
category: studylog
tags: algorithm
image:
  path: /assets/img/algorithm/algorithm.jpg
---

<!--more-->

- this ordered seed list will be replaced by the toc
  {:toc}

# Reverse Integer

---

**알고리즘을 푸는 스타일은 사람마다 다 다르므로 이것 또한 저의 주관적인 풀이 입니다.**

## 문제 설명

> reverse 함수에 정수인 숫자를 인자로 받습니다. 그 숫자를 뒤집어서 return해주세요.

## 예제

- Example 1:

```js
Input: x = 1234;
Output: 4321;
```

- Example 2:

```js
Input: x = -1234;
Output: -4321;
```

- Example 3:

```js
Input: x = 1230;
Output: 321;
```

## 풀이

```js
// file: "solution.js"
const reverse = (x) => {
  const answer =
    parseInt(x.toString().split("").reverse().join("")) * Math.sign(x);
  return answer;
};
```

## 설명

1. 'x' 인자로 받은 숫자를 쪼개기 위해서 `toString()`으로 문자형으로 변환해준다.
   1. 왜냐하면 `split` 매서드는 String.prototype 이기때문
2. `split('')`으로 하나하나 쪼개서 배열로 만들어준다.
3. `reverse()`로 순서를 거꾸로 만든다.
4. `join('')`으로 쪼개것을 다 합쳐준다.
5. 다시 숫자형으로 되돌리기 위해 `parseInt()`로 감싸준다.
6. 그리고 다시 `Math.sign` 함수로 x 를 담아 기존의 값을 곱하고 값이 담긴 'answer' 변수를 반환

> **MDN 인용**  
> Math.sign() 함수는 주어진 수의 부호를 나타내는 +/-1을 반환합니다.  
> 단, Math.sign()에 제공한 수가 0일 경우 부호에 따라 +/-0을 반환합니다.  
> 즉 주어진 수가 양수면 1을 음수면 -1을 반환한다.
