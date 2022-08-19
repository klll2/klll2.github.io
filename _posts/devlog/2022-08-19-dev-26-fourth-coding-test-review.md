---
layout: post
title: "[코테] 4주차 오답노트"
subtitle: "[코테] 4주차 오답노트"
date: 2022-08-19 23:43
categories:
  - devlog
tag: [codingtest, zerobase]
image:
  path: ../../../assets/img/algorithm/algorithm.jpg
---

# [코테] 4주차 오답노트

> 4주차 코딩테스트 중 아쉬게 틀린 문제 다시 풀어보기
> 

## 6. FoundMatchedWord

(0.6 / 1.0)

**[ 문제 설명 ]**

낱말 퍼즐을 풀려고 합니다. 퍼즐 판은 4 x 4 크기로 임의의 한글이 섞여 있습니다.

주어진 낱말이 퍼즐 판에 인접한 형태로 존재하는지 구하는 함수, solution을 완성해주세요.

예를 들어, puzzle [[`대`, `한`, `가`, `나`], [`국`, `민`, `다`, `라`], [`마`, `바`, `사`, `아`], [`자`, `차`, `카`, `타`]] 과 word `대한민국`이 있을 때,

> puzzle[0][0] = `대`

> puzzle[0][1] = `한`

> puzzle[1][1] = `민`

> puzzle[1][0] = `국`

으로 결과는 true입니다.

**[ 제한 사항 ]**

- 모든 낱말은 한글입니다.
- 인접함은 상하좌우로 붙어있는 단어를 말합니다.
- word는 공백없는 문자열입니다.
- 한번 사용된 퍼즐 판의 낱말은 또다시 사용할 수 없습니다.

**[ 입력 형식 ]**

- puzzle은 4 * 4 크기의 배열입니다.
- word는 길이가 1 이상 10 이하의 문자열입니다.

**[ 출력 형식 ]**

- 주어진 낱말이 퍼즐 판에 인접한 형태로 존재하는지를 출력합니다.

---

**[ 제출 코드 ]**

```jsx
function solution(puzzle, word) {
  let answer = true;
  let array = [...word];

  
  for(let i = 0 ; i < 4 ; i++) {

  }

  return answer;
}

console.log(solution([["대", "한", "가", "나"], ["국", "민", "다", "라"], ["마", "바", "사", "아"], ["자", "차", "카", "타"]], "대한민국"));
```

**[ 답안 코드 ]**

```jsx
/**
 * @param puzzle {string[][]}
 * @param word {string}
 * @returns {boolean}
 */
function solution(puzzle, word) {
  for (let x = 0; x < SIZE; x++) {
    for (let y = 0; y < SIZE; y++) {
      if (move(puzzle, word, x, y, 0)) return true;
    }
  }

  return false;
}

const SIZE = 4;
const DIRECTIONS = [
  [-1, 0],
  [0, 1],
  [1, 0],
  [0, -1],
];

function move(puzzle, word, x, y, moveIndex) {
  if (puzzle[x][y] !== word[moveIndex]) return false;
  if (moveIndex === word.length - 1) return true;

  puzzle[x][y] = 'x';

  for (const [dx, dy] of DIRECTIONS) {
    const dirX = x + dx;
    const dirY = y + dy;
    if (0 <= dirX && dirX < SIZE && 0 <= dirY && dirY < SIZE) {
      if (move(puzzle, word, dirX, dirY, moveIndex + 1)) return true;
    }
  }

  return false;
}

solution
```

---

## 7. Lamp

(0.4 / 1.0)

**[ 문제 설명 ]**

r * c 크기의 온실에 식물을 키우고 있습니다. 식물이 잘 자라도록 n * n만큼 커버가 가능한 램프를 설치하려고 합니다.

r * c 크기의 field에 식물이 없는 경우 0으로, 식물이 있는 경우 1로 주어지고, 램프의 크기 n이 주어질 때, 최대한 커버 가능한 식물의 수를 구하는 함수, solution을 완성해주세요.

예를 들어, 3 x 3 크기의 온실 [[1, 0, 1], [0, 0, 1], [0, 1, 1]]가 그림 (a) 와 같이 주어지고 램프의 크기 2가 주어질 때, 최대한 커버 가능한 식물의 수는 그림 (b) 와 같이 3입니다.

**[ 제한 사항 ]**

- 주어진 식물은 옮겨 심을 수 없습니다.

**[ 입력 형식 ]**

- 온실의 식물 정보 field가 주어집니다.
- field는 0과 1로 이루어진 r x c 크기의 2차원 배열입니다.
- 온실의 크기 r과 c는 1 이상 100 이하의 정수입니다.
- 램프의 크기 n이 주어집니다.
- n은 1 이상 r과 c 이하의 정수입니다.

**[ 출력 형식 ]**

- 램프의 최대한 커버 가능한 식물의 수를 출력합니다.

---

**[ 제출 코드 ]**

```jsx
function solution(field, n) {
  
}

console.log(solution([[1, 0, 1], [0, 0, 1], [0, 1, 1]], 2));
```

**[ 답안 코드 ]**

