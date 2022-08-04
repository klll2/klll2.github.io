---
layout: post
title: "ex [Leetcode #537] Complex Number Multiplication"
subtitle: "[Leetcode #537] Complex Number Multiplication"
category: studylog
tags: algorithm
image:
  path: /assets/img/algorithm/algorithm.jpg
---

[leetcode #537 : complex number multiplication]: https://leetcode.com/problems/complex-number-multiplication/

<!--more-->

- this ordered seed list will be replaced by the toc
  {:toc}

[Leetcode #537 : Complex Number Multiplication]
{:.note title="Link"}

# Majority Element

---

**알고리즘을 푸는 스타일은 사람마다 다 다르므로 이것 또한 저의 주관적인 풀이 입니다.**

## 문제 설명

> 두 개의 input에는 복소수(complex number)가 string 으로 주어집니다.
> 복소수란 a+bi 의 형태로, 실수와 허수로 이루어진 수입니다.
> input으로 받은 두 수를 곱해서 반환해주세요.
> 반환하는 표현도 복소수 형태의 string 이어야 합니다.
> 복소수 정의에 의하면 (i^2)는 -1 이므로 (i^2) 일때는 -1로 계산해주세요.

**원문**

> A complex number can be represented as a string on the form "real+imaginaryi" where:
> real is the real part and is an integer in the range [-100, 100].
> imaginary is the imaginary part and is an integer in the range [-100, 100].
> i2 == -1.
> Given two complex numbers num1 and num2 as strings, return a string of the >complex number that represents their multiplications.

<br>  
## 예제

- Example 1:

```js
Input: num1 = "1+1i", num2 = "1+1i"
Output: "0+2i"
Explanation: (1 + i) * (1 + i) = 1 + i2 + 2 * i = 2i, and you need convert it to the form of 0+2i.
```

- Example 2:

```js
Input: num1 = "1+-1i", num2 = "1+-1i"
Output: "0+-2i"
Explanation: (1 - i) * (1 - i) = 1 + i2 - 2 * i = -2i, and you need convert it to the form of 0+-2i.
```

## 풀이

```js
// file: "solution.js"
var complexNumberMultiply = function (num1, num2) {
  const i = [];
  const j = [];
  i[0] = num1.split("+")[0]; // #1
  i[1] = num1.split("+")[1].split("i")[0];
  j[0] = num2.split("+")[0]; // #2
  j[1] = num2.split("+")[1].split("i")[0];

  return `${i[0] * j[0] - i[1] * j[1]}+${i[1] * j[0] + i[0] * j[1]}i`; // #3
};
```

## 설명

1. 주어진 복소수의 '+' 와 'i' 를 제거하고 각각 배열에 담아준다.
2. 두번째 인자도 마찬가지로 제거한다.
3. 복소수 계산방식에 맞추어 각각의 수를 곱한값을 한쪽은 더해주고 다른 한쪽은 빼준다.

## 회고

복소수라는 것 자체를 이해를 못하니 또 접근 하는방법조차 몰랐던 문제였다.  
여러 검색을 병행했고 푸는방식은 이해했지만, 복소수라는것은 아직도 이해가 잘 가지 않는다.  
수학을 잘했으면 풀기 쉬웠을 문제
