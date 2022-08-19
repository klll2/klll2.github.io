---
layout: post
title: "[코테] 1주차 오답노트"
subtitle: "[코테] 1주차 오답노트"
date: 2022-08-19 23:40
categories:
  - devlog
tag: [codingtest, zerobase]
image:
  path: ../../../assets/img/algorithm/algorithm.jpg
---

# [코테] 1주차 오답노트

> 1주차 코딩테스트 중 아쉬게 틀린 문제 다시 풀어보기
> 

## 6. Maze(2)

(0.6 / 1.0)

**[ 문제 설명 ]**

제로와 베이스는 코로나가 끝나 오랜만에 해외로 놀러가서, 그 지역 유명 관광명소인 미로에 갔습니다. 미로는 N개의 방이 존재했고, M개의 일방통행 할 수 있는 길이 존재했습니다.

방은 1번부터 시작하여 N번까지 번호가 붙여져 있고, 저희는 주어진 S위치에서 경로를 찾기 시작합니다. M개의 길은 각각의 방을 일방통행으로만 연결하고 있습니다.

다만, 제로와 베이스는 같은 출발지에서 시작하지만 서로 다른 경로로 미로를 탈출하고 싶었습니다.

도착지는 출발지를 제외한 1번부터 N번 사이의 임의의 지점이고, 저희가 아무 곳이나 선택해도 상관없습니다. 각각의 루트에서는 한번 지나온 지점을 다시 지나갈 수는 없고, 가장 짧은 경로를 찾지 않아도 됩니다. 또한, 출발지와 도착지를 제외하고서 제로가 지나갔던 방을 베이스가 지나갈 수 없고, 베이스가 지나갔던 방을 제로가 지날 수 없습니다.

이 때, 저희는 제로와 베이스가 갈 수 있는 서로 다른 두 경로를 찾아주어야 합니다. 찾을 수 있다면 “YES”를 찾을 수 없다면 “NO”를 반환해주세요.

**[ 제한 사항 ]**

- N은 2 이상 10000 이하입니다.
- M은 0 이상 10000 이하입니다.
- S는 1 이상 N 이하입니다.

**[ 입력 형식 ]**

- 방의 개수 N과 방과 방 사이를 연결하는 일방통행로 M의 개수 그리고 출발지 S가 주어지고, 방을 연결하는 정보인 maps 배열이 주어집니다.

**[ 출력 형식 ]**

- 조건을 만족하는 서로 다른 두 경로를 찾을 수 있다면 “YES” 찾을 수 없다면 “NO”를 반환해주세요.

---

**[ 제출 코드 ]**

```jsx
function solution(N, M, S, maps) {
  var answer = "";

  let startPoint = S;

  return answer;
}

solution(5, 5, 1, [
  [1, 2],
  [2, 3],
  [1, 4],
  [4, 3],
  [3, 5],
]);
```

**[ 답안 코드 ]**

```jsx
/**
 * @param {int} n
 * @param {int} m
 * @param {int} s
 * @param {array} maps
 * @return {string}
 */
function solution(n, m, s, maps) {
    s = s - 1;
    const edges = [];
 
    for (let idx = 0; idx < m; idx++) {
        const [u, v] = maps[idx];
    
        edges.push([u - 1, v - 1]);
    }

    let map = new Map();
    const g = Array.from({
        length: n
    }, () => []);

    for (let [u, v] of edges) {
        g[u].push(v);
    }
   
    for (let child of g[s]) {
        let tmp = new Map([[child, s]]);
        const queue = [child];
    
        for (let node of queue) {
            if (map.has(node)) {
                return 'YES';
            }
    
            for (let c of g[node]) {
                if (c === s) continue;
                if (tmp.has(c)) continue;
                tmp.set(c, node);
                queue.push(c);
            }
        }
   
        for (let [child, node] of tmp) {
            map.set(child, node);
        }
    }
   
    return 'NO';
}
```

---

## 7. Perfect

(0.0 / 1.0)

**[ 문제 설명 ]**

