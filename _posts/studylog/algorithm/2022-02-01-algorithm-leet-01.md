---
layout: post
title: "ex [Leetcode #1] Two Sum"
subtitle: "[Leetcode #1] Two Sum"
category: studylog
tags: algorithm
image:
  path: /assets/img/algorithm/algorithm.jpg
---

[leetcode #1 : two sum]: https://leetcode.com/problems/two-sum/

<!--more-->

- this ordered seed list will be replaced by the toc
  {:toc}

[Leetcode #1 : Two Sum]
{:.note title="Link"}

# Two Sum

---

**알고리즘을 푸는 스타일은 사람마다 다 다르므로 이것 또한 저의 주관적인 풀이 입니다.**

## 문제 설명

> 정수인 배열 num 과 정수인 숫자 target 이 인자로 주어집니다.  
> num 배열의 두 숫자 인덱스를 더하여 target 을 반환해야합니다.

**원문**

> Given an array of integers nums and an integer target,  
> return indices of the two numbers such that they add up to target.

## 예제

- Example 1:

```js
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

- Example 2:

```js
Input: (nums = [3, 2, 4]), (target = 6);
Output: [1, 2];
```

- Example 3:

```js
Input: (nums = [3, 3]), (target = 6);
Output: [0, 1];
```

## 풀이

```js
// file: "solution.js"
var twoSum = function (nums, target) {
  for (i = 0; i < nums.length; i++) {
    for (j = i + 1; j < nums.length; j++) {
      if (nums[i] + nums[j] === target) return [i, j];
    }
  }
};
```

## 설명

- for 문 두개를 사용하여 두개중 하나는 i+1을 하여 반복문을 돈다.
- 두개의 다른 for문이 배열의 인덱스를 돌며 값을 더한 후 target과 비교
- target과 같은 값이 나오는 배열 인덱스를 반환한다.

---

## 다른 풀이 방법

```js
// file: "Another-solution.js"
function twoSum(nums, target) {
  let numObj = {};
  for (let i = 0; i < nums.length; i++) {
    let complement = target - nums[i];
    if (numObj[complement] !== undefined) {
      return [numObj[complement], i];
    }
    numObj[nums[i]] = i;
  }
}
```

> 인터넷에 다른 외국인분이 푸신 문제
> 객체를 사용하여 풀었다. 어렵다.

- 빈오브젝트를 만들어서 변수에 numObj 넣어준다.
- 반복문을 배열의 길이만큼 돌아준다.
- target 값에 num[i] 를 빼준 값을 complement 변수에 담아준다.
- numObj 객체의 위에서 저장한 complement 의 값이 없다면 생략하여  
  첫번째 키값을 가진 numObj 객체에 i번째 밸류값을 넣어준다.
- 이렇게 돌다가 해당 키값에 대한 밸류가 존재 한다면 해당 키값이 가지고 있는 밸류값과
  인덱스를 리턴한다.

> 너무 어렵다 ㅠㅠ
