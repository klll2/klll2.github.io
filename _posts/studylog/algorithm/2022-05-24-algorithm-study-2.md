---
layout:   post
title:    "[Inflearn #2] 삼각형 판별하기"
subtitle: "[Inflearn #2] 삼각형 판별하기"
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
>삼각형 판별하기
>
>길이가 서로 다른 A, B, C 세 개의 막대 길이가 주어지면 이 세 막대로 삼각형을 
>만들 수 있 으면 “YES"를 출력하고, 만들 수 없으면 ”NO"를 출력한다.



<br>  

## 문제 예제  

▣ 입력설명  
첫 번째 줄에 100이하의 서로 다른 A, B, C 막대의 길이가 주어진다.  
▣ 출력설명  
첫 번째 줄에 “YES", "NO"를 출력한다.  
▣ 입력예제 1 6 7 11  
▣ 출력예제 1 YES  
▣ 입력예제 1 13 33 17  
▣ 출력예제 1 NO  


## 풀이  

* 메소드 없이 풀기
```js
// file: "solution.js"
   function solution(a, b, c) {
        let answer;
        let max;
        let result;
        const sum = a + b + c;

        if (a > b) {
          max = a;
        } else if (a < b) {
          max = b;
        } else if (max < c) {
          max = c;
        }

        result = sum - max;

        if (result > max) {
          answer = 'YES';
        } else {
          answer = 'NO';
        }

        return answer;
      }
```

* 메소드 사용
```js
// file: "solution.js"
   function solution(a, b, c) {
        let maxNum = Math.max(a, b, c);
        let num = [a, b, c].filter((e) => e !== maxNum);

        let numSum = num[0] + num[1];

        if (numSum > maxNum) {
          answer = 'YES';
        } else {
          answer = 'NO';
        }

        return answer;
      }
```

* 강의 해설
```js
// file: "solution.js"
    function solution(a, b, c){
                let answer="YES", max;
                let tot=a+b+c;
                if(a>b) max=a;
                else max=b;
                if(c>max) max=c;
                if(tot-max<=max) answer="NO"; 
                return answer;
            }
```


## 설명  

>삼각형이 되기 위한 조건  
>-> 최대 길이가 나머지 두길이의 합보다 짧아야한다.  

1. a,b,c에 대한 모두 더해 값을 저장한다.  
2. a,b,c중 최대 값을 더한다.  
3. 모두 더한값에 최대값을 빼주고 최대값이 더 크다면 'No'를 출력, 작다면 'Yes' 출력  


