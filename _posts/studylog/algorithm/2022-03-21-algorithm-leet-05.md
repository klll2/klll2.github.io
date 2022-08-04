---
layout:   post
title:    "[Leetcode #14] Roman to Integer"
subtitle: "[Leetcode #14] Roman to Integer"
category: studylog
tags:     algorithm
image:
  path:    /assets/img/algorithm/algorithm.jpg
---

[Leetcode #13 : Roman to Integer]:https://leetcode.com/problems/roman-to-integer/

<!--more-->
* this ordered seed list will be replaced by the toc
{:toc}  

[Leetcode #13 : Roman to Integer]
{:.note title="Link"}  

# Roman to Integer  
---  
__알고리즘을 푸는 스타일은 사람마다 다 다르므로 이것 또한 저의 주관적인 풀이 입니다.__  

## 문제 설명  
>로마 숫자는 7개의 다른 숫자료 표시합니다.  
>인자 s 로 로마숫자가 주어지면 정수로 변환하시오  

__원문__
>Roman numerals are represented by seven different  
>Given a roman numeral, convert it to an integer.  

<br>  
## 예제  

* Example 1:
```js
Input: s = "III"
Output: 3
Explanation: III = 3.
```  

* Example 2:
```js
Input: s = "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
```  

* Example 3:
```js
Input: s = "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```  

## 풀이  

```js
// file: "solution.js"
var romanToInt = function(s) {
  const roman = { // #1
      I: 1,
      V: 5,
      X: 10,
      L: 50,
      C: 100,
      D: 500,
      M: 1000,
  }

  let result = 0; // #2

  for(i=0; i<s.length; i++) { // #3
      if(roman[s[i]] < roman[s[i+1]]){  // #4
          result -= roman[s[i]]  // #4-1
      } else {
          result += roman[s[i]]  // #4-2
      }
  } return result // #5
};
}
```  

## 설명  

1. 로마숫자에 해당하는 아라비아 숫자를 객체로 만들어준다.  
2. 마지막 결과값을 담을 result 변수 하나를 숫자형으로 생성해 준다.  
3. 인자로 주어지는 s 의 길이만큼 반복문을 만들어 준다.  
4. 인자 s의 i번째에 해당하는 객체와, i+1을 해준 객체를 비교해서  
   1. i 번째 보다 i+1 번째가 더 작으면 값을 빼고  
   2. 아니라면 그대로 더해준다.  
   왜냐하면 4, 9, 14, 19 ... 4나 9의 숫자는 1과 5를 동시에 쓴 값이기때문에
   4는 IV 이므로 각각 1과 5의 숫자인데 -1의 값을 먼저 저장한뒤 다음 5를 저장하면
   4가 된다. 동시에 쓰는 값은 적은숫자가 앞에 있기때문에 앞과 뒤를 비교해서
   앞의 숫자가 더 작으면 먼저 -1을 빼준다.
5. 결과값을 리턴


## 회고  

값을 저장하고 꺼내는건 객체를 생각하면 쉽지만 4나 9같은경우에는 어떤식으로  
계산해야할지 너무 어려웠는데 앞의 1을 무조건 빼주는 규칙을 발견하고는 조건문을 통해  
5의 배수가 나올때면 1씩 빼주게 만들었다.  
`new Map` 으로 get, set 을 통해 하는방법도 있지만, 뭔가 비효율같아서 삭제  
굳이 올린다면,
```js
var romanToInt = function(s) {
  const roman = new Map()
  
  roman.set('I', 1);
  roman.set('V', 5);
  roman.set('X', 10);
  roman.set('L', 50);
  roman.set('C', 100);
  roman.set('D', 500);
  roman.set('M', 1000);
  
  let result = 0;
  for(i=0; i<s.length; i++){
      const roman1 = roman.get(s[i]);
      const roman2 = roman.get(s[i+1]);
      if(roman1 < roman2){
          result -= roman1
      } else{
          result += roman1
      }
  } return result
};
```  

값을 roman 이라는 Map 생성자를 만든것일뿐 값을 비교하고 하는것은 똑같다.  
