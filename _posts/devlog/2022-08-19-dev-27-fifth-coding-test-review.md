---
layout: post
title: "[코테] 5주차 오답노트"
subtitle: "[코테] 5주차 오답노트"
date: 2022-08-19 23:44
categories:
  - devlog
tag: [codingtest, zerobase]
image:
  path: ../../../assets/img/algorithm/algorithm.jpg
---

# [코테] 5주차 오답노트

> 5주차 코딩테스트 중 아쉬게 틀린 문제 다시 풀어보기
> 

## 1. SortedAppearNumber

(0.8 / 1.0)

**[ 문제 설명 ]**

숫자로 이루어진 문자열 s가 있습니다. 이때 가장 많이 들어온 숫자 순서대로 출력하는 함수, solution을 완성해주세요.

단, 들어온 횟수가 같은 경우에는 작은 수를 먼저 출력합니다.

예를 들어, s가 ‘221123’으로 주어질 때, 출력 결과는 ‘2 1 3 0 4 5 6 7 8 9’ 입니다.

**[ 입력 형식 ]**

s는 길이가 1 이상 100,000 이하의 문자열입니다.

s는 숫자로 구성됩니다.

**[ 출력 형식 ]**

가장 많이 들어온 숫자 순서대로 공백으로 구분하여 string 형식으로  출력합니다.

---

**[ 제출 코드 ]**

```jsx
function solution(s) {
  let num = Number(s);

  let arr = new Array();
  for(let i = 0 ; i < 10 ; i++) {
    arr[i] = 0;
  }

  let resultArr = new Array();
  for(let i = 0 ; i < 10 ; i++) {
    resultArr[i] = i;
  }

  while(1) {
    arr[num % 10]++;
    num = Math.floor(num / 10);
    if(num == 0) break;
  }

  resultArr = bubble(arr, resultArr);

  let result = "";
  for (let i = 0 ; i < resultArr.length ; i++) {
    result += resultArr[i];
    if(i != resultArr.length - 1)
      result += ' ';
  }

  return result;
}

function bubble (array, result) {
  for (let i = 0 ; i < array.length - 1 ; i++) {
    let swap;
    for (let j = 0 ; j < array.length - 1 - i ; j++) {
      if (array[j] < array[j + 1]) {
        swap = array[j];
        array[j] = array[j + 1];
        array[j + 1] = swap;

        swap = result[j];
        result[j] = result[j + 1];
        result[j + 1] = swap;
      }
    }
  }

  return result;
}

console.log(solution("221123"));
```

**[ 답안 코드 ]**

```jsx
/**
 * @param s {string}
 * @returns {string}
 */
function solution(s) {
  const countedArr = getCountedArr(s);
  const orders = getBiggerOrders(countedArr);
  return orders.join(' ');
}

function getCountedArr(s) {
  const result = new Array(10).fill(0)
  for (let i = 0; i < s.length; i++) {
    result[s[i]]++;
  }
  return result;
}

function getBiggerOrders(arr) {
  const order = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
  for (let high = 1; high < arr.length; high++) {
    for (let low = 0; low < high; low++) {
      if (arr[low] < arr[high]) {
        switching(arr, low, high);
        switching(order, low, high);
      } else if (arr[low] === arr[high] && order[low] > order[high]) {
        switching(order, low, high);
      }
    }
  }
  return order;
}

function switching(arr, i, j) {
  const temp = arr[i];
  arr[i] = arr[j];
  arr[j] = temp;
}

solution
```

---

## 5. 4Rule

(0.2 / 1.0)

**[ 문제 설명 ]**

문자열 S는 숫자와 4칙연산 기호로 이루어진 수식입니다.

해당 수식을 4칙연산 계산 순서에 맞춰 계산하는 함수를 작성하세요.

단, 소수점 자리는 2번째 자리까지 표현합니다.

**[ 입력 형식 ]**

사칙 연산이 가능한 String 문자열

**[ 출력 형식 ]**

소수점 2자리까지 표현된 사칙 연산 결과값

예를 들어, S가 “23+5/63+15” 인 경우 결과는 23.50 입니다.

---

**[ 제출 코드 ]**

```jsx
function solution(S) {
  
}

console.log(solution("2-6-7*8/2+5"));
```

**[ 답안 코드 ]**

```jsx
function solution(S){
    var arr = S.split("");
    var numbers = S.match(/\d+/gi);
    var operators = S.match(/[+\-*/]/gi);
  
    var temp = parseFloat(numbers[0]);
    var result = 0;
  
    for(var i = 0; i < operators.length; i++){
      switch (operators[i]) {
        case '*':
          temp *= parseFloat(numbers[i+1]);
          break;
        case '/':
          temp /= parseFloat(numbers[i+1]);
          break;
        case '+':
          result += temp;
          temp = 0;
          temp += parseFloat(numbers[i+1]);
          break;
        case '-':
          result += temp;
          temp = 0;
          temp -= parseFloat(numbers[i+1]);
          break;
      }
    }
  
    result += temp;
  
    return result.toFixed(2);
  }
```

---

## 6. CountBinaryCard

(0.8 / 1.0)

**[ 문제 설명 ]**

2진수를 학습하던 윤주는 색종이로 이를 표현하려고 합니다. 2진수의 1은 붉은색 종이로, 0은 흰색 종이로 표현할 때, 흰색 종이가 무수히 많은 윤주는 붉은색 종이를 얼마나 준비해야 하는지 궁금해졌습니다.

숫자 n이 주어질 때, 0부터 n까지 수를 색종이로 표현하려고 합니다. 

이 때, 윤주가 준비해야 하는 붉은색 종이의 수를 구하는 함수, solution을 완성해주세요.

예를 들어, 숫자 3이 주어진다고 가정할 때, 필요한 붉은색 종이의 수의 예시는 다음과 같습니다.

0을 이진수로 표현 : 0

0을 표현할 때 필요한 붉은색 종이 수 : 0개

1을 이진수로 표현 : 1

1을 표현할 때 필요한 붉은색 종이 수 : 1개

2를 이진수로 표현 : 10

2를 표현할 때 필요한 붉은색 종이 수 : 1개

3을 이진수로 표현 : 11

3을 표현할 때 필요한 붉은색 종이 수 : 2개

결과 : 0개 + 1개 + 1개 + 2개 = 4개

**[ 입력 형식 ]**

n은 1 이상 100,000 이하의 정수입니다.

**[ 출력 형식 ]**

총 필요한 붉은색 종이의 수를 int 형식으로 출력합니다.

---

**[ 제출 코드 ]**

```jsx
function solution(n) {
  let count = 0;

  for (let i = 1 ; i <= n ; i++) {
    let value = i.toString(2);
    value = Number(value);
    while(value != 0) {
      if(value % 10 == 1) count++;
      console.log(value);
      value = Math.floor(value / 10);
    }
  }

  return count;
}

console.log(solution(3));
```

**[ 답안 코드 ]**

```jsx
/**
 * @param n {number}
 * @return {number}
 */
function solution(n) {
  // 중복된 결과를 저장
  const dp = [0];

  // 2의 배수로 반복되는 bit 처리를 위함
  let offset = 1;

  for (let i = 1; i <= n; i++) {
    if (offset * 2 === i) offset *= 2;

    dp[i] = dp[i - offset] + 1;
  }

  // 0부터 n까지 필요한 붉은색 종이수
  return dp.reduce((a, b) => a + b, 0);
}

solution
```