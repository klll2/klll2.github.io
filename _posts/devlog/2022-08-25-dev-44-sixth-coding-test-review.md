---
layout: post
title: "[코테] 6주차 오답노트"
subtitle: "[코테] 6주차 오답노트"
date: 2022-08-25 16:57
categories:
  - devlog
tag: [codingtest, zerobase]
image:
  path: ../../../assets/img/algorithm/algorithm.jpg
---

# [코테] 6주차 오답노트

> 6주차 코딩테스트 중 아쉬게 틀린 문제 다시 풀어보기
> 

## 1. Billboard

(0.2 / 1.0)

**[ 문제 설명 ]**

n개의 문자를 보여주는 크기가 n인 전광판이 있습니다. 전광판의 문자는 오른쪽에서 왼쪽으로 반복해서 흘러가며, 1초에 한 글자씩 흘러갑니다.

예를 들어, 크기가 5인 전광판에 “Snowball” 노출한다고 가정할 때, 시간 t의 변화에 따른 노출 예시는 다음과 같습니다.

t : 0초

전광판 : …..

t : 1초

전광판 : ….S

t : 5초

전광판 : Snowb

t : 10초

전광판 : all..

t : 15초

전광판 : …Sn

전광판의 크기 n과 전광판에 노출할 문자 s 그리고 시간 t가 주어질 때, t 초 후의 전광판에 표시될 문구를 출력하는 함수, solution을 완성해주세요.

**[ 제한 사항 ]**

전광판의 문자는 1초부터 흐르기 시작합니다.

**[ 입력 형식 ]**

n은 1 이상 50 이하의 정수입니다.

s는 길이가 1 이상 100 이하의 문자열입니다.

s는 알파벳 대/소문자와 숫자로 구성됩니다.

t는 1 이상 1000 이하의 정수입니다.

**[ 출력 형식 ]**

t 초 후, 주어진 전광판에 노출되는 문자를 출력합니다.

전광판의 공백은 마침표(”.”)로 대체하여 출력합니다.

---

**[ 제출 코드 ]**

```jsx
function solution(n, s, t) {
  let result = '';
  
  let str = '';
  for (let element of s) {
    str += element;
  }

  let sample = [];
  for (let i = 0 ; i < n ; i++) {
    sample.push('.');
  }

  for (let i = 0 ; i < t % (str.length * 2) ; i++) {
    sample.shift();
    sample.push(i < str.length ? str.substring(i, i + 1) : '.');
  }

  for (let element of sample) {
    result += element;
  }

  return result;
 }

 console.log(solution(5, "Snowball", 18));
```

**[ 답안 코드 ]**

```jsx
/**
 * @param n {number}
 * @param s {string}
 * @param t {number}
 * @return {string}
 */
function solution(n, s, t) {
  // 반복 주기
  const repeatDuration = n + s.length;

  // 반복되는 주기를 제외하고 남은 시간 계산
  const optimizeTime = t % repeatDuration;

  // 남은 시간이 흐른 후의 전광판 출력
  const text = '.'.repeat(n) + s + '.'.repeat(n - 1);
  return text.substr(optimizeTime, n);
}

solution
```

---

## 3. BusStop

(0.0 / 1.0)

**[ 문제 설명 ]**

도시의 아파트에서 버스 정류장까지 거리를 구하려고 합니다. 도시는 격자 모양의 지역으로 구분되어 있으며, 아파트는 1로, 버스 정류장은 0으로 표시되어 있습니다. 아파트에서 버스 정류장으로 이동은 상하좌우로만 이동할 수 있으며, 대각선으로는 이동이 불가합니다.

예를 들어, 3 x 3 크기의 도시 [[1, 0, 1], [1, 1, 1], [1, 1, 1]]가 주어질 때, 각 아파트에서 가까운 버스 정류장까지의 거리를 나타내는 결과는 [[ 1, 0, 1 ], [ 2, 1, 2 ], [ 3, 2, 3 ]] 입니다.

**[ 제한 사항 ]**

도시에서 이동은 상하좌우로만 이동할 수 있으며, 대각선으로는 이동할 수 없습니다.

도시에서 버스 정류장은 적어도 하나 이상 존재합니다.

도시에는 아파트와 버스 정류장만 존재합니다.

**[ 입력 형식 ]**

도시의 정보 city가 주어집니다.

city는 0과 1로 이루어진 h x w 크기의 2차원 배열입니다.

도시의 크기 h와 w는 1 이상 50 이하의 정수입니다.

**[ 출력 형식 ]**

아파트에서 버스 정류장까지의 최단 거리를 출력합니다.

결과는 h x w 크기의 2차원 배열입니다.

---

**[ 제출 코드 ]**

