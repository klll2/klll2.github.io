---
layout:   post
title:    "[Leetcode #20] Valid Parentheses"
subtitle: "[Leetcode #20] Valid Parentheses"
category: studylog
tags:     algorithm
image:
  path:    /assets/img/algorithm/algorithm.jpg
---

[Leetcode #20 : Valid Parentheses]:https://leetcode.com/problems/valid-parentheses/

<!--more-->
* this ordered seed list will be replaced by the toc
{:toc}  

[Leetcode #20 : Valid Parentheses]
{:.note title="Link"}  

# Majority Element  
---  
__알고리즘을 푸는 스타일은 사람마다 다 다르므로 이것 또한 저의 주관적인 풀이 입니다.__  

## 문제 설명  
>'(', ')', '{', '}', '[' and ']' 이 포함된 문자열 s 가 주어진다.
>s가 유효한 표현인지 아닌지 true/false로 반환해주세요.

__원문__
>Given a string s containing just the characters '(', ')', '{', '}', '[' and ']',  
>determine if the input >string is valid.  
>You may assume that the majority element always exists in the array.  
>An input string is valid if:
>Open brackets must be closed by the same type of brackets.
>Open brackets must be closed in the correct order.
<br>  
## 예제  

* Example 1:
```js
Input: s = "()"
Output: true
```  

* Example 2:
```js
Input: s = "()[]{}"
Output: true
```  

* Example 3:
```js
Input: s = "(]"
Output: false
```  

## 풀이  

```js
// file: "solution.js"
var isValid = function(s) {
  while(s.includes('()') || s.includes('{}')|| s.includes('[]')){ // #1
    s = s.replace('()','').replace('{}','').replace('[]','') // #2
  } return !s.length // #3
};
```  

## 설명  

1. while 반복문으로 '()','{}','[]'와 같은것이 더이상 나오지 않을때까지 s배열을 돈다.  
2. 같은것이 있으면 그 문자열을 삭제한다. 더이상 #1과 같은것이 나오지 않는다면,  
3. 리턴 (배열 s가 다 비어있으면 true, 그렇지 않으면 false)  

## 회고  

처음엔 Stack으로 생각했으나, 조금 쉽게 단순하게 생각했다. 어짜피 같은 괄호와 닫는것이  
아니면 무조건 true이기에 같은 문자열만 지워주면 되니까!  

아래는 Stack으로 풀어본 것  

```js
// file : "stack.js"
var isValid = function(s) {
  let stack = []
  for(i in s){
    if(s[i]==='('){
      stack.push(')')
    } else if (s[i]==='{'){
      stack.push('}')
    } else if (s[i]==='['){
      stack.push(']')
    } 
    else if(stack.pop()!==s[i]){
      return false
    }      
  } return !stack.length
};
```

* s배열을 돌면서 해당 괄호가 있으면 반대 괄호를 Stack에 저장하고, 해당 괄호가 없으면,  
* 스택에 있는 것을 꺼내서 다음 순번이랑 비교하고 맞지 않으면 false 모두 맞는다면 true  