---
layout: post
title: "[TS] 타입 앨리어스"
subtitle: "[TS] 타입 앨리어스"
date: 2022-08-22 03:25
categories:
  - devlog
tag: [typescript, study, zerobase, frontend]
image:
  path: ../../../assets/img/tslogo.png
---

# [TS] 타입 앨리어스

**TypeScript**가 아름답고 강력한 이유는 첫번째로 **Type Alias**가 가능하기 때문이다. 

타입 앨리어스는 타입 별칭이라고 부르는데 기본적인 타입 정의부터 시작해서 굉장히 복잡하고 재밌는 타입들을 정의해 볼 수 있다.

실제로 새로운 타입을 만드는 것이 아니라 그 **타입을 나타내는 새로운 이름을 만드는 것**이다.

타입으로 사용할 수 있다는 점에서 타입 앨리어스는 인터페이스와 유사한 면이 존재한다.

정의 방법은 다음과 같다.

```tsx
type 별칭 = 타입;
```

인터페이스는 다음과 같이 타입으로 사용할 수 있는데, 타입 앨리어스 또한 마찬가지로 타입으로 사용할 수 있다.

```tsx
// 인터페이스
interface Person {
	name: string,
	age: number
}

const ps = {} as Person;
ps.name = 'Kim';
ps.age = 23;
ps.address = 'Daegu'; // Error 발생

// 타입 앨리어스
type Person {
	name: string,
	age: number
}

const ps = {} as Person;
ps.name = 'Kim';
ps.age = 23;
ps.address = 'Daegu'; // Error 발생
```

하지만, 타입 앨리어스는 원시값, 유니온 타입, 튜플 등도 타입으로 지정할 수 있다.

```tsx
// 문자열 리터럴로 타입 지정하기
type Str = 'Kim';

// 유니온 타입으로 타입 지정하기
type Union = string | null;

// 문자열 유니온 타입으로 타입 지정하기
type Name = 'Kim' | 'Park';

// 숫자 리터럴 유니온 타입으로 타입 지정하기
type Num = 1 | 2 | 3 | 4 | 5;

// 객체 리터럴 유니온 타입으로 타입 지정하기
type Obj = {a: 1} | {b: 2};

// 함수 유니온 타입으로 타입 지정하기
type Func = (() => string) | (() => void);

// 인터페이스 유니온 타입으로 타입 지정하기
type Shape = Square | Rectangle | Circle;

// 튜플로 타입 지정하기
type Tuple = [string, boolean];
const tp: Tuple = ['', '']; // Error 발생
```

인터페이스는 **extends**나 **implements**될 수 있지만, 타입 앨리어스는 **extends**나 **implements**될 수 없다. 또한, 인터페이스는 어디서나 사용할 수 있는 새로운 이름을 만들 수 있지만, 타입 앨리어스는 새로운 이름을 만들 수 없다.