```jsx
function solution(city) {
  
  return
}

console.log(solution([[1, 0, 1], [1, 1, 1], [1, 1, 1]]));
```

**[ 답안 코드 ]**

```jsx
/**
 * @param city {number[][]}
 * @return {number[][]}
 */
function solution(city) {
  return calcDistance(city);
}

function calcDistance(city) {
  const aptLocations = [];
  const busLocations = [];

  getLocations(city, aptLocations, busLocations);

  const ret = createBaseResult(city);

  for (let aptIndex = 0; aptIndex < aptLocations.length; aptIndex++) {
    const aptY = aptLocations[aptIndex][0];
    const aptX = aptLocations[aptIndex][1];
    for (let busIndex = 0; busIndex < busLocations.length; busIndex++) {
      const distance = getDistance(aptLocations[aptIndex], busLocations[busIndex]);
      ret[aptY][aptX] = (ret[aptY][aptX] === 0) ? distance : Math.min(ret[aptY][aptX], distance);
    }
  }

  return ret;
}

function getLocations(city, aptLocations, busLocations) {
  const ySize = city.length;
  const xSize = city[0].length;

  for (let y = 0; y < ySize; y++) {
    for (let x = 0; x < xSize; x++) {
      if (city[y][x] === 1) {
        aptLocations.push([y, x]);
      } else {
        busLocations.push([y, x]);
      }
    }
  }
}

function createBaseResult(city) {
  const ySize = city.length;
  const xSize = city[0].length;

  return Array.from(Array(ySize), () => new Array(xSize).fill(0));
}

function getDistance(aptLocation, busLocation) {
  return Math.abs(aptLocation[0] - busLocation[0]) + Math.abs(aptLocation[1] - busLocation[1]);
}

solution
```

---

## 6. MoleGame

(0.4 / 1.0)

**[ 문제 설명 ]**

3 x 3개의 격자 형태의 두더지 게임판이 있습니다. 두더지들은 들어가거나 나와 있는데, 이 두더지들을 모두 나오도록 바꾸는 게임입니다.

두더지를 조작하는 유일한 방법은 10개의 스위치를 조작하는 것으로, 각 스위치는 1개 이상의 두더지에 연결되어 있습니다.

한 스위치를 누를 때마다, 해당 스위치와 연결된 나와 있던 두더지는 들어가고, 들어가 있던 두더지는 나옵니다.

이때, 모든 두더지를 나오게 하려면 최소한 스위치를 몇 번이나 눌러야 할지를 출력하는 함수, solution을 완성해주세요.

예를 들어, 게임판의 9마리 두더지 상태 state로 [ 1, 0, 1, 0, 0, 1, 1, 1, 1 ]가 있고, 10개의 스위치에 연결된 두더지 번호 linkNums가 [ [1], [7], [8], [4, 7], [1, 3], [3, 4, 8], [0], [6], [2], [1, 4] ] 라고 가정할 때,

스위치에 연결된 두더지 정보는 다음과 같습니다.

스위치 0에 연결된 두더지 번호 1

스위치 1에 연결된 두더지 번호 7

스위치 2에 연결된 두더지 번호 8

스위치 3에 연결된 두더지 번호 4, 7

스위치 4에 연결된 두더지 번호 1, 3

스위치 5에 연결된 두더지 번호 3, 4, 8

스위치 6에 연결된 두더지 번호 0

스위치 7에 연결된 두더지 번호 6

스위치 8에 연결된 두더지 번호 2

스위치 9에 연결된 두더지 번호 1, 4

이때, 모든 두더지를 나오게 하려면 최소한 3번의 스위치(스위치 0, 2, 5)를 눌러야 합니다.

**[ 제한 사항 ]**

두더지의 상태는 0이면 들어가 있는 두더지, 1이면 나와 있는 두더지입니다.

**[ 입력 형식 ]**

두더지 상태 state가 주어집니다.

state는 0과 1로 이루어진 길이가 9인 배열입니다.

스위치에 연결된 두더지 번호 linkNums가 주어집니다.

linkNums는 각 스위치에 연결된 두더지 번호로 이루어진 길이가 10인 배열입니다.

**[ 출력 형식 ]**

모든 두더지를 나오게 하도록 스위치를 눌러야 하는 최소한의 수를 int 형식으로 출력합니다.

모든 두더지를 나오게 할 수 없다면 -1을 출력합니다.

---

**[ 제출 코드 ]**

```jsx

```

**[ 답안 코드 ]**

