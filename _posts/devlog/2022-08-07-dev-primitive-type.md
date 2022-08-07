---
layout: post
title: "[TS] 기본 타입"
subtitle: "[TS] 기본 타입"
date: 2022-08-07 20:30
categories:
  - devlog
tag: [typescript, zerobase, frontend]
image:
  path: ../../../assets/img/tslogo.png
---

# [TS] 기본 타입

## Type Annotation

```tsx
/*
 *	Type Annotation
 *
 *  value: type
 */

const val: number = "123";
```

- **value:** **type** 형태 → 콜론(:)을 기준으로 좌측이 value, 우측이 type
- Type을 달 때 사용한다(?)

---

## 원시 타입

```tsx
/*
 * Primitive (원시값)
 */
const str: string = "String";
const num: number = 123;
const bool: boolean = true;
const big: bigint = 100n;

// 이와 같은 형태도 가능하다
// 문자열의 경우, 소문자로 넣어야 인정됨
// 숫자의 경우 또한 동일한 값을 넣어줘야 됨
// boolean 값 또한 동일한 값을 넣어줘야 됨
const str: "string" = "string";
const num: 123 = 123;
const bool: true = true;

// 타입 추론
const str = "string";
const num = 123;
const bool = true;
```

- 불변
- 객체가 아닌 값들

→ **Type을 달고 싶을 때는 Type Annotation을 사용하면 된다!**

---

## 객체 타입

```tsx
/*
 * Object Type
 */

const obj: object = {
  str: "str",
  num: 123,
  child: {
    str: "str",
    num: 123,
  },
};

obj.str.trim(); // error 발생
```

- **any**와 다를게 없는 상황

```tsx
const obj2: {
  str: string;
  num: number;
  child: {
    str: string;
    num: number;
  };
} = {
  str: "str",
  num: 123,
  child: {
    str: "str",
    num: 123,
  },
};

obj2.str; // 정상
```

- 이와 같은 방식이면 type을 안전하게 달고(?) 사용할 수 있다.

---

## 함수 타입

```tsx
/*
 * Function Type
 */

function func(num: number, str: string) {
  return num + str;
}

func("str", 123); // error 발생
func(123, "str"); // 정상
```

- 함수는 매개변수( () ), 반환 ( return ) 을 명시해주어야 한다.
- 9번 라인의 경우, 매개변수가 잘못되었기에 error가 발생한다.

```tsx
function func(num: number, str: string): void {
  // return
}
```

- 반환 타입으로 void를 명시해주면 return 값을 주면 안된다.

```tsx
function func(num: number, str: string): string {
  return num + str;
}
```

- 이와 같이 **string**을 명시해주면 문제 없이 반환된다.

```tsx
function func(num1: number, str: string): number {
  return num1 + str; // error 발생
}
```

- 반환 타입이 **number** 인데 반해, return 값이 **string**이기 때문

이러한 경우에는

```tsx
function func(num1: number, str: string): number {
  return num1 + Number(str);
}

func(123, 123);
```

- 형변환을 시켜주면 정상적으로 작동한다.

```tsx
function func(num1: Function, num2: Function): Function {
  console.log(num1 + num2);
}
```

- **이와 같이 단순하게 Function이라고만 다는 것은 지양하기**

**함수 표현식**의 경우에는 다음과 같이 나타낸다.

```tsx
// 함수 표현식
const func = (str1: string, str2: string): string => {
  return str1 + " " + str2;
};
```

**객체 타입** 또한 받을 수 있다.

```tsx
// 객체 타입
const func = (obj: { str1: string; str2: string }) => {
  return obj.str1 + " " + obj.str2;
};
```

### 결론

- **매개변수와 반환값 모두 타입을 명시할 수 있다.**
- **return 값의 경우, 타입 추론이 잘되기 때문에 꼭 type을 지정해야만 하는 것은 아니다! 하지만, 매개변수는 type을 지정해주는 것을 권장한다!**

---

## 배열 타입

```tsx
/*
 * Array Type
 */

// String Array
const strArr: string[] = ["str", "str2", "str3"];
const strArr2: Array<string> = ["str", "str2", "str3"];

// number Array
const numArr: Array<number> = [1, 2, 3];

// boolean Array
const boolArr: boolean[] = [false, true, false, true];

// 동작 X
strArr.push(1);
numArr.push("str");

// 정상 동작
boolArr.push(false);

// Tuple로
const arr = ["str", 123, false];
```

- 6, 7번 라인과 같이 표현 방식에 2가지 방법이 있다.
- 타입에 맞지 않는 값을 삽입하려 하면 동작하지 않는다.

---

## 리터럴 타입

```tsx
/*
 * Literal Type
 */

let letString = "Hello"; // string
const constString = "Hello"; // "Hello"

let letNumber = 123;
const constNumber = 123;
```

- letString의 경우에는 **string**, constString의 경우에는 **“Hello”** 으로 선언이 되어 있다.
- type이 number인 경우에도 동일한데 이러한 이유로는 let으로 선언된 경우 값이 재할당이 가능하기 때문이다.
- 안전한 애플리케이션을 만들 때 유용하다.

