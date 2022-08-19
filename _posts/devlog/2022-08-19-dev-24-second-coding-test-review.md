---
layout: post
title: "[코테] 2주차 오답노트"
subtitle: "[코테] 2주차 오답노트"
date: 2022-08-19 23:41
categories:
  - devlog
tag: [codingtest, zerobase]
image:
  path: ../../../assets/img/algorithm/algorithm.jpg
---

# [코테] 2주차 오답노트

> 2주차 코딩테스트 중 아쉬게 틀린 문제 다시 풀어보기
> 

## 3. ReverseNumber

(0.8 / 1.0)

**[ 문제 설명 ]**

숫자를 뒤집어 주세요.

만약에 -587이 들어오면 -785로 변경되어야 합니다.

결과의 절댓값이 100,000을 넘어가면 0을 출력해주세요.

**[ 제한 사항 ]**

결과의 절댓값이 100,000을 넘어가면 0을 출력합니다.

**[ 입력 형식 ]**

num은 -1,000,000 이상 1,000,000 이하의 정수입니다.

**[ 출력 형식 ]**

leading zeros는 제거합니다. (ex: 340이 입력되면 043이 아니라 43이 출력되어야 합니다.)

int 형식으로 출력합니다.

---

**[ 제출 코드 ]**

```jsx
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

**[ 답안 코드 ]**

```jsx
/**
 * @param num {number}
 * @return {number}
 */
function solution(num) {
  let reverseNumber = 0;
  const NEGATIVE = num < 0;

  if (NEGATIVE) num *= -1;

  for (let i = num; i; i = Math.trunc(i / 10)) {
    reverseNumber = reverseNumber * 10 + (i % 10);
  }

  if (100000 < reverseNumber) {
    return 0;
  }

  return NEGATIVE ? -reverseNumber : reverseNumber;
}

solution
```

---

## 4. ReverseSentence

(0.6 / 1.0)

**[ 문제 설명 ]**

알파벳 대/소문자와 숫자 그리고 구분자인 마침표(”.”), 쉼표(”,”), 느낌표(”!”), 물음표(”?”), 스페이스(” “)로 이뤄진 문장이 있습니다. 문장 내에는 구분자를 기준으로 단어를 구분합니다.

문장 s가 주어질 때, 단어를 거꾸로 출력하는 함수, solution을 완성해주세요.

예를 들어, 문장 “Hello, World!?”가 주어진다고 가정할 때, 구분자를 기준으로 구분된 단어는 “Hello, World”이며, 단어를 거꾸로 출력한 결과는 [”olleH”, “dlroW”] 입니다.

**[ 입력 형식 ]**

s는 길이가 1 이상 1000 이하의 문자열입니다.

**[ 출력 형식 ]**

단어를 거꾸로 치환한, 문자열로 이뤄진 배열을 출력합니다.

비어있는 단어는 제거하고 출력합니다.

---

**[ 제출 코드 ]**

```jsx
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

**[ 답안 코드 ]**

```jsx
/**
 * @param s {string}
 * @return {string[]}
 */
function solution(s) {
  return s.split(/[.,!? ]/)
    .filter(word => word !== '')
    .map(word => word.split('').reverse().join(''));
}

solution
```

---

## 5. NumberPick

(0.8 / 1.0)

**[ 문제 설명 ]**

배열 A에는 0~9까지의 숫자가 랜덤하게 들어있습니다.

해당 배열의 숫자를 두개 뽑아 조합했을 때 K번째로 큰 숫자를 리턴하는 함수를 작성하세요.

**[ 입력 형식 ]**

0 ~ 9까지의 임의의 숫자 배열 A

숫자 K

**[ 출력 형식 ]**

K 번째 큰 2자리 숫자

---

**[ 제출 코드 ]**

