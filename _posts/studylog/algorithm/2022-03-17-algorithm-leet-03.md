---
layout: post
title: "ex [Leetcode #9] Palindrome Number"
subtitle: "[Leetcode #9] Palindrome Number"
category: studylog
tags: algorithm
image:
  path: /assets/img/algorithm/algorithm.jpg
---

[leetcode #9 : palindrome number]: https://leetcode.com/problems/palindrome-number/

<!--more-->

- this ordered seed list will be replaced by the toc
  {:toc}

[Leetcode #3 : Palindrome Number]
{:.note title="Link"}

# Palindrome Number

---

**알고리즘을 푸는 스타일은 사람마다 다 다르므로 이것 또한 저의 주관적인 풀이 입니다.**

## 문제 설명

> 정수인 인자 x가 주어집니다. x가 회문이면 true를 반환하고,
> 정수가 앞에서 읽어도 거꾸로 읽어도 같으면 회문입니다.
> 예를들면 121은 거꾸로 읽어도 121이어서 회문이지만 123은 321이므로 회문이 아닙니다.

**원문**

> Given an integer x, return true if x is palindrome integer.  
> An integer is a palindrome when it reads the same backward as forward.  
> For example, 121 is a palindrome while 123 is not.

## 예제

- Example 1:

```js
Input: x = 121
Output: true
Explanation: 121 reads as 121 from left to right and from right to left.
```

- Example 2:

```js
Input: x = -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-.
Therefore it is not a palindrome.
```

- Example 3:

```js
Input: x = 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

## 풀이

```js
// file: "solution.js"
var isPalindrome = function (x) {
  const reverse = parseInt(x.toString().split("").reverse().join("")); // #1
  return x === reverse && true; // #2
};
```

## 설명

1. x는 정수이므로 거꾸로 변환해주기 위해 `toString()` 매소드로 문자열로 변환 ->  
   `split('')`으로 하나하나 쪼개 배열로 저장 -> `reverse()` 로 뒤집고 `join('')` 으로 붙이기  
   마지막으로 숫자형으로 다시 변환
2. x 인자와 변환된 변수가 같은지 비교후 같을때만 true 리턴

## 회고

비교적 쉬운문제 였지만 조금 애매한것이 이렇게 하면 - 가 뒤에 안붙고 사라지는거 같다.  
일단은 결과는 -가 있나 없나 잘나오지만 정확하지 않다는 면에서 다시 고민해봐야겠다.