---

## 튜플 타입

```tsx
/*
 * Tuple Type
 */

// 기존의 배열 타입
const arr: string[] = ["A", "B", "C"];

const tuple: [number, string] = [1, "A"]; // 길이와 타입이 고정
const tuple2: [number, ...string[]] = [0, "A", "B"]; // 튜플의 길이를 가변적으로 바꿀 수 있다.
```

- 배열 타입의 경우, 타입을 제한하여 안전하게 사용할 수 있지만, 다른 타입이 들어올 수 없다는 단점 또한 존재한다.
- 길이 고정 & 인덱스 타입이 고정되어 다양한 타입을 안전하게 받을 수 있다.
- 여러 다른 타입으로 이루어진 배열을 안전하게 관리할 수 있다.
- 배열 타입의 길이 조절이 가능하다.

---

## undefined & null

```tsx
/*
 * undefined & null
 */

const nu: null = null;
const un: undefined = undefined;

console.log(nu == un); // 느슨한 검사, true
console.log(nu === un); // false

// return Type을 지정하지 않아도 string or (null or undefined) 값이 리턴되는 것을 알아서 추정해준다.
function sayHello(word: string) {
  if (word === "world") {
    return "hello" + word;
  }

  return null; // string or null
  return; // string or undefined
}

function log(message: string | number) {
  console.log(message);

  return undefined;
}
```

### 원시 값

- **JavaScript**에서 **원시 값**(primitive, 또는 원시 자료형)이란 객체가 아니면서 메서드도 가지지 않는 데이터이다. 원시 값에는 7종류, **string**, **number**, **bigint**, **boolean**, **undefined**, **symbol**, **null**이 존재한다.
- **TypeScript** 또한 마찬가지로 고유의 특별한 타입으로 **인정**한다.
  → 이외에 **void**, **never**와 같이 더 세밀한 타입 또한 제공한다.
- **strictNullChecks**가 핵심
- 헷갈릴 수 있기 때문에 최대한 **null**과 **undefined**는 사용하지 않는 것이 좋다.
  → 프로젝트 등에서 빈 칸을 사용하고자 한다면 **null**과 **undefined** 중 하나를 사용하는 것을 권장

---

[원시 값 - 용어 사전 | MDN](https://developer.mozilla.org/ko/docs/Glossary/Primitive)

---

## any

```tsx
/*
 * any type
 */

// 대부분의 모든 값을 수용할 수 있는 any는 지양하자
function func(anyParam: any) {
  anyParam.trim(); // error가 발생할 수 있는 상황임에도 에러 메세지가 없다. 물론, 콘솔 창에는 error가 뜬다.
}

func([1, 2, 3]);
```

- 모든 값의 집합
- any 타입을 붙이면 **TypeScript**가 아닌 **JavaScript**처럼 사용 가능하게 된다.
- **사용하지 말자**
- **noImplicitAny** or **strict 옵션 true** 권장
  → **error message**를 표시해준다.

---

## unknown

```tsx
/*
 * unknown
 */

// any의 경우, 아무런 error 메시지가 뜨지 않는다.
function func(x: any) {
  let val1: any = x;
  let val2: unknown = x;
  let val3: string = x;
  let val4: boolean = x;
  let val5: number = x;
  let val6: string[] = x;
  let val7: {} = x;
}

// val1, val2를 제외한 나머지에서 error 발생
function func(x: unknown) {
  let val1: any = x; // 정상
  let val2: unknown = x; // 정상
  let val3: string = x; // error
  let val4: boolean = x; // error
  let val5: number = x; // error
  let val6: string[] = x; // error
  let val7: {} = x; // error
}

let num: any = 99;
num.trim(); // 동작할 수 없음에도 error message가 나오지 않는다. 물론, 동작하지 않으며 콘솔창에는 error message가 나온다.

let num: unknown = 99;
if (typeof num === "string") {
  // 타입 가드, num이 string 타입일 경우 동작한다. 즉, 다음 코드는 동작하지 않는다.
  num.trim();
}
```

- 새로운 최상위 타입
- **any** 처럼 모든 값을 허용하지만, 상대적으로 엄격하다.
- **TypeScript** 에서 **unknown** 으로 추론하는 경우는 없으니 개발자가 **직접 명시**해야 한다.
- **assertion** 혹은 **타입 가드**와 함께 사용한다.

---

## void

```tsx
/*
 * void
 */

// 다음 두 코드 모두 undefined를 반환하지만 두 코드는 엄연히 다르다!
function test(): undefined {}
function test2(): void {}

function voidFunc() {} // 타입 추론으로 TypeScript에서 알아서 void로 추론해준다!
```

- 함수의 반환이 없는 경우를 명시
- **JavaScript**에서는 암시적으로 **undefined** 반환
- 그러나 **void와 undefined는 TypeScript에서 같은 것이 아니다**.
- **TypeScript에서 타입 추론을 통해 알아서 추론해주므로 타입 추론에 위임하자**

---