```jsx
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

**[ 답안 코드 ]**

```jsx
function solution(A, R)
{
  var result = "";

  A.sort(function(a, b) {
    return b - a;
  });

  result += A.splice(R/A.length, 1);
  result += A[R%A.length == 0 ? A.length -1 : R%A.length - 1];

  return result;
}
```

---

## 6. AppDesign

(0.4 / 1.0)

**[ 문제 설명 ]**

앱 디자인을 하려고 합니다. 디자인 영역 area가 주어질 때, 이 영역과 일치하는 사각형의 가로 w와 세로 h를 구하는 함수, solution을 완성해주세요.

단, 다음 조건을 만족해야 합니다.

세로 화면 최적화를 위해 가로는 세로보다 길 수 없습니다.

여러 가능한 가로, 세로 조합 중 두 값의 차이가 가장 적은 값을 찾습니다.

예를 들어, area가 4일 때, 커버할 수 있는 가로, 세로는 다음과 같습니다.

가로 w가 1 이고 세로 h가 4인 경우.

가로 w가 2 이고 세로 h가 2인 경우.

가로 w가 4 이고 세로 h가 1인 경우는 가로가 세로보다 길기 때문에 제외됩니다.

이 중, 가로, 세로의 차이가 가장 적은 가로 w가 2, 세로 h가 2인 [2, 2]를 반환합니다.

**[ 입력 형식 ]**

area는 1 이상 100,000 이하의 정수입니다.

**[ 출력 형식 ]**

가로, 세로의 값을 배열로 담은 [w, h]를 반환합니다.

가로, 세로는 1 이상 100,000 이하의 정수입니다.

---

**[ 제출 코드 ]**

```jsx
function solution(area) {
  let answer = [0, 0];
  let combination = [];
  let i = 1;
  for (let i = 1; i <= area / 2; i++) {
    if (area % i == 0) {
      let x = parseInt(area / i);
      let y = i;
      if (x > y) {
        answer[0] = y;
        answer[1] = x;
      } else {
        answer[0] = x;
        answer[1] = y;
      }
    }
  }

  return answer;
}

console.log(solution(4));
```

**[ 답안 코드 ]**

```jsx
/**
 * @param area {number}
 * @returns {number[]}
 */
function solution(area) {
  let w = Math.floor(Math.sqrt(area))
  while (area % w !== 0) w--
  return [w, area / w]
}

solution
```

---

## 9. CoronaKeepDistance

(0.6 / 1.0)

**[ 문제 설명 ]**

코로나로 인해 거리 두기를 수행 중입니다.

사람들의 간격 lineUp은 사람을 나타내는 1과 비어있는 자리 0의 배열로 이루어져 있습니다.

코로나 심각도에 따라 거리두기 레벨 level이 주어질 때 방역수칙을 준수했는지 여부를 출력하는 함수, solution을 완성해주세요.

예를 들어, lineUp이 c이고, level이 2일 때, 결과는 true입니다.

첫 번째 사람 (index=0)과 두 번째 사람 (index=4)은 거리가 3만큼 떨어져 있으므로 방역수칙을 준수했습니다.

두 번째 사람 (index=4)과 세 번째 사람 (index=7)은 거리가 2만큼 떨어져 있으므로 방역수칙을 준수했습니다.

결과 : 방역수칙을 준수했습니다.

**[ 제한 사항 ]**

두 사람 사이의 거리 즉, lineUp의 두 개의 1 사이의 0의 수가 K일 때, K ≥ level이면 방역수칙 준수 중입니다.

**[ 입력 형식 ]**

lineUp은 길이가 1 이상 1,000 이하의 배열입니다.

lineUp은 0과 1의 요소로 이루어져 있습니다.

level은 1 이상 1,000 이하의 정수입니다.

**[ 출력 형식 ]**

방역수칙 준수 여부를 boolean 값으로 출력합니다.

---

**[ 제출 코드 ]**

```jsx
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

**[ 답안 코드 ]**

```jsx
/**
 * @param lineUp {number[]}
 * @param level {number}
 * @returns {boolean}
 */
function solution(lineUp, level) {
  let distanceSoFar = 9999
  for (let num of lineUp) {
    if (num === 1) {
      if (distanceSoFar < level) return false
      distanceSoFar = 0
    } else if (num === 0) {
      distanceSoFar++
    }
  }
  return true
}

solution
```

---

## 10. CombineTwoDigirOddNumber

(0.8 / 1.0)

**[ 문제 설명 ]**

한 자리 숫자 배열 array가 주어집니다. 주어진 수를 조합해서 만들 수 있는 두 자리 홀수의 개수를 출력하는 함수 solution을 완성해주세요.

예를 들어, array [1, 3, 4]가 주어질 때, 조합할 수 있는 두 자리 홀수는 [13, 31, 41, 43]으로 결과는 4입니다.

**[ 입력 형식 ]**

- array는 길이가 100 이하의 배열입니다.
- array는 1 이상 9 이하의 정수로 이루어져 있습니다.

**[ 출력 형식 ]**

- 조합할 수 있는 두 자리의 홀수 개수를 출력합니다.

---

**[ 제출 코드 ]**

```jsx
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

**[ 답안 코드 ]**

```jsx
/**
 * @param array {number[]}
 * @return {number}
 */
function solution(array) {
  let set = new Set()

  for (let i = 0; i < array.length; i++) {
    for (let j = 0; j < array.length; j++) {
      if (i === j) continue

      const num = createNumber(array[i], array[j])
      const isEven = num % 2 === 1
      if (isEven) {
        set.add(num)
      }
    }
  }

  return set.size
}

function createNumber(tenDigits, oneDigit) {
  return tenDigits * 10 + oneDigit
}

export default solution
```