제로는 어느날 길을 걷다가 a와 b로만 이루어진 세계로 워프했습니다.

문자열 알고리즘을 풀어야 원래의 세계로 돌아갈 수 있는 미션이 주어지고, 이를 해결해야합니다.

문자열 알고리즘은 a와 b로 이루어진 문자열 중 n개의 문자열을 a는 b로, b는 a로 변경하여 만들 수 있는 최장 부분 문자열을 알아내고 싶습니다.

최장 부분 문자열이란 ‘aaaaabbbb’와 같은 문자열이 있을 때, 최장 부분 문자열의 후보가 될 수 있는 경우는 ‘aaaaa’와 ‘bbbb’이고, ‘aaaaa’가 같은 ㅁ누자로 이루어진 가장 긴 문자열입니다. 고로 ‘aaaaabbbb’의 최장 부분 문자열은 ‘aaaaa’입니다.

또, ‘abbbaababa’일 경우 후보가 될 수 있는 문자열은 ‘bbb’와 ‘aa’, ‘a’, ‘b’ 4가지가 존재하고 여기서 같은 문자로 이루어진 가장 긴 문자열인 최장 부분 문자열은 ‘bbb’입니다.

이런 경우에 n개의 문자열을 a는 b로, b는 a로 변경하여 만들 수 있는 문자열 중 최장 부분 문자열의 길이를 반환해주세요.

예를 들면 ‘abab’라는 문자열이 주어졌고 n=2인 상황이 있다면, 저희는 a 2개를 b로 바꾸던지, b 2개를 a로 바꾸어서 ‘aaaa’ 혹은 ‘bbbb’ 문자열로 변경할 수 있고 최장 부분 문자열의 길이는 4이기 때문에 4를 반환해주면 됩니다.

**[ 제한 사항 ]**

- n은 1 이상 100,000 이하이고, 문자열의 길이는 0 이상 n 이하입니다.

**[ 입력 형식 ]**

- 변경할 수 있는 문자열의 개수 n과 문자열 ab가 주어집니다.

**[ 출력 형식 ]**

- 주어진 문자열 k의 최장 부분 문자열의 길이를 출력해주세요.

---

**[ 제출 코드 ]**

```jsx
function solution(n, ab) {
  var answer = 0;

  let length = [];

  let lengthCount = 0;
  let tmp = "a";
  for (let i of ab) {
    if (i == tmp) {
      lengthCount++;
    } else {
      length.push(lengthCount);
      lengthCount = 1;
      tmp = i;
    }
  }
  length.push(lengthCount);

  let max = 0;

  for (let i = 0; i < length.length - 2; i++) {
    // console.log(length[i] + length[i + 1] + length[i + 2]);
    let tmp = 0;
    for (let j = 0; j < n * 2 + 1; j++) {
      tmp += length[i + j];
    }
    if (max < tmp) max = tmp;
  }

  answer = max;

  return answer;
}

solution(2, "aabaabaa");
```

**[ 답안 코드 ]**

```jsx
/**
 * @param {int} n
 * @param {string} ab
 * @return {int}
 */
function solution(n, ab) {
    let i = 0, j = 0, maxlen = 0;
    let count_a = 0, count_b = 0;
 
    while (j < ab.length) {
 
        if (ab[j] == 'a')
            count_a++;
        else
            count_b++;
 
        if (i < j && count_a > n && count_b > n) {
            if (ab[i] == 'a') count_a--;
            else count_b--;
            i++;
        }
 
        j++;
        maxlen = Math.max(maxlen, j - i);
    }
 
    return maxlen;
}
```

---

## 8. Transform

(0.6 / 1.0)

**[ 문제 설명 ]**

문자열이 하나 주어지고, 이 문자열은 ‘x’와 ‘y’ 그리고 ‘z’로만 이루어져 있는 문자열입니다.

이 문자열을 저희가 목표로 하는 문자열로 바꾸고 싶은데, 바꿀 때 규칙이 존재합니다.

‘xy’ 문자열은 ‘yx’로 바꿀 수 있고, ‘yz’ 문자열은 ‘zy’로 바꿀 수 있습니다.

