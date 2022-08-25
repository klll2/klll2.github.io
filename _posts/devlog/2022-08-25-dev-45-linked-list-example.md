---
layout: post
title: "[알고리즘] 연결 리스트 문제 풀이"
subtitle: "[알고리즘] 연결 리스트 문제 풀이"
date: 2022-08-25 23:05
categories:
  - devlog
tag: [algorithm, zerobase]
image:
  path: ../../../assets/img/algorithm/algorithm.jpg
---

# [알고리즘] 연결 리스트 문제 풀이

### 선형 자료구조와 비선형 자료구조

![overview.png](../../assets/img/develop/2022-08-25-dev-linked-list-example/overview.png)

그 중에서도 선형 자료구조인 **연결 리스트** 문제들을 몇 문제 가져와서 풀어보도록 하겠다.

### 열차 연결

💡 **문제 설명**

새로운 지하철 노선이 신설되어, 이를 위한 열차가 새로 반입되었다. 하지만 이 열차들은 서로 연결되어 있지 않아 현재 운행이 어려운 상태이다. 열차 운행을 위해 열차 찻간을 이어주는 프로그램을 작성하시오. 열차 별로 고유의 식별번호가 있어, 이를 기준으로 반입된 순서대로 열차 찻간을 이어주도록 한다. 입력은 배열 형태로 열차 식별번호가 주어지며, 열차 찻간을 이어주어 Linked List 형태로 반환한다. 열차 연결 및 반환을 위해 사용해야 할 Train 객체와 Linked List 객체는 템플릿 코드를 참고한다.

⌨️ **입력 값**

**#1.** [4, 7, 1, 10, 6]

**#2.** [3, 10, 6, 9, 11, 3, 4]

**#3.** [5, 8, 7, 3, 4, 1, 2, 7, 10, 7]

🖨️ **출력 값**

**#1.** 4 → 7 → 1 → 10 → 6 → null

**#2.** 3 → 10 → 6 → 9 → 11 → 3 → 4 → null

**#3.** 5 → 8 → 7 → 3 → 4 → 1 → 2 → 7 → 10 → 7 → null

**풀이**

```jsx
function Train(number) {
  this.number = number;
  this.next = null;
}

function LinkedList() {
  this.head = null;
}

function answer(nums) {
  let ll = new LinkedList();

  // 1. Train 객체를 nums 수만큼 만들고, next를 이용해서 열차 간 연결
  // 연결 작업: 이전 Train 객체.next = 현재 Train 객체

  // 2. 가장 첫번째 Train 객체는 this.head로 연결

  let current, prev;
  for (let i = 0 ; i < nums.length ; i++) {
    current = new Train(nums[i]);

    if (i === 0) {
      ll.head = current;
    } else {
      prev.next = current;
    }

    prev = current;
  }

  return ll;
}

let input = [
  // TC: 1
  [4, 7, 1, 10, 6],

  // TC: 2
  [3, 10, 6, 9, 11, 3, 4],

  // TC: 2
  [5, 8, 7, 3, 4, 1, 2, 10, 7],
];

LinkedList.prototype.printNode = function () {
  for (let node = this.head ; node != null ; node = node.next) {
    process.stdout.write(`${node.number} -> `);
  }
  console.log("null");
};

for (let i = 0 ; i < input.length ; i++) {
  process.stdout.write(`#${i + 1} `);
  answer(input[i]).printNode();
}
```

### 서류 정리

💡 **문제 설명**

동생에게 전달해준 서류를 순서대로 서랍에 정리해달라고 부탁했더니, 서류를 반대 순서로 넣어두었다. 다시 제대로 정렬하기 위해, 이미 정리된 순서의 반대로 서류를 역 정렬시키는 프로그램을 제작하시오. 만약 서류가 1 → 2 → 3 순으로 들어가 있다면 3 → 2 → 1로 역 정렬시켜야 한다.

입력은 동생의 가공을 통해 역 정렬된 서류가 저장되어 있는 Linked List 객체가 주어지며, 포인트 조작을 통해 파일 순서만 변경하여 Linked List 객체를 반환한다.

⌨️ **입력 값**

**#1.** 1 → 3 → 7 → null

**#2.** 3 → 1 → 9 → 6 → 4 → null

**#3.** 6 → 9 → 7 → 2 → 1 → 4 → 3 → null

🖨️ **출력 값**

**#1.** 7 → 3 → 1 → null

**#2.** 4 → 6 → 9 → 1 → 3 → null

**#3.** 3 → 4 → 1 → 2 → 7 → 9 → 6 → null

**풀이**

```jsx
function File(number) {
  this.number = number;
  this.next = null;
}

