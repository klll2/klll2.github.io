---
layout: post
title: "ex [Inflearn #11] 졸업 선물"
subtitle: "[Inflearn #11] 졸업 선물"
category: studylog
tags: algorithm
image:
  path: /assets/img/algorithm/algorithm.jpg
---

<!--more-->

[인프런 : js 알고리즘 문제풀이]: https://www.inflearn.com/course/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4

- this ordered seed list will be replaced by the toc
  {:toc}

[인프런 : JS 알고리즘 문제풀이]  
{:.note title="Link"}

**인프런 코테 대비 알고리즘 문제풀이를 정리해 놓은 것입니다.**

## 문제 설명

> 졸업 선물
>
> 선생님은 올해 졸업하는 반 학생들에게 졸업선물을 주려고 합니다.  
> 학생들에게 인터넷 쇼핑몰에서 각자 원하는 상품을 골라 그 상품의 가격과 배송비를 제출하라고 했습니다.  
> 선생님이 가지고 있는 예산은 한정되어 있습니다.
> 현재 예산으로 최대 몇 명의 학생에게 선물을 사줄 수 있는지 구하는 프로그램을 작성하세요.  
> 선생님은 상품 하나를 50% 할인해서(반 가격) 살 수 있는 쿠폰을 가지고 있습니다.  
> 배송비는 할인에 포함되지 않습니다.

<br>

## 문제 예제

▣ 입력설명  
첫 번째 줄에 반 학생수 N(1<=N<=1000)과 예산 M(1<=M<=100,000,000)이 주어진다.  
두 번째 줄부터 N줄에 걸쳐 각 학생들이 받고 싶은 상품의 가격과 배송비가 입력됩니다.  
상품가격과 배송비는 각각 100,000을 넘지 않습니다. 상품가격은 짝수로만 입력됩니다.

▣ 출력설명  
첫 번째 줄에 선생님이 현재 예산으로 선물할 수 있는 최대 학생수를 출력합니다.  
선생님 최소한 1개 이상의 상품을 살 수 있는 예산을 가지고 있습니다.

▣ 입력예제 1  
5 28  
6 6  
2 2  
4 3  
4 5  
10 3

▣ 출력예제 1  
4

출력설명
(2, 2), (4, 3), (4, 5)와 (10, 3)를 할인받아 (5, 3)에 사면 비용이 4+7+9+8=28입니다.

## 풀이

```java
// file: "solution.js"
function solution(m, product) {
  let answer = 0;  // #1
  let money = 0;
  product.sort((a, b) => a[0] + a[1] - (b[0] + b[1]));  // #2
  for (i = 0; i < product.length; i++) {  // #3
    money = m - product[i][0] / 2 + product[i][1];  // #4
    let count = 1;  // #11
    for (j = 0; j < product.length; j++) {  // #5
      if (j !== i && product[j][0] + product[j][1] > money) break;  // #6
      if (j !== i && product[j][0] + product[j][1] <= money) {  // #7
        money -= product[j][0] + product[j][1];  // #8
        count++;  // #9
      }

      answer = Math.max(answer, count);  // #10
    }
  }
  return answer;
}
```

## 설명

1. 답을 리턴시킬 answer 와 money 값을 지정해 줄 변수를 선언해 줍니다.
2. 한정적인 금액으로 많이 살 수 있는 것은 적은 금액 순이므로 parameter로 들어올 배열을  
   오름차순으로 정렬해 줍니다.
3. 배열을 다 돌릴 반복문을 만들어 줍니다.
4. 배열을 하나씩 50% 할인 해서 총 금액에서 빼고 택배비를 더한 후 시작합니다.
5. 할인 금액을 제외한 나머지 금액을 돌릴 반복문을 만들어 줍니다.  
   (할인한 선물의 금액은 이미 총금액에서 빼주었기 때문에 j 와 i가 같지 않은것만 계산 되게 한다.)
6. 남은 금액보다 선물의 값이 높으면 (선물을 사지 못하므로) 중단 해줍니다.
7. 남은 금액보다 선물의 값이 낮으면
8. 남은 금액에서 선물의 값을 빼주고
9. count의 숫자를 올려줍니다.
10. answer와 count중 높은 수를 answer에 대입해 줍니다.
11. 다음 반복문을 위해 카운트를 1로(할인된 선물의 값이 있기때문에 1) 초기화 해줍니다.
