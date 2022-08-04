---
layout:   post
title:    "[프로그래머스 #42576] 완주하지 못한 선수"
subtitle: "[프로그래머스 #42576] 완주하지 못한 선수"
category: studylog
tags:     algorithm
image:
  path:    /assets/img/algorithm/algorithm.jpg
---

<!--more-->
[프로그래머스 #42576 : 완주하지 못한 선수]:https://programmers.co.kr/learn/courses/30/lessons/42576
<!--more-->
* this ordered seed list will be replaced by the toc
{:toc}  

[프로그래머스 #42576 : 완주하지 못한 선수]
{:.note title="Link"}  

---  
__알고리즘을 푸는 스타일은 사람마다 다 다르므로 이것 또한 저의 주관적인 풀이 입니다.__

## 문제 설명  

>완주하지 못한 선수  
>
>수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는  
>모든 선수가 마라톤을 완주하였습니다.

>마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의  
>이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을  
>return 하도록 solution 함수를 작성해주세요.  

## 제한 사항  

>마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.  
>completion의 길이는 participant의 길이보다 1 작습니다.  
>참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.  
>참가자 중에는 동명이인이 있을 수 있습니다.  

<br>  

## 입출력 예  

| participant |  completion   |   return   |
| :-------: | :---------: | :------: |
| ["let","kiki","eden"] | ["eden","kiki"] |  "leo"  |
| ["marina", "josipa", "nikola", "vinko", "filipa"] | ["josipa", "filipa", "marina", "nikola"] |  "vinko"  |
| ["mislav", "stanko", "mislav", "ana"] | ["stanko", "ana", "mislav"] | "mislav" |

## 입출력 예 설명
예제 #1  
"leo"는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.  

예제 #2
"vinko"는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.  

예제 #3
"mislav"는 참여자 명단에는 두 명이 있지만, 완주자 명단에는 한 명밖에 없기 때문에  
한명은 완주하지 못했습니다.  


## 풀이  

```java
// file: "solution.js"
function solution(participant, completion) {
  let map = new Map();  // #1
  for (let p of participant) {
    map.has(p) ? map.set(p, map.get(p) + 1) : map.set(p, 1);
  }  // #2
  for (let c of completion) { 
    map.set(c, map.get(c) - 1);  // #3
  }
  for (let [key, value] of map) {  // #4
    if (value !== 0) {  // #5
      return key;  // #6
    }
  }
}
```

## 설명  

1. hash map을 이용하기 위하여 map을 만들어 줍니다.  
2. 선수들이 map에 있는지 확인하고 없다면 선수에 +1 을 해주고 없다면 1을 해줍니다.  
3. 완주한 선수들이 map에 있는지 확인하고 있다면 -1 을 해줍니다.  
4. map을 반복문을 돌려서 key와 value를 뽑아냅니다.  
5. value가 0이 아니면 완주를 못한 사람이기에  
6. 선수(key)를 리턴시켜 줍니다. 동명이인이라도 완주한 사람만 -1이기때문에 다 걸립니다.  