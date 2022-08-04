---
layout: post
title: "ex [Leetcode #14] Longest Common Prefix"
subtitle: "[Leetcode #14] Longest Common Prefix"
category: studylog
tags: algorithm
image:
  path: /assets/img/algorithm/algorithm.jpg
---

[leetcode #14 : longest common prefix]: https://leetcode.com/problems/longest-common-prefix/

<!--more-->

- this ordered seed list will be replaced by the toc
  {:toc}

[Leetcode #3 : Palindrome Number]
{:.note title="Link"}

# Longest Common Prefix

---

**알고리즘을 푸는 스타일은 사람마다 다 다르므로 이것 또한 저의 주관적인 풀이 입니다.**

## 문제 설명

> 문자열이 담긴 배열 중에 공통접두사가 있는 문자열을 찾는 함수를 작성하시오.  
> 공통 접두사가 없으면 빈문자열 "" 을 반환합니다.

**원문**

> Write a function to find the longest common prefix string amongst an array of strings.  
> If there is no common prefix, return an empty string "".

<br>  
## 예제

- Example 1:

```js
Input: strs = ["flower", "flow", "flight"];
Output: "fl";
```

- Example 2:

```js
Input: strs = ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

## 풀이

```js
// file: "solution.js"
var longestCommonPrefix = function (strs) {
  for (i = 0; i < strs[0].length; i++) {
    // #1
    if (!strs.every((e) => e[i] === strs[0][i])) {
      // #2
      return strs[0].slice(0, i); // #3
    }
  }
  return strs[0]; // #4
};
```

## 설명

1. 문자열이 담긴 strs 배열에서 비교군이 될 첫번째 요소를 기준(str[0]) 으로 반복문을 만듦
2. every 메서드 -> 배열 안의 모든 요소가 주어진 판별 함수를 통과하는지 Boolean 값으로 반환
   strs 배열의 모든 요소를 기준점인 strs[0]의 요소들과 비교하고 false 가 나온다면
   strs[0] 의 요소에서 첫 문자열부터 false가 나온지점까지 문자열을 잘라 반환
3. 위에서 반환했던 배열을 반환

## 회고

처음엔 `every` 메서드 대신 `for` 문을 이중으로 쓰고 `if` 문까지 써서 코드를 짰는데,  
많이 길어지지는 않았지만 그래도 조금 지저분해지는 게 있었다.

배열 메서드 중에 설정한 값과 같은지 비교해서 Boolean 값을 반환하는 메서드가 기억나서  
그것을 써보았다. 전보다는 어느 정도 깔끔해졌다.

하지만 더 짧고 간결하게 만드는 괴물들이 있겠지만, 이 정도도 만족!!
