---
layout:   post
title:    "[Inflearn #8] 봉우리"
subtitle: "[Inflearn #8] 봉우리"
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

>봉우리  
>
>지도 정보가 N*N 격자판에 주어집니다. 각 격자에는 그 지역의 높이가 쓰여있습니다.  
>각 격자 판의 숫자 중 자신의 상하좌우 숫자보다 큰 숫자는 봉우리 지역입니다.  
>봉우리 지역이 몇 개 있는 지 알아내는 프로그램을 작성하세요.  
>격자의 가장자리는 0으로 초기화 되었다고 가정한다.  
>만약 N=5 이고, 격자판의 숫자가 다음과 같다면 봉우리의 개수는 10개입니다.  

![](data:image/png;base64,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){: width="50%" height="50%"}


<br>  

## 문제 예제  

▣ 입력설명  
첫 줄에 자연수 N이 주어진다.(1<=N<=50)  
두 번째 줄부터 N줄에 걸쳐 각 줄에 N개의 자연수가 주어진다.  
각 자연수는 100을 넘지 않는다.  

▣ 출력설명  
봉우리의 개수를 출력하세요.  

▣ 입력예제 1  
5
5 3 7 2 3  
3 7 1 6 1  
7 2 5 3 4  
4 3 6 4 1  
8 7 3 5 2  

▣ 출력예제 1  
10  


## 풀이  

```js
// file: "solution.js"
function solution(arr) {
  let answer = 0;
  let n = arr.length;
  let dx = [-1, 0, 1, 0];  // #1
  let dy = [0, 1, 0, -1];  // #2
  for (i = 0; i < n; i++) {
    for (j = 0; j < n; j++) {  // #3
      let flag = true;  // #4
      for (k = 0; k < dx.length; k++) {  // #5
        let nx = i + dx[k];  // 현재위치 i에서 좌우 탐색
        let ny = j + dy[k];  // 현재위치 j에서 상하 탐색
        if (nx >= 0 && nx < n && ny >= 0 && ny < n && arr[nx][ny] >= arr[i][j]) {
          // 없는 값을 탐색하면 에러이기때문에 nx와 ny는 0보다 크거나 같고 n보다 작아야 한다.
          flag = false;  // #6
          break;
        }
      }
      if (flag) { // #7
        answer++;
      }
    }
  }
  return answer;
}
```

## 설명  

1. 현재 위치(arr[i][j]) 에서 비교할 x 축 좌표를 설정합니다. 왼쪽(-1) 오른쪽(1)  
2. 현재 위치(arr[i][j]) 에서 비교할 y 출 좌표를 설정합니다. 위(-1) 아래(1)  
3. 행과 열에 접근하는 이중 반복문을 만든다.  
4. 봉우리의 조건에 맞지 않으면 바로 넘기기 위한 boolean 변수를 생성해 준다.  
5. 1,2번에서 설정한 것에 대한 반복문을 만든다. (현재 위치에서 상하좌우를 비교하기 위해)  
6. 현재위치보다 상하좌우가 높으면 조건에 맞지 않기때문에 false를 담아주고 break를 한다.  
7. flag가 true면 봉우리의 조건이 맞기 때문에 answer을 1씩 더해준다.  