이 때, 문자열 두 개가 주어지고 처음 주어진 문자열 ‘ini’를 바꾸고 싶은 문자열 ‘trans’로 바꿀 수 있는지 여부를 반환해주세요.

예를 들어 ini = ‘xyyxyz’ 로 주어지고 trans = ‘yyxxzy’이라면, 저희는 다음과 같은 순서로 이 문자를 바꿀 수 있습니다.

‘xy’yxyz → ‘yx’yxyz / y’xy’xyz → y’yx’xyz / yyxx’yz’ → yyxx’zy’ 로 3번에 걸쳐 바꾸면, trans와 같아지게 됩니다. 이 경우 문자열을 목표한 trans로 바꿀 수 있기 때문에 ‘YES’를 반환해주시면 되고, 만약 불가능할 경우 ‘NO’를 반환해주시면 됩니다.

**[ 제한 사항 ]**

- 문자열은 1 이상 100,000 이하의 길이를 가지고 있고 항상 x, y, z 로만 이루어져 있습니다.

**[ 입력 형식 ]**

- 원래의 문자열 ini와 바뀌어야 하는 문자열 trans가 주어집니다.

**[ 출력 형식 ]**

- ini를 trans로 바꿀 수 있다면 ‘YES’를 반환, 아니라면 ‘NO’를 반환해주세요.

---

**[ 제출 코드 ]**

```jsx
function solution(ini, trans) {
  var answer = "YES";

  return answer;
}

function justice(ini, trans) {
  let bool = true;
  for (let i = 0; i < ini.length(); i++) {
    if (ini.charAt(i) == trans.charAt(i)) continue;
    else {
      bool = false;
      break;
    }
  }

  return bool;
}

solution("x", "y");
```

**[ 답안 코드]**

```jsx
/**
 * @param {string} ini
 * @param {string} trans
 * @return {string}
 */
 function solution(ini, trans) {
    let i = 0;
    let j = 0;

    while (i < ini.length || j < trans.length) {
        while (ini[i] == "y") i++;
        while (trans[j] == "y") j++;

        if ((i == ini.length || j == ini.length) && i != j) return "NO";
        if (ini[i] !== trans[j]) return "NO";
        if (ini[i] == "x" && i > j) return "NO";
        if (ini[i] == "z" && i < j) return "NO";

        i++;
        j++;
    }

    return "YES";
}
```

---

## 9. Messenger

(0.0 / 1.0)

**[ 문제 설명 ]**

제주도에 있는 제로는 저희와 메신저를 통해서 연락을 하려고 합니다.

제로와 저희가 사용하고 있는 메신저는 제로가 직접 만든 메신저여서 w를 uu로 보내고, m을 nn을 ㅗ보내는 버그가 존재합니다.

버그를 잡는 것이 중요한데, 제로는 버그를 잡을 생각이 없어 보입니다.

그래서 저희는 제로가 메시지를 보냈을 때, 버그를 고려하여 원래 보내려던 메세지의 가능한 가짓수를 생각해보기로 했습니다.

만약 제로가 보낸 메세지가 ‘bannauua’라면, [’bannauua’, bamauua’, ‘bammawa’, ‘bamawa’]  4가지의 경우의 수가 존재합니다.

이 때 저희는 숫자 4를 반환해주면 됩니다.

**[ 제한 사항 ]**

- message의 길이는 1 이상 100,000 이하입니다.
- message에는 알파벳 소문자만 존재합니다.

**[ 입력 형식 ]**

- 문자열 ‘message’가 입력으로 주어집니다.

**[ 출력 형식 ]**

- 주어진 문자열에서 버그를 고려하여 원래 보내려던 메세지의 가능한 가짓수를 반환해주세요.

---

**[ 제출 코드 ]**

```jsx
function solution(message) {
  var answer = 0;
  let count = 0;

  let prev;

  for (let i of message) {
    if (!prev) {
      prev = i;
      continue;
    }
    if (prev == "u" && i == "u") {
      count++;
    } else if (prev == "n" && i == "n") {
      count++;
    }

    prev = i;
  }

  answer = Math.pow(count, 2);
  console.log(answer);

  return answer;
}

solution("nnn");
```

