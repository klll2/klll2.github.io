---
layout:   post
title:    "[Leetcode #11] Container With Most Water"
subtitle: "[Leetcode #11] Container With Most Water"
category: studylog
tags:     algorithm
image:
  path:    /assets/img/algorithm/algorithm.jpg
---

[Leetcode #11 : Container With Most Water]:https://leetcode.com/problems/container-with-most-water/

<!--more-->
* this ordered seed list will be replaced by the toc
{:toc}  

[Leetcode #11 : Container With Most Water]
{:.note title="Link"}  

# Majority Element  
---  
__알고리즘을 푸는 스타일은 사람마다 다 다르므로 이것 또한 저의 주관적인 풀이 입니다.__  

## 문제 설명  
>x축과 함께 컴테이너를 형성하는 두개의 선을 찾아라.
>물을 담는 제일 면적이 넓은 값이어야 한다.

__원문__
>You are given an integer array height of length n.  
>There are n vertical lines drawn such that the two endpoints  
>of the ith line are (i, 0) and (i, height[i]). 

>Find two lines that together with the x-axis form a container, 
>such that the container contains the most water.

<br>  
## 예제  

* Example 1:
![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)
```js
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
```  

* Example 2:
```js
Input: height = [1,1]
Output: 1
```  


## 풀이  

```js
// file: "solution.js"
var maxArea = function(height) {
    let result = 0;
    let i = 0;
    let j = height.length-1 // #1
    while(i < j){ // #2
        result = Math.max(result, Math.min(height[i], height[j])*(j-i)) // #3
        height[i] < height[j] ? i++ : j-- // #4
    } 
    return result // #5
};
```

## 설명  

1. 결과값을 저장할 `result`, 제일 좌측 인덱스를 지정할 `i` 제일 우측 인덱스를 지정 할 `j` 선언  
2. `i` 값이 `j` 값보다 작는 한 계속 반복문을 돌아 준다.  
3. 면적 구하기는 가로 곱하기 세로 그래서 일일히 다 계산해서 기존의 값과 비교 후 더 큰값을 저장  
   1. 세로의 높이가 길면 물이 넘치므로 `Math.min`으로 제일 좌측과 우측중에 작은 값을 골라
   가로의 면적(j에서 i를 뺀 값)과 곱한다. 그리고 result와 비교하여 더 큰값을 바로 result에 넣어준다.  
4. 높이 i 인덱스 값이 j 인덱스 값보다 낮으면 좌측 인덱스를 1씩 한단계 올려주고 아니라면 j를 뺀다.  
5. 결과값 리턴!  


## 회고  

지금은 여러번 되새겨 보며 어느정도 이해가 가지만, 처음엔 문제 자체 접근을 못했다.  
최대면적 구하는 수학 공식은 이미 머리속에서 지워진지 오래이기때문에 공식 자체를 모르니  
접근을 할 수가 없었다. 그래서 어쩔수 없이 답을 조금 찾아보았다.ㅠ_ㅠ  
알고리즘은 역시 수학을 잘해야 한다는 말은 틀린말은 아닌셈  
더욱더 노력 해야겠다.
