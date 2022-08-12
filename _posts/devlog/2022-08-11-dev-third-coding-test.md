---
layout: post
title: "[코테] 3주차 코딩테스트"
subtitle: "[코테] 3주차 코딩테스트"
date: 2022-08-11 14:30
categories:
  - devlog
tag: [codingtest, zerobase]
image:
  path: ../../../assets/img/algorithm/algorithm.jpg
---

# [코테] 3주차 코딩테스트

**8월 3일**, 세 번째 코딩테스트가 있었다.

---

결과는

![third-coding-test](../../assets/img/develop/2022-08-11-dev-third-coding-test/third-coding-test.png)

10점 만점에 7.8점! 지난 주보다는 0.2점 떨어진 조금 아쉬운 성적이었다.

---

상승곡선을 그리며 점수가 향상되었으면 했다마는 아쉬운 결과였다. 

여전히 10번은 건드리지도 못했다.. ㅠ

다음 테스트는 좀 더 심기일전해서 볼 수 있도록 하겠다!

---

## 내 풀이

### 1. ReverseText

```jsx
function solution(s) {
  var answer = "";

  for (let element of s) {
    answer = element + answer;
  }

  return answer;
}

console.log(solution("apple"));
```

### 2. CountEqualElement

```jsx
function solution(nums) {
  var answer = 0;

  let tmp = [];

  for (let element of nums) {
    tmp.push(element);
  }

  for (let i = 0; i < tmp.length; i++) {
    for (let j = i + 1; j < tmp.length; j++) {
      if (tmp[i] == tmp[j]) answer++;
    }
  }

  return answer;
}

nums = [2, 5, 6, 3, 2, 6, 6];
console.log(solution(nums));
```

### 3. CountPrefixWordNumber

```jsx
function solution(array, s) {
  var answer = 0;

  let arrays = [];
  for (let element of array) {
    arrays.push(element);
  }

  let compare = [];
  for (let element of s) {
    compare.push(element);
  }

  let tmp = 0;

  for (let i = 0; i < arrays.length; i++) {
    for (let j = 0; j < arrays[i].length; j++) {
      if (arrays[i].charAt(j) == compare[tmp]) {
        tmp++;
      } else {
        tmp = 0;
        break;
      }

      if (tmp == arrays[i].length) {
        answer++;
        tmp = 0;
      }
    }
  }

  return answer;
}

let array = ["n", "nav", "nev"];
let s = "naver";

console.log(solution(array, s));
```

### 4. IndexOfWord

```jsx
// (0.8/1.0)

function solution(sentence, word) {
  var answer = -1;
  let answers = [];
  let bool = false;

  let array = sentence.split(" ");

  for (let i = 0; i < array.length; i++) {
    if (array[i] === word) {
      answers.push(i);
      bool = true;
    }
  }

  if (!bool) return answer;
  else if (answers.length == 1) return answers[0];
  else return answers;
}

let sentence = "Hello every world";
let word = "every";

console.log(solution(sentence, word));
```

### 5. SmallestSameIndex

```jsx
function solution(nums, n) {
  var answer = -1;

  let array = [];
  for (let element of nums) {
    array.push(element);
  }

  for (let i = 0; i < array.length; i++) {
    if (array[i] == n) {
      answer = i;
      break;
    }
  }

  return answer;
}

let nums = [1, 3, 5, 3, 2];
let n = 3;

console.log(solution(nums, n));
```

### 6. CountEqualWithDividedNumber

```jsx
function solution(nums, d) {
  var answer = 0;

  let array = [];
  for (let element of nums) {
    array.push(element);
  }

  for (let i = 0; i < array.length - 1; i++) {
    for (let j = i + 1; j < array.length; j++) {
      if (array[i] == array[j] && array[i] % d == 0) answer++;
    }
  }

  return answer;
}

let nums = [4, 1, 2, 1, 4];
let d = 2;

console.log(solution(nums, d));
```

### 7. CountMatchedPrefixWord

```jsx
// (0.8/1.0)

function solution(array, p) {
  var answer = 0;

  let arrays = [];
  for (let element of array) {
    arrays.push(element);
  }

  let compare = [];
  for (let element of p) {
    compare.push(element);
  }

  let tmp = 0;

  for (let i = 0; i < arrays.length; i++) {
    for (let j = 0; j < arrays[i].length; j++) {
      if (arrays[i].charAt(j) == compare[tmp]) {
        tmp++;
      } else {
        tmp = 0;
        break;
      }

      if (tmp == compare.length) {
        tmp = 0;
        answer++;
      }
    }
  }

  return answer;
}

let array = ["apple", "banana", "kakao", "naver", "apache"];
let p = "a";

console.log(solution(array, p));
```
