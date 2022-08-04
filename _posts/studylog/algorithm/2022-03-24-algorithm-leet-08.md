---
layout:   post
title:    "[Leetcode #347] Top K Frequent Elements"
subtitle: "[Leetcode #347] Top K Frequent Elements"
category: studylog
tags:     algorithm
image:
  path:    /assets/img/algorithm/algorithm.jpg
---

[Leetcode #347 : Top K Frequent Elements]:https://leetcode.com/problems/top-k-frequent-elements/

<!--more-->
* this ordered seed list will be replaced by the toc
{:toc}  

[Leetcode #347 : Top K Frequent Elements]
{:.note title="Link"}  

# Majority Element  
---  
__알고리즘을 푸는 스타일은 사람마다 다 다르므로 이것 또한 저의 주관적인 풀이 입니다.__  

## 문제 설명  
>숫자가 남긴 배열 nums와 숫자 k 가 주어진다.
>같은숫자가 많은 순서대로 k 만큼 리턴하라.

__원문__
>Given an integer array nums and an integer k,  
>return the k most frequent elements. You may return the answer in any order.  

<br>  
## 예제  

* Example 1:
```js
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```  

* Example 2:
```js
Input: nums = [1], k = 1
Output: [1]
```  


## 풀이  

```js
// file : "solution.js"
var topKFrequent = function(nums, k) {
  const map = new Map() // #1
  for(n of nums){
    map.set(n, map.get(n)+1 || 1) // #2
  } 
    return [...map].sort((a,b)=>b[1]-a[1]).map(el=>el[0]).slice(0,k) // #3
};
```

## 설명  

1. map의 변수에 Map()을 선언 해 준다.  
2. map에 키값으로 n을 대입하고 밸류값으로 n이 존재하면 +1 해주고 없으면 1을 선언 해 준다.  
3. 스프레드 연산자로 map을 배열로 만들어 준 후 밸류값을 기준으로 내림차순으로 바꾸어 준다.  
그 후 키 값만 걸러내기위해 map 배열 함수로 key값만 뽑아 낸후 인덱스 0부터 k만큼 잘라준다.  


## 회고  

이전에 map을 사용한 적이 있어서 바로 map이 생각났다. 객체를 잘 사용할 줄 알아야하는데  
자꾸 다른 메소드를 쓰는거 같아 좀 그렇지만 ㅠㅠㅠㅠㅠ  
map의 메소드인 entries(), keys(), value()를 쓰고싶은데 잘 적용하지 못하였다ㅠㅠ  
알고리즘은 이처럼 풀기 쉬운게 나오면 재미있는데....... 계속 어렵겠지..  