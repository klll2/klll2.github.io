---
layout:   post
title:    "[Leetcode #169] Majority Element"
subtitle: "[Leetcode #169] Majority Element"
category: studylog
tags:     algorithm
image:
  path:    /assets/img/algorithm/algorithm.jpg
---

[Leetcode #169 : Majority Element]:https://leetcode.com/problems/majority-element/

<!--more-->
* this ordered seed list will be replaced by the toc
{:toc}  

[Leetcode #169 : Majority Element]
{:.note title="Link"}  

# Majority Element  
---  
__알고리즘을 푸는 스타일은 사람마다 다 다르므로 이것 또한 저의 주관적인 풀이 입니다.__  

## 문제 설명  
>크기가 n인 num로 이루어진 배열이 주어진다. 과반수를 리턴하라  
>과반수는 [n / 2] 이상으로 나타나는 요소이다.  
>과반수 요소는 항상 배열에 존재한다.  

__원문__
>RGiven an array nums of size n, return the majority element.  
>GThe majority element is the element that appears more than ⌊n / 2⌋ times.  
>You may assume that the majority element always exists in the array.  

<br>  
## 예제  

* Example 1:
```js
Input: nums = [3,2,3]
Output: 3
```  

* Example 2:
```js
Input: nums = [2,2,1,1,1,2,2]
Output: 2
```  

## 풀이  

```js
// file: "solution.js"
var majorityElement = function(nums) {
    let map = new Map; // #1
  for(x of nums){ // #2
    map.has(x) ? map.set(x, map.get(x)+1) : map.set(x, 1); // #3
    if(Math.floor(nums.length/2) < map.get(x)){ // #4
      return x
    }
  }
};
```  

## 설명  

1. map 변수에 Map을 선언해 준다.  
2. `for of` 반복문으로 nums 배열을 x 인자로 순차적으로 돌아준다.  
3. Map의 has 메소드로 현재 map에 x번째의 숫자가 있는지 확인 하고 없다면 set 메소드로  
키값을 x번째 인덱스의 숫자를, 밸류 값으로 1을 넣어준다. 숫자가 있다면 x 의 숫자와 맞는 키 를  
꺼내고 꺼낸 값의 밸류에 +1을 해준다.  
4. 조건문으로 과반수를 알기위해 nums 배열의 길이를 2로 나누고 정수로 변환해준다.  
그리고 nums 배열의 과반수(1/2이상) 보다 map에 저장된 밸류값이 더 큰 것이 있다면 리턴해준다.  

```js
let obj = {};
 for(let x of nums){
   obj[x] ? obj[x] = obj[x] + 1 : obj[x] =1
  if(Math.floor(nums.length/2) < obj[x]) {
return x
   }
}
```
Map을 이용한 방법과 비슷한 방법이다. 객체를 이용하는 방법!  

## 회고  

처음 이문제를 보고 생각이 든게 객체로 하면되겠다 생각했었다.  
하지만 같이 이 문제를 풀었던 분이 알고리즘을 잘 하시는 분이었고, Map 생성자를 잘 알고 있어서  
map으로 풀어나갔다. 5분만에 바로 풀어서 너무 기뻤지만, 나에게 조금 난해 했던 문제라  
이해하는데 조금 시간이 걸렸다.  
그리고나서 혹시나 다른 사람들은 어떻게 풀었는지 보았는데 아래와 같이 풀었다.  


```js
var majorityElement = function(nums) {
    let result = 0, count = 0 
    for(let x of nums){
        if(!count) // #1
            result = x // #2
        count = x == result ? count+1 : count-1 // #3
    }
    return result
};
```  

1. count가 0이면  
2. result에 x 인덱스 값을 저장한다.  
3. count가 0이면 값을 result에 저장하고 result에 값과 x의 값이 같으면 count + 1을 하고 아니면 -1을 한다.  
   1. count가 0이 아니라면 바로 result에 값과 x의 값이 같으면 count + 1을 하고 아니면 -1을 한다.  
4. 계속 비교하면서 결국 마지막에 남는 result가 과반수의 숫자다.  

하지만....  

시간이 지나고 충격적인 것을 발견하게 되는데...  


```js
var majorityElement = function(nums) {
    nums.sort((a, b) => a - b);
    return nums[Math.floor(nums.length / 2)];
};
```  

두둥.... 이렇게 간단한 거였나....??????  
nums를 오름차순 정렬해서 배열의 길이를 반으로 나누고 가운데 값...... 그럼 과반수가 나온다.  