**[ 답안 코드 ]**

```jsx
/**
 * @param {string} message
 * @return {int}
 */
function solution(message) {
    const dp = [1]; dp[-1] = 1;
    
    for (let i = 1; i < message.length; i++) {
        dp[i] = dp[i-1];
        if (message[i] == message[i-1] && (message[i] == 'u' || message[i] == 'n')) { 
            dp[i] = dp[i] + dp[i-2];
        }
    }
 
    return dp[message.length-1];
}
```

---

## 10. Palette

(0.0 / 1.0)

**[ 문제 설명 ]**

제로는 x축과 y축이 존재하는 2차원 평면에서 좌표가 주어지면 그 좌표를 색칠하라는 임무를 받았습니다. 좌표는 (x, y)의 형태로 주어지고 같은 좌표는 주어지지 않습니다. 두 개의 다른 좌표 사이의 거리는 𝑑(𝑖,𝑗) | 𝑥𝑖 − 𝑥𝑗 | − | 𝑦𝑖 − 𝑦𝑗 | 로 구할 수 있습니다.

각 좌표에서 제로는 1부터 n 사이로 대표되는 색을 선택하여서 색을 좌표에 칠해야 합니다. 다만 색칠하는 데에는 2가지 조건이 필요합니다.

첫 번째 조건은 세 좌표를 선택했을 때, 세 좌표의 색이 모두 같다면 모든 좌표 사이의 거리는 같아야 한다는 점입니다. 세 좌표가 (a, b, c)라고 할 때, d(a, b) = d(a, c) = d(b, c)의 조건을 만족해야 합니다.

또, 두 번째 조건은 세 좌표를 선택했을 때, 두 좌표의 색이 같고 나머지 한 좌표가 색이 다르다면 같은 두 좌표의 거리가 나머지 한 좌표와의 거리보다 작아야 한다는 점입니다. 이를 식으로 표현하면 d(a, b) < d(a, c) 그리고 d(a, b) < d(b, c)입니다. 여기서 a와 b가 같은 색으로 표현되고, c가 다른 색으로 표현됩니다.

좌표들이 배열로 주어지면, 여기에서 위 조건을 만족하는 경우의 수가 몇 개인지 반환해주세요. 만약 세 좌표의 색이 모두 다르거나, 주어진 전체 좌표가 두 개라면 조건을 만족할 필요는 없어서 가능한 색 조합을 모두 구해주시면 됩니다. 또한 결과를 998244353로 mod 연산하여 반환해주세요.

예를 들어, 좌표가 [[1, 0], [3, 0], [2, 1]]으로 주어졌을 경우 색칠이 가능한 경우의 수는 [1, 1, 1], [2, 2, 2], [3, 3, 3], [1, 2, 3], [1, 3, 2], [2, 1, 3], [2, 3, 1], [3, 1, 2], [3, 2, 1]으로 총 9가지입니다.

**[ 제한 사항 ]**

- 좌표의 개수는 2개 이상 100개 이하입니다. 또한 좌표들은 모두 다른 좌표를 가지고 있습니다.

**[ 입력 형식 ]**

- 좌표 maps이 주어집니다.

**[ 출력 형식 ]**

- 색칠할 수 있는 모든 경우의 수를 고려하여 반환해주세요. 또한 결과를 998244353로 mod 연산하여 반환해주세요.

---

**[ 제출 코드 ]**

```jsx
function solution(maps) {
  var answer = 0;

  return answer;
}
```

**[ 답안 코드]**

