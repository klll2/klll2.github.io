---
layout: post
title: "[코테] 3주차 오답노트"
subtitle: "[코테] 3주차 오답노트"
date: 2022-08-19 23:42
categories:
  - devlog
tag: [codingtest, zerobase]
image:
  path: ../../../assets/img/algorithm/algorithm.jpg
---

# [코테] 3주차 오답노트

> 3주차 코딩테스트 중 아쉬게 틀린 문제 다시 풀어보기
> 

## 4. IndexOfWord

(0.8 / 1.0)

**[ 문제 설명 ]**

문장 sentence에서 word가 몇 번째 인덱스의 단어와 일치하는지를 출력하는 함수, solution을 완성해주세요.

sentence에서 단어의 구분은 공백(” “)으로 구분합니다.

예를 들어, sentence가 “Hello every world” 이고, word가 “every” 일 때 결과는 1 입니다.

**[ 제한 사항 ]**

- sentence에서 word와 일치하는 단어가 없으면 -1을 반환합니다.

**[ 입력 형식 ]**

- sentence와 word는 길이가 1000 이하의 문자열입니다.
- sentence와 word는 알파벳 대/소문자로 구성됩니다.

**[ 출력 형식 ]**

- word와 일치하는 단어의 인덱스를 반환합니다.

---

**[ 제출 코드 ]**

```jsx
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

**[ 답안 코드 ]**

```jsx
/**
 * @param sentence {string}
 * @param word {string}
 * @returns {number}
 */
function solution(sentence, word) {
  if (word === '') return -1

  const words = sentence.split(' ')

  for (let i = 0; i < words.length; i++) {
    if (words[i] === word) return i
  }

  return -1
}

export default solution
```

---

## 7. CountMatchedPrefixWord

(0.8 / 1.0)

**[ 문제 설명 ]**

문자열 배열 array와 문자열 p가 주어집니다. 이때, array의 요소 중 p를 접두사로 갖는 단어의 수를 출력하는 함수, solution을 완성해주세요.

예를 들어, array가 [ ‘apple’, ‘banana’, ‘kakao’, ‘naver’, ‘apache’ ] 이고, p가 ‘a’ 일 때 다음과 같습니다.

- ‘apple’은 ‘a’를 접두사로 갖습니다.
- ‘apache’는 ‘a’를 접두사로 갖습니다.

결과는 2입니다.

**[ 입력 형식 ]**

- array는 길이가 100 이하의 배열입니다.
- array는 길이가 100 이하의 문자열로 이루어져 있습니다.
- p는 길이가 100 이하의 문자열입니다.

**[ 출력 형식 ]**

- p를 접두사로 갖는 array 요소 개수를 출력합니다.

---

**[ 제출 코드 ]**

```jsx
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

**[ 답안 코드 ]**

```jsx
/**
 * @param array {number[]}
 * @param p {string}
 * @return {number}
 */
function solution(array, p) {
  let result = 0

  for (let i = 0; i < array.length; i++) {
    const s = array[i]
    if (s.indexOf(p) === 0) {
      result++
    }
  }

  return result
}

export default solution
```

---

## 8. Organize

(0.8 / 1.0)

**[ 문제 설명 ]**

제로마트에서 창고정리를 위해 보유하고 있는 재고를 줄을 세워서 순차적으로 정리하려고 합니다.

다만, 저희는 굉장히 게으르기 때문에 stock 배열이 주어지면, 딱 한 번만 일을 하려고 합니다.

이 때, 저희가 할 수 있는 일은 2가지가 있습니다. 첫 번째로는 두 가지 물품의 자리를 서로 바꾸는 일과 두 번째로는 정해진 시작과 끝 자리의 물건을 거꾸로 배치하는 일을 할 수 있습니다.

예를 들어 [1, 2, 5, 4, 3] 라는 배열이 존재할 때, 5와 3의 위치를 바꾸면 순차적으로 정렬이 되고, 또는 5부터 3까지의 위치를 통째로 거꾸로 배치하면 순차적으로 정렬이 됩니다.

이는 [5, 4, 3] 의 배열을 [3, 4, 5] 로 거꾸로 배치하여 원래의 자리에 넣는 것과 일맥상통합니다.

이와 같은 2가지 업무를 할 수 있을 때, 주어진 재고배열을 가지고 한 번의 업무로 오름차순으로 배치할 수 있으면 1, 배치할 수 없다면 0으로 반환해주세요.

