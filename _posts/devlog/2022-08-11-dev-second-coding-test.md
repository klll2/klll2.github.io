---
layout: post
title: "[코테] 2주차 코딩테스트"
subtitle: "[코테] 2주차 코딩테스트"
date: 2022-08-11 00:50
categories:
  - devlog
tag: [codingtest, zerobase]
image:
  path: ../../../assets/img/algorithm/algorithm.jpg
---

# [코테] 2주차 코딩테스트

**7월 27일**, 지난 주의 참패에 이어 두 번째 코딩테스트가 있는 날이었다!

---

이전보다 더 열심히 준비한 결과!

![second-coding-test.png](../../assets/img/develop/2022-08-11-dev-second-coding-test/second-coding-test.png)

이전보다는 만족스러운 결과였다!

---

물론 언제나 목표는 만점이기에 만점을 받지 못한 문제들이 있다는 점이 무척 아쉽지만, 이전의 피드백이 효과가 있었다는 것이 입증되어 기뻤고, 이대로 꾸준히 공부해나가야겠다 다짐했다!

마지막 코딩테스트 전까지는 만점에 가까운 점수를 받을 수 있을 실력이 되면 좋겠다!

---

## 내 풀이

### 1. CountEven

```jsx
function solution(arr) {
  var answer = 0;

  for (let i of arr) {
    if (i % 2 == 0) answer++;
  }

  return answer;
}
```

### 2. CountEvenEachNumber

```jsx
function solution(n) {
  var answer = 0;

  while (true) {
    let tmp = n % 10;
    n = parseInt(n / 10);
    // console.log(tmp);
    if (tmp % 2 == 0) answer++;
    if (n == 0) break;
  }

  return answer;
}

console.log(solution(2875812));
```

### 3. ReverseNumber

```jsx
// (0.8/1.0)

function solution(num) {
  var answer = "";

  if (num < 0) {
    answer += "-";
    num *= -1;
  }

  let tmp = num % 10;
  if (tmp != 0) answer += tmp;
  num = parseInt(num / 10);

  while (true) {
    answer += num % 10;
    num = parseInt(num / 10);
    if (num == 0) break;
  }

  answer = parseInt(answer);
  if (answer > 100000) {
    return 0;
  }

  return answer;
}

console.log(solution(-587));
```

### 4. ReverseSentence

```jsx
// (0.6/1.0)

function solution(s) {
  let answer = [];

  let tmp = "";

  for (let i of s) {
    switch (i) {
      case ".":
      case ",":
      case "!":
      case "?":
      case " ":
        if (tmp != "") answer.push(tmp);
        tmp = "";
        break;
      default:
        tmp = i + tmp;
    }
  }

  return answer;
}

console.log(solution("Hello, World!?"));
```

### 5. NumberPick

```jsx
// (0.8/1.0)

function solution(A, K) {
  var answer = 0;
  A.sort(function (a, b) {
    return b - a;
  });

  let i = parseInt(K / 4);
  let j = K % 4;
  if (i == j) j++;

  answer = A[i] * 10 + A[j];

  return answer;
}

console.log(solution([1, 2, 3, 4, 5], 1));
```

### 7. BinaryDistance

```jsx
function solution(n) {
  var answer = 0;
  let binary = n.toString(2);

  let length = 0;
  for (let i of binary) {
    if (i == 0) {
      length++;
    } else {
      length++;
      if (answer < length) answer = length;
      length = 0;
    }
  }

  return answer;
}

console.log(solution(11));
```

### 8. Corona

```jsx
function solution(history, infected) {
  let answer = [];
  let corona = false;
  let now = [];

  for (let element of history) {
    if (element == infected) {
      corona = true;
      for (let elements of now) {
        if (!answer.includes(elements)) {
          answer[answer.length] = elements;
        }
      }

      continue;
    } else if (element * -1 == infected) {
      corona = false;

      continue;
    }

    if (element > 0) {
      if (corona) {
        if (!answer.includes(element)) {
          answer[answer.length] = element;
        }
      }
      if (!now.includes(element)) {
        now[now.length] = element;
      }
    } else {
      for (let i = 0; i < now.length; i++) {
        if (now[i] == element * -1) {
          now.splice(i, 1);
          break;
        }
      }
    }
  }

  answer.sort(function (a, b) {
    return a - b;
  });

  return answer;
}

console.log(solution([3, 2, -3, 1, -1, -2, 4, -4, 1, -1], 2));
```

### 9. CoronaKeepDistance

```jsx
// (0.6/1.0)

function solution(lineUp, level) {
  var answer = true;

  let length = 0;
  for (let i = 1; i < lineUp.length; i++) {
    if (lineUp[i] == 0) {
      length++;
    } else {
      if (level > length) {
        answer = false;
        return answer;
      } else {
        continue;
      }
    }
  }

  return answer;
}

console.log(solution([1, 0, 0, 0, 1, 0, 0, 1], 2));
```

### 10. CombineTwoDigitOddNumber

```jsx
// (0.8/1.0)

function solution(array) {
  var answer = 0;

  let count = 0;
  let length = 0;

  for (let element of array) {
    if (element % 2 == 1) {
      count++;
    }
    length++;
  }

  answer = (length - 1) * count;

  return answer;
}

console.log(solution([1, 3, 4]));
```