```jsx
/**
 * @param {array} maps
 * @return {int}
 */
function solution(maps) {
    const f = [1];
    const n = maps.length;
    for (let i = 1; i <= n; i++) {
        f[i] = mul(f[i - 1], i);
    }
    const edges = [];
    const dis = (i, j) => Math.abs(maps[i][0] - maps[j][0]) + Math.abs(maps[i][1] - maps[j][1]);
    for (let i = 0; i < n - 1; i++) {
        for (let j = i + 1; j < n; j++) {
            const d = dis(i, j);
            edges.push([i, j, d]);
        }
    }
    edges.sort((a, b) => a[2] - b[2]);
    const st = [];
    const check = arr => {
        if (arr.length > 4) return false;
        let t = -1;
        for (let i = 0; i < arr.length; i++) {
            if (st[arr[i]]) return false;
            for (let j = i + 1; j < arr.length; j++) {
                if (st[arr[j]]) return false;
                if (t == -1) t = dis(arr[i], arr[j]); else if (t !== dis(arr[i], arr[j])) return false;
            }
        }
        return true;
    };
    const pos = [];
    for (let i = 0, j = 0; i < edges.length; i = ++j) {
        while (j + 1 < edges.length && edges[i][2] === edges[j + 1][2]) {
            j++;
        }
        const uf = new UnionFind(n);
        for (let k = i; k <= j; k++) {
            const [u, v] = edges[k];
            uf.union(u, v);
        }
        const groups = [...uf.group().values()];
        pos.push(...groups.filter(check));
        for (let k = i; k <= j; k++) {
            const [u, v] = edges[k];
            st[u] = 1;
            st[v] = 1;
        }
    }
    let p2 = 0,
        p3 = 0,
        p4 = 0;
    for (let arr of pos) {
        if (arr.length === 2) p2++; else if (arr.length === 3) p3++; else p4++;
    }
    let res = 0;
    const ff = [1n];
    for (let i = 1; i <= n; i++) {
        ff[i] = ff[i - 1] * BigInt(i);
    }
    [0, 0, pos.filter(arr => arr.length === 2).length, pos.filter(arr => arr.length === 3).length, pos.filter(arr => arr.length === 4).length];
    const c = (i, n) => mul(f[n], mul(power(f[i], MOD - 2), power(f[n - i], MOD - 2)));
    for (let i = 0; i <= p2; i++) {
        for (let j = 0; j <= p3; j++) {
            for (let k = 0; k <= p4; k++) {
                const N = n - i - j * 2 - k * 3;
                res = mod(res + mul(f[N], c(i, p2), c(j, p3), c(k, p4), c(N, n)));
            }
        }
    }
    return mod(res);
}

const MOD = 998244353;
const mod = num => (num % MOD + MOD) % MOD;

function power(a, b) {
    let res = 1;
    while (b) {
        if (b & 1) res = mul(res, a);
        a = mul(a, a);
        b = b >> 1;
    }
    return res;
}

function mul(...args) {
    if (args.length === 1) return args[0];
    if (args.length > 2) return mul(args[0], mul(...args.slice(1)));
    const [a, b] = args;
    return ((a >> 16) * b % MOD * 65536 + (a & 65535) * b) % MOD;
}

function _defineProperty(obj, key, value) {
    if (key in obj) {
        Object.defineProperty(obj, key, {
            value: value,
            enumerable: true,
            configurable: true,
            writable: true
        });
    } else {
        obj[key] = value;
    }

    return obj;
}

class UnionFind {
    constructor(n) {
        _defineProperty(this, "vis", []);
        this.n = n;
        this.p = [...new Array(n).keys()];
    }

    union(i, j) {
        this.vis[i] = this.vis[j] = 1;
        const [rooti, rootj] = [this.find(i), this.find(j)];
        if (rooti === rootj) return;
        this.p[rootj] = rooti;
    }

    find(i) {
        const {
            p
        } = this;
        while (i !== p[i]) {
            p[i] = p[p[i]];
            i = p[p[i]];
        }
        return i;
    }

    group() {
        const groups = new Map();
        for (let i = 0; i < this.n; i++) {
            var _groups$get;
            if (!this.vis[i]) continue;
            const root = this.find(i);
            if (!groups.has(root)) groups.set(root, []);
            (_groups$get = groups.get(root)) === null || _groups$get === void 0 ? void 0 : _groups$get.push(i);
        }
        return groups;
    }
}
```