**[ 제한 사항 ]**

- 재고 배열의 길이는 2 이상 100000 이하입니다.
- 각 재고 원소의 크기는 0 이상 100000 이하입니다.
- 모든 재고 원소는 재고 배열에 유일하게 존재합니다.

**[ 입력 형식 ]**

- stock이라는 재고 배열이 주어집니다.

**[ 출력 형식 ]**

- 재고 배열을 정해진 1번의 작업만으로 오름차순으로 배열할 수 있는지 여부를 반환해주세요.

---

**[ 제출 코드 ]**

```jsx
function solution(stock) {
  var answer = 0;

  answer = 1;

  return answer;
}

let stock = [4, 2];

console.log(solution(stock));
```

**[ 답안 코드 ]**

```jsx
/**
 * @param {array} stock
 * @return {int}
 */
function solution(stock) {
    var downMarks = countDownMarks(stock);
    var newArray, newDownMarks, start, end;

    // try swap
    if (downMarks.length == 1 ||
        downMarks.length == 2) {

        newArray = stock.slice(0);

        start = downMarks.shift();
        end = (downMarks.length) ? downMarks.shift() + 1 : start + 1;

        swap(newArray, start, end);
        newDownMarks = countDownMarks(newArray);
        if (!newDownMarks.length) {
            return 1;
        }
    }

    // try reverse
    if (downMarks.length > 2 &&
        downMarks.length == downMarks[downMarks.length - 1] - downMarks[0] + 1) {

        start = downMarks.shift();
        end = downMarks.pop() + 1;
        newArray = reverse(stock, start, end);
        newDownMarks = countDownMarks(newArray);
        if (!newDownMarks.length) {
            return 1;
        }
    }

    return 0
}

function swap(array, idx1, idx2) {
    var tmp = array[idx1];
    array[idx1] = array[idx2];
    array[idx2] = tmp;
}

function reverse(array, idx1, idx2) {
    return array.slice(0, idx1).concat(array.slice(idx1, idx2 + 1).reverse()).concat(array.slice(idx2 + 1));
}

function countDownMarks(array) {
    var downMarks = [];

    for (var i = 0; i < array.length - 1; i++) {
        if (array[i + 1] < array[i]) {
            downMarks.push(i);
        }
    }

    return downMarks;
}
```

---

## 9. Identity

(0.4 / 1.0)

**[ 문제 설명 ]**

저희는 인증시스템을 구현하라는 역할을 부여받고, 개발 중에 있습니다.

도중에, 악성 가입유저들이 중복해서 가입하는 것을 방지하기 위하여 동일한 패턴을 가지고 있는 아이디를 하나로 묶어 한 명의 유저로 생각하기로 했습니다.

예를 들어 [’a’, ‘b’, ‘ab’, ‘d’]가 주어졌을 경우, ‘a’라는 아이디와 ‘b’라는 아이디 그리고 ‘ab’라는 아이디가 있으면 ‘ab’와 ‘a’는 같은 아이디이고 ‘ab’와 ‘b’도 같은 아이디로 판단하는데, 그 이유는 ‘a’와 ‘ab’ 안에 같은 문자열이 존재하고, ‘b’와 ‘ab’안에 같은 문자열이 존재하기 때문에 3개의 아이디는 모두 같은 사람입니다.

또한, ‘a’와 ‘d’는 같은 사람이지 않고, ‘b’와 ‘d’, ‘ab’와 ‘d’도 마찬가지로 같은 사람이 아닙니다.

그러므로 독립적인 사람은 단 2명 존재합니다.

이렇듯 아이디의 배열이 주어질 때, 독립된 사람은 몇 명인지 저희는 판단하여 반환해야 합니다.

**[ 제한 사항 ]**

- 아이디 배열의 길이는 1 이상 1000 이하입니다.
- 아이디는 1 이상 50 이하의 문자열이며 공백일 수 없습니다.
- 아이디는 중복된 값이 배열에 존재할 수 있습니다.

**[ 입력 형식 ]**

- 아이디의 배열 identity가 주어집니다.

**[ 출력 형식 ]**

- 몇 명의 독립적으로 구분할 수 있는 사람이 존재하는지 반환해주세요.

---

**[ 제출 코드 ]**

```jsx
function solution(param0) {
  var answer = 0;

  answer = 1;

  return answer;
}

let param0 = ["a", "ac", "b", "cb"];

console.log(solution(param0));
```

