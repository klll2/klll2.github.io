---
layout: post
title: "[TS] 타입 가드"
subtitle: "[TS] 타입 가드"
date: 2022-08-26 22:48
categories:
  - devlog
tag: [typescript, zerobase, frontend]
image:
  path: ../../../assets/img/tslogo.png
---

# [TS] 타입 가드

타입을 좁혀내기 위한 과정

## typeof

피연산자의 평가 전 **자료형을 나타내는 문자열을 반환한다.**

```tsx
console.log(typeof 42); // expected output: "number"
console.log(typeof 'blubber'); // expected output: "string"
console.log(typeof true); // expected output: "boolean"
console.log(typeof undeclaredVariable); // expected output: "undefined"
```

**JavaScript**에서 이미 존재하는 타입 검사 연산자이다.

```tsx
function print(value: number | string): string {
	if (typeof value === 'number') {
		return value // 에러 발생
	}

	if (typeof value === 'string') {
		return value
	}

	// undefined인 경우일 수도 있기 때문에 기입하지 않으면 에러 발생
	return value
}
```

## in

**명시된 속성이 명시된 객체에 존재하면 true를 반환한다.**

```tsx
속성 in 객체명
```

사용 예제는 다음과 같다.

```tsx
interface Dog {
	name: string,
	bark(): '멍멍'
}

interface Cat {
	name: string,
	meow(): '냐옹'
}

function sayAnimal(animal: Dog | Cat) {
	if ('bark' in animal) {
		animal.bark()
		animal.name
		animal.meow() // 에러 발생
	}
	
	if ('meow' in animal) {
		animal.meow()
	}
	
	animal.name // 에러 발생
}
```

## instanceof

**생성자의 prototype 속성이 객체의 프로토타입 체인 어딘가에 존재하는지 판별한다.**

```tsx
function Car(make, model, year) {
	this.make = make;
	this.model = model;
	this.year = year;
}

const auto = new Car('Honda', 'Accord', 1998);

console.log(auto instanceof Car); // expected output: true
console.log(auto instanceof Object); // expected output: true
```

**instanceof 연산자는 object의 프로토타입 체인에 constructor.prototype이 존재하는지 판별한다.**

```tsx
// 생성자 정의
function C(){}
function D(){}

var o = new C();

o instanceof C; // true, 왜냐하면 Object.getPrototypeOf(o) === C.prototype
o instanceof D; // false, 왜냐하면 D.prototype이 o 객체의 프로토타입 체인에 없음

o instanceof Object; // true, 왜냐하면
C.prototype instanceof Object; // true

C.prototype = {};
var o2 = new C();

o2 instanceof C; // true

o instanceof C; // false, 왜냐하면 C.prototype이 더 이상 o의 프로토타입 체인에 없음

D.prototype = new C(); // C를 D의 [[Prototype]] 링크로 추가
var o3 = new D();
o3 instanceof D; // true
o3 instanceof C; // true, 왜냐하면 이제 C.prototype이 o3의 프로토타입 체인에 존재
```

## 사용자 정의 타입 가드

**매개변수 is 타입** 을 통해 타입가드를 활용할 수 있다.

```tsx
// 다음과 같은 양식으로 작성한다.
function isDate(date: Date | string): 매개변수 is 타입 {
	return date instanceof Date
}

function isDate(date: Date | string): date is Date {
	return date instanceof Date
}

function getDate(date: Date | string): Date {
	if (isDate(date)) {
		return date
	}

	return new Date(date)
}

// ---

interface Dog {
	name: string,
	bark(): '멍멍'
}

interface Cat {
	name: string,
	meow(): '냐옹'
}

function isDog(animal: Dog | Cat): animal is Dog {
	return 'bark' in animal
}

function isCat(animal: Dog | Cat): animal is Cat {
	return 'meow' in animal
}

function sayAnimal(animal: Dog | Cat) {
	if (isDog(animal)) {
		animal.bark()
		animal.name
	}

	if (isCat(animal)) {
		animal.meow()
	}
}
```