```jsx
/**
 * @param state {number[]}
 * @param linkNums {number[][]}
 * @return {number}
 */
function solution(state, linkNums) {
  const linked = generateLinked(linkNums);
  const minClickCount = countMinClickToAllOut(state, linked, 0);

  // 모든 두더지를 나오게 할 수 없으면 -1을 반환한다.
  return minClickCount === INF ? -1 : minClickCount;
}

const INF = 9999;

// 주어진 linkNums를 사용하기 편하게 이중 배열로 가공한다
function generateLinked(linkNums) {
  const MOLE_SIZE = 9;
  const linked = [];

  for (let i = 0; i < linkNums.length; i++) {
    linked[i] = new Array(MOLE_SIZE).fill(0);

    for (let j = 0; j < linkNums[i].length; j++) {
      const linkedMoleIndex = linkNums[i][j];
      linked[i][linkedMoleIndex] = 1;
    }
  }

  return linked;
}

function countMinClickToAllOut(state, linked, switchIndex) {
  // 기저사례 : 모든 스위치를 순회한 경우
  if (switchIndex >= linked.length) return (isAllOut(state) ? 0 : INF);

  // 스위치 누른 횟수를 큰 수로 초기화 한다.
  let clickCount = INF;
  for (let i = 0; i < 2; i++) {
    // 스위치를 누른 횟수가 작은 수를 취한다.
    clickCount = Math.min(clickCount, i + countMinClickToAllOut(state, linked, switchIndex + 1));
    clickSwitch(state, linked, switchIndex);
    // 버튼을 2번 누르면 초기 상태로 돌아간다.
  }

  return clickCount;
}

// 모든 두더지가 나왔는지 확인
function isAllOut(state) {
  return state.reduce((acc, cur) => acc && cur === 1, true);
}

// 스위치 눌렀을 때, 두더지의 상태 변경
function clickSwitch(state, linked, switchIndex) {
  for (let i = 0; i < linked[switchIndex].length; i++) {
    const isLinked = linked[switchIndex][i] === 1;
    if (isLinked) {
      state[i] = (state[i] + 1) % 2;
    }
  }
}

solution
```

---

## 8. pyramidGame

(0.8/1.0)

**[ 문제 설명 ]**

n 층의 피라미드의 꼭대기에서 1층으로 내려와 탈출하려고 합니다. 피라미드에는 방이 있으며, n 층에는 1개의 방이 존재하고, n-1 층에는 2개의 방, n-2 층에는 3개의 방, 1층에는 n개의 방이 존재합니다.

각 방은 왼쪽 아래와 오른쪽 아래의 방으로 이동하는 계단이 있고, 각 방에는 j개의 보석이 존재합니다.

n 층의 피라미드 각 방에 존재하는 보석의 정보 arr가 주어질 때, 꼭대기 층에서 1층까지 내려오면서 모을 수 있는 보석의 최대 수를 구하는 함수, solution을 완성해주세요.

예를 들어, 3층의 피라미드 그림 (a) 인 각 방에 존재하는 보석의 정보 arr가 [ [3], [5, 10], [4, 8, 6] ]이 주어질 때, 피라미드를 탈출하며 모을 수 있는 보석의 최대 수는 그림 (b) 인 다음과 같습니다.

![pyramidGame.png](../../assets/img/develop/2022-08-25-dev-sixth-coding-test-review/pyramidGame.png)

3 + 10 + 8 = 21

**[ 제한 사항 ]**

계단은 올라갈 수 없고, 내려갈 수만 있습니다.

**[ 입력 형식 ]**

피라미드의 층수 n은 1 이상 100 이하의 정수입니다.

각 방의 보석 수 j는 1 이상 1000 이하의 정수입니다.

**[ 출력 형식 ]**

피라미드를 탈출하며 모을 수 있는 보석의 최대 수를 int 형식으로 출력합니다.

---

**[ 제출 코드 ]**

```jsx
function solution(arr) {
  let result = 0;
  let array = [...arr];

  result += array[0][0];

  let position = 0;
  for (let element of array) {
    if (element == array[0]) continue;

    if (element[position] > element[position + 1]) {
      result += element[position];
    } else {
      result += element[position + 1];
      position += 1;
    }

  }

  return result;
}

console.log(solution([[3], [5, 10], [4, 8, 6]]));
```

**[ 답안 코드 ]**

```jsx
/**
 * @param arr {number[][]}
 * @return {number}
 */
function solution(arr) {
  const dp = [];

  const n = arr.length;
  for (let i = n - 1; i >= 0; i--) {
    dp[i] = [];
    for (let j = i; j >= 0; j--) {
      if (i === n - 1) {
        dp[i][j] = arr[i][j];
        continue;
      }

      dp[i][j] = arr[i][j] + Math.max(dp[i + 1][j], dp[i + 1][j + 1]);
    }
  }

  return dp[0][0];
}

solution
```