function LinkedList() {
  this.head = null;
}

function answer(ll) {
  let current = ll.head,
    prev = null,
    next;
  
  // 1. 역 방향 정렬
  while (current != null) {
    next = current.next;
    current.next = prev;
    prev = current;
    current = next;
  }

  // 2. head 업데이트
  ll.head = prev;

  return ll;
}

let input = [
  // TC: 1
  [7, 3, 1],

  // TC: 2
  [4, 6, 9, 1, 3],

  // TC: 3
  [3, 4, 1, 2, 7, 9, 6],
];

LinkedList.prototype.printNode = function () {
  for (let node = this.head ; node != null ; node = node.next) {
    process.stdout.write(`${node.number} -> `);
  }
  console.log("null");
};

LinkedList.prototype.makeFiles = function (files) {
  let current = this.head;
  let node;
  for (let i = 0 ; i < files.length ; i++) {
    node = new File(files[i]);
    node.next = current;
    this.head = node;

    current = node;
  }
};

for (let i = 0 ; i < input.length ; i++) {
  process.stdout.write(`#${i + 1} `);

  let ll = new LinkedList();
  ll.makeFiles(input[i]);
  answer(ll).printNode();
}
```

### 대표 선출

💡 **문제 설명**

네카라쿠배 마을에 대표를 선출해야 한다. 모두 자신이 대표가 되고 싶어하여, 아래 규칙을 통해 대표를 선출하기로 하였다. 규칙은 먼저 원탁에 둘러 앉아 시계 방향으로 1번부터 n번까지 번호를 부여한다. 그리고 주사위를 통해 굴려 나온 숫자 m의 사람을 제외하고, 그 다음으로 나온 주사위 숫자 k만큼 이동해 가며 대표 후보에서 제외시킨다. 이렇게 순회하며 1명이 남을 때까지 반복해 마을의 대표를 선출하기로 하였다. n, m, k가 주어졌을 때 대표 후보에서 제외되는 번호를 출력해주는 프로그램을 제작하시오. 입력은 n, m, k의 자연수가 주어지며, 대표 후보에서 제외되는 번호를 순차적으로 배열로 반환한다.

⌨️ **입력 값**

**#1.** 8 2 3

**#2.** 10 2 3

**#3.** 20 5 7

🖨️ **출력 값**

**#1.** [ 2, 5, 8, 4, 1, 7, 3, 6 ]

**#2.** [ 2, 5, 8, 1, 6, 10, 7, 4, 9, 3 ]

**#3.** [ 5, 12, 19, 7, 15, 3, 13, 2, 14, 6, 18, 11, 9, 8, 10, 17, 4, 16, 20, 1 ]

**풀이**

```jsx
function Node(data) {
  this.data = data;
  this.next = null;
}

function LinkedList() {
  this.head = null;
}

function answer(n, m, k) {
  let result = [];

  // 1. Circular Linked List 제작
  let ll = new LinkedList();
  let current, prev;
  for (let i = 1 ; i <= n ; i++) {
    current = new Node(i);

    if (i === 1) {
      ll.head = current;
    } else {
      prev.next = current;
    }

    prev = current;
  }
  current.next = ll.head;

  // 2. Start node 위치 설정
  current = ll.head;
  while (--m) {
    prev = current;
    current = current.next;
  }

  // 3. 후보자들 중 k만큼 움직이면서 제거 -> 단, 혼자 남을 때
  let count;
  while (current.next != current) {
    result.push(current.data);
    prev.next = current.next;

    count = k;
    while (count--) {
      prev = current;
      current = current.next;
    }
  }

  // 4. 혼자 남은 후보 번호를 result 추가
  result.push(current.data);

  return result;
}

let input = [
  // TC: 1
  [8, 2, 3],

  // TC: 2
  [10, 2, 3],

  // TC: 3
  [20, 5, 7],
];

for (let i = 0 ; i < input.length ; i++) {
  process.stdout.write(`#${i + 1} `);
  console.log(answer(input[i][0], input[i][1], input[i][2]));
}
```