**[ 답안 코드 ]**

```jsx
/**
 * @param {array} identity
 * @return {int}
 */
 function solution(identity) {
    var visited = [];
    var v = new Array(26).fill(0);
    var counter = 0;
    
    function dfs(node) {
        if(v[node]) {
            return;
        }
        
        v[node] = 1;
    
        for(var i=0;i<visited[node].length;i++) {
            var n = visited[visited[node][i]];
            
            n.forEach((x) => {
            if(v[x] === 0) {
                dfs(x);
            } 
            });
        }
    }
    
    for(var i=0; i < identity.length; i++) {
        for(var j=0; j < identity[i].length; j++) {
            var x = identity[i][j].charCodeAt(0) - 'a'.charCodeAt(0); 
            if(visited[x]) {
                visited[x].push(26 + i);
            } else {
                visited[x] = [26+i];
            }
            
            if(visited[26+i]) {
                visited[26+i].push(x);
            } else {
                visited[26+i] = [x];
            }
        }
    }
    
    for(var i=0;i<26;i++) {
        if(v[i] === 0 && visited[i]) {
            dfs(i);
            counter++;
        }
    }
    
    return counter;
}
```

---

## 10. Friend

(0.0 / 1.0)

**[ 문제 설명 ]**

SNS 서비스에는 보통 친구 추천 기능이 존재합니다.

친구 추천 기능을 구현하는 방법에는 여러가지 방식이 있는데, 가장 간단한 방법 중 하나가 친구의 친구를 추천하는 방식입니다.

즉, 아직 나와 친구가 아닌 사람들 중에서, 나의 친구 중 1명 이상과 친구인 사람을 추천하는 것입니다.

임의의 인원 수 N과 그 N명 사이의 친구 관계가 주어질 때, 위에서 설명한 것과 친구 추천 기능으로 각 사람들이 몇명을 추천받는지 계산하는 함수, solution을 완성해주세요.

**[ 입력 형식 ]**

- n은 3 이상 10 이하의 정수입니다.
- graph는 0과 1로 이루어진 n * n 크기의 2차원 배열입니다.
- graph[i][j] 가 1이면 i번 사람과 j번 사람이 서로 친구임을 나타내고, 0이면 친구가 아님을 나타냅니다.
- graph[i][i] 는 항상 0 입니다.
- 가능한 모든 (i, j) 쌍에 대해서 graph[i][j] == graph[j][i] 를 만족합니다.

**[ 출력 형식 ]**

- i번 index에 i번 사람이 추천 받는 사람 수를 담은 1차원 배열을 출력합니다.

---

**[ 제출 코드 ]**

```jsx
function solution(n, graph) {
  var answer = [];

  return answer;
}

let n = 4;
let graph = [
  [0, 1, 0, 1],
  [1, 0, 1, 0],
  [0, 1, 0, 1],
  [1, 0, 1, 0],
];

console.log(solution(n, graph));
```

**[ 답안 코드 ]**

```jsx
/**
 * 
 * @param n {number}
 * @param graph {number[][]} 
 * @return {number[]}
 */
function solution(n, graph) {
    return new Array(n).fill(0).map((_, idx) => bfs(n, idx, graph));
}

function bfs(n, start, graph) {
    let que = [];
    let que_front = 0;

    let dist = new Array(n).fill(-1);

    que.push(start);
    dist[start] = 0;

    while (que_front < que.length) {
        let here = que[que_front];
        que_front += 1;

        for (let i = 0; i < n; i++) {
            if (graph[here][i] === 0 || dist[i] !== -1) {
                continue;
            }

            dist[i] = dist[here] + 1;

            if (dist[i] < 2) {
                que.push(i);
            }
        }
    }

    return dist.filter(it => it === 2).length;
}

console.log(solution(10,[[0, 1, 1, 0, 1, 0, 0, 1, 0, 1], [1, 0, 0, 0, 1, 0, 0, 1, 1, 1], [1, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 1, 0, 1, 1, 1, 1], [1, 1, 0, 1, 0, 1, 1, 1, 1, 0], [0, 0, 0, 0, 1, 0, 1, 1, 1, 0], [0, 0, 0, 1, 1, 1, 0, 0, 1, 0], [1, 1, 0, 1, 1, 1, 0, 0, 0, 0], [0, 1, 0, 1, 1, 1, 1, 0, 0, 0], [1, 1, 0, 1, 0, 0, 0, 0, 0, 0]]))
```