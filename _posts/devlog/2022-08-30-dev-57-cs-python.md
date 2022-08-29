---
layout: post
title: "[CS] 파이썬"
subtitle: "[CS] 파이썬"
date: 2022-08-30 02:39
categories:
  - devlog
tag: [cs, backend, zerobase]
image:
  path: ../../../assets/img/cs.jpg
---

# [CS] 파이썬

## 1. 파이썬 자료형

**파이썬 자료형 (데이터를 담는 그릇)**

### 리스트 (List)

- x = [”a”, “b”, “c”, “d”, “e”]
- **대괄호([])로 감싸고, 각 요소들 사이에 콤마가 들어간다.**

### 튜플 (Tuple)

- t = (”a”, “b”, “c”, “d”, “e”)

**리스트형은 요소값 수정이 가능(mutable)하나 튜플은 불가능(불변, immutable)**

### 딕셔너리형 (Dict)

- x = {”name”: “kim”, “age”: “23”, “country”: “korea”}
- **중괄호({}) 안에 key와 value로 구성되어 있는 형태**
- **키 값은 중복이 안된다.**

### 집합형 (Set)

- x = set([5, 2, 1])
- 집합(set)은 순서가 없고, 인덱스가 없는 모음 ⇒ **순서를 갖지 않는다.** (Unordered)
- **중복을 허용하지 않는다.** ⇒ 중복된 값이 입력되면 제거

---

## 2. continue, break 차이

**둘다** **반복문 (for, while)에서 사용**

### continue

- **반복되는 문장에서 해당 조건에서 건너뛰고 싶을 때 사용한다.**

```python
for i in range(10):
	if 3 <= i <= 5:
		continue
	print(i)
```

### break

- **반복문을 멈추고 싶을 때 사용한다.**

```python
for i in range(6):
	if i == 3:
		break
	print(i)
```

---

## 3. __**init__ 메서드 역할**

- __init__ 를 **초기화 함수**라고 부른다.
- 인스턴스화를 실시할 때 **가장 먼저 호출**되는 함수이다.
- **첫 번째 인수를 self로 지정**해야 하는 특징이 존재한다.

```python
class Info():
	def __init__(self, country, rank):
		self.country = country
		self.rank = rank
```

---

## 4. Lambda와 def의 차이점

- **Lambda와 def 모두 함수를 정의하는 방식이다.**
- **람다는 실행 시 해당 변수를 참조한다.** 변수 참조가 실행시점이라는 뜻.

```python
add_lambda = lambda a, b: a + b

def add_def(x, y):
	return x + y

print(add_lambda) # <function <lambda> at 0x7fbd87f424d0>
print(add_def) # <function add_def at 0x7ff2ce95f950>
```