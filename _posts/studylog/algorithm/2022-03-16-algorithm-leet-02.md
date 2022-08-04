---
layout:   post
title:    "[Leetcode #3] Longest Substring Without Repeating Characters"
subtitle: "[Leetcode #3] Longest Substring Without Repeating Characters"
category: studylog
tags:     algorithm
image:
  path:    /assets/img/algorithm/algorithm.jpg
---

[Leetcode #3 : Longest Substring Without Repeating Characters]:https://leetcode.com/problems/longest-substring-without-repeating-characters/

<!--more-->
* this ordered seed list will be replaced by the toc
{:toc}  

[Leetcode #3 : Longest Substring Without Repeating Characters]
{:.note title="Link"}  

# Longest Substring Without Repeating Characters  
---  
__알고리즘을 푸는 스타일은 사람마다 다 다르므로 이것 또한 저의 주관적인 풀이 입니다.__  

## 문제 설명  
>문자열인 s 인자가 주어집니다.  
>중복되지 않는 문자열중에 제일 긴 문자열의 길이를 반환하세요.

__원문__
>Given a string s, find the length of the longest substring  
>without repeating characters.  

## 예제  

* Example 1:
```js
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

* Example 2:
```js
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

* Example 3:
```js
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```  

## 풀이  

```js
// file: "solution.js"
var lengthOfLongestSubstring = function(s) {
    let start = 0; // #1
    let index = 0;
    let temporary = '';
    let result = '';
    for(i=0; i<s.length; i++){ // #2
        index = temporary.indexOf(s[i]) // #3
        if(index !== -1){ // #4
            start = start + index + 1 // #5
        } temporary = s.substring(start, i+1) // #6 
        if(temporary.length > result.length) { // #7
            result = temporary
        }
    }return result.length 
};
```  

## 설명  

1. 각 값을 저장할 변수를 설정해 준다.
   1. start : 중복이 되지 않는 문자열이 시작 될 시작점을 지정하기 위한 변수
   2. index : 중목되는 문자열의 인덱스를 저장하기 위한 변수
   3. temporary : 문자열을 임시적으로 저장하기 위한 변수
   4. result : 결과 값을 저장하기 위한 변수  

2. 0부터 문자열의 길이만큼 반복문을 실행
3. 임시로 저장된 문자열변수에서 s[i]의 문자열과 겹치는 문자열이 있으면 저장
4. 중복되는 문자 열이 있다면
5. 시작점을 start 에 중복되는 문자열의 인덱스를 더하고 1을 더함
   1. 1을 더하는 이유는 이전 시작점 + 인덱스는 중복되는 문자열임, 다음 문자열부터 지정
6. 중복되지 않는다면 temporary변수에 substring으로 시작점과 중복되기전 까지의 문자열을 잘라 담음
7. temporary의 값과 result의 값을 비교해서 더 큰 값을 result에 저장
8. result 반환


## 회고  

진심 너무 어려웠다. 제일힘들었던 것은 처음 #5번에 해당되는 변수 설정을  
`start = i` 로만 해주었는데 이렇게해도 결과는 Accepted로 나온다.  
하지만 중복되는 문자열이 붙어있지 않고 떨어져있으면 통과가 안되는데,  
왜 안되는지 되게하려면 어떻게 해야하는지 고민을 많이 했다.  

결국엔 중복되는 시점의 인덱스부터 시작하면안되고 중복되는 첫문자열부터  
시작을 해야하기에 그만큼 앞으로 당겨줘야하는것...  

난 알고리즘에 소질이 없는것같다 ㅠㅠ 그렇지만 노력할 것이다!