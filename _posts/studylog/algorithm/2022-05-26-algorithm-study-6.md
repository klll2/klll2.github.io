---
layout:   post
title:    "[Inflearn #6] 일곱 난쟁이"
subtitle: "[Inflearn #6] 일곱 난쟁이"
category: studylog
tags:     algorithm
image:
  path:    /assets/img/algorithm/algorithm.jpg
---

<!--more-->

[인프런 : JS 알고리즘 문제풀이]:https://www.inflearn.com/course/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4

* this ordered seed list will be replaced by the toc
{:toc}  

[인프런 : JS 알고리즘 문제풀이]  
{:.note title="Link"}  

__인프런 코테 대비 알고리즘 문제풀이를 정리해 놓은 것입니다.__  

## 문제 설명  

>일곱 난쟁이  
>
>왕비를 피해 일곱 난쟁이들과 함께 평화롭게 생활하고 있던 백설공주에게 위기가 찾아왔다.  
>일과를 마치고 돌아온 난쟁이가 일곱 명이 아닌 아홉 명이었던 것이다.  
>아홉 명의 난쟁이는 모두 자신이 "백설 공주와 일곱 난쟁이"의 주인공이라고 주장했다.  
>뛰어난 수학적 직관력을 가지고 있던 백설공주는, 다행스럽게도 일곱 난쟁이의 키의 합이  
>100이 됨을 기억해 냈다.  
>아홉 난쟁이의 키가 주어졌을 때, 백설공주를 도와 일곱 난쟁이를 찾는 프로그램을 작성하시오.  


<br>  

## 문제 예제  

▣ 입력설명  
아홉 개의 줄에 걸쳐 난쟁이들의 키가 주어진다.  
주어지는 키는 100을 넘지 않는 자연수이며, 아홉 난쟁이의 키는 모두 다르며,  
가능한 정답이 여러 가지인 경우에는 아무거나 출력한다.  

▣ 출력설명  
입력된 순서대로 일곱 난쟁이의 키를 출력한다.  

▣ 입력예제 1  
20 7 23 19 10 15 25 8 13  

▣ 출력예제 1  
20 7 23 19 10 8 13  


## 풀이  

```java
// file: "solution.js"
function solution(arr) {
  let answer = arr;
  let sum = arr.reduce((a, b) => a + b); // #1
  for (let i = 0; i < arr.length - 1; i++) {
    for (let j = i + 1; j < arr.length; j++) { // #2
      if (sum - (arr[i] + arr[j]) === 100) { // #3
        arr.splice(j, 1); // #4
        arr.splice(i, 1);
      }
    }
  }
  return answer;
}
```

## 설명  

1. 9명의 난쟁이 키의 총합을 구한다. reduce 메소드를 이용해 누산한다.  
2. 7명 난쟁이 키의 총합은 100, 나머지 2명의 키를 뺐을때 100이 나오면  
그 나머지 2명이 가짜 난쟁이 이다. 그래서 일일이 2명을 짝지어 더해주는 2중 for문을 만든다.  
3. 9명 키의 총 합과 2명의 합을 빼서 100이 되는지 확인한다.  
4. 3번 조건문에서 100 되면 나머지 두명이 가짜 난쟁이 이므로 해당 하는 인덱스를 빼준다.  
* 여기서 뒷부분부터 splice를 해주는 이유는 앞에서부터 하면 인덱스가 당겨지기때문에  
두번째 splice를 할 때 엉뚱한 인덱스가 삭제된다.  