```jsx
/**
 * @param field {number[][]}
 * @param n {number}
 * @return {number}
 */
function solution(field, n) {
  const fieldRow = field.length;
  const fieldCol = field[0].length;
  const rowSize = fieldRow - n + 1;
  const colSize = fieldCol - n + 1;

  let ret = 0;
  for (let row = 0; row < rowSize; row++) {
    for (let col = 0; col < colSize; col++) {
      ret = Math.max(ret, countPlant(field, n, row, col));
    }
  }

  return ret;
}

function countPlant(field, n, row, col) {
  let plantCount = 0;

  for (let curRow = row; curRow < row + n; curRow++) {
    for (let curCol = col; curCol < col + n; curCol++) {
      plantCount += field[curRow][curCol];
    }
  }

  return plantCount;
}

solution
```

---

## 8. LargestPerimeterRectangle

(0.4 / 1.0)

**[ 문제 설명 ]**

둘레가 가장 큰 사각형을 구하려고 합니다.

N개의 정수로 만들 수 있는 둘레가 가장 큰 사각형의 둘레를 구하는 함수, solution을 완성해주세요.

예를 들어, arr [3, 2, 3, 1]이 주어질 때, 결과는 9입니다.

**[ 제한 사항 ]**

- 사각형을 만들 수 없는 경우 0을 반환합니다.

**[ 입력 형식 ]**

- arr는 길이가 4 이상 1,000 이하인 배열입니다.
- arr의 요소는 1 이상 1,000,000 이하의 정수입니다.

**[ 출력 형식 ]**

- 둘레가 가장 큰 사각형의 둘레를 구합니다.

---

**[ 제출 코드 ]**

```jsx
function solution(arr) {
}
```

**[ 답안 코드 ]**

```jsx
/**
 * @param arr {number[]}
 * @returns {number}
 */
function solution(arr) {
  arr.sort((a, b) => b - a)
  console.log(arr)
  for (let i = 0; i < arr.length - 3; i++) {
    if (isRectangleable(arr[i], arr[i + 1], arr[i + 2], arr[i + 3])) return arr[i] + arr[i + 1] + arr[i + 2] + arr[i + 3]
  }

  return 0
}

function isRectangleable(longest, long, short, shortest) {
  return longest < long + short + shortest
}

solution
```

---

## 10.

(0.0 / 1.0)

**[ 문제 설명 ]**

넓이가 같은 n개의 나무판자를 붙여 만든 다리가 있습니다.

태풍의 영향으로 다리가 부서지고, 각 나무판자의 길이가 들쭉날쭉하게 잘려 나가서 더욱 튼튼한 철골 다리로 새로 만들기로 했습니다.

이때, 기존 다리의 나무판자 일부를 직사각형으로 잘라 재활용하고자 할 때, 그림 (b)는 다리 (a)에 남겨진 나무판자에서 잘라낼 수 있는 가장 넓은 직사각형이며, 그림 (c)와 같이 비스듬하게 자를 수 없습니다.

나무판자의 길이 배열 1이 주어질 때, 잘라낼 수 있는 직사각형의 최대 넓이를 구하는 함수, solution을 완성해주세요.

**[ 제한 사항 ]**

- 모든 나무판자의 넓이는 1이라고 가정합니다.
- 나무판자의 수직과 수평에 맞춰 잘라야 하며, 비스듬하게 자를 수 없습니다.

**[ 입력 형식 ]**

- 왼쪽부터 순서대로 나무판자의 길이 배열 l이 주어집니다.
- l은 1 이상 10,000 이하의 정수로 이뤄진 배열입니다.
- 나무판자의 수 n은 1개 이상 10,000개 이하입니다.

**[ 출력 형식 ]**

- 다리에서 잘라낼 수 있는 직사각형의 최대 크기를 출력합니다.

---

**[ 제출 코드 ]**

```jsx
function solution(l) {
  let answer;

  

  return answer;
}

console.log(solution([1, 10, 10, 10, 5]));
```

**[ 답안 코드 ]**

```jsx
/**
 * @param l {number[]}
 * @return {number}
 */
function solution(l) {
  return calcMaxArea(l, 0, l.length - 1);
}

const calcMaxArea = function (l, left, right) {
  // 기저사례 : 나무판자가 하나인 경우
  if (left === right) return l[left];

  // 중간 지점 구한다.
  const mid = Math.floor((left + right) / 2);

  // 중간지점을 기준으로 좌/우의 최대 넓이를 구한다
  const leftMaxArea = calcMaxArea(l, left, mid);
  const rightMaxArea = calcMaxArea(l, mid + 1, right);

  let low = mid;
  let high = mid + 1;
  let curMinLength = Math.min(l[low], l[high]);
  let curMaxArea = curMinLength * 2;

  // 좌/우로 한칸씩 이동하며 최대 넓이를 구한다.
  while (left < low || high < right) {
    // 나무판자의 길이가 긴 방향으로 한칸씩 이동한다.
    if ((left < low) && ((high === right) || (l[low - 1] > l[high + 1]))) {
      low--;
      curMinLength = Math.min(curMinLength, l[low]);
    } else {
      high++;
      curMinLength = Math.min(curMinLength, l[high]);
    }

    const curWidth = high - low + 1;
    curMaxArea = Math.max(curMaxArea, curMinLength * curWidth);
  }

  // 각 넓이중 최대 넓이를 반환한다.
  return Math.max(leftMaxArea, rightMaxArea, curMaxArea);
};

solution
```