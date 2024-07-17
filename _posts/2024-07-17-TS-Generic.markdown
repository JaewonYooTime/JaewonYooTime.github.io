---
layout: post
title:  "타입스크립트 제네릭(Generics) 정리 & 예제"
date:   2024-07-17 13:33:36 +0900
categories: Typescript Generics Type
---

# 시작하며

TypeScript에서 제네릭(Generics)은 함수, 클래스, 인터페이스 등을 정의할 때 타입을 유연하고 재사용 가능하게 만드는 강력한 도구입니다. 이는 코드의 타입 안전성을 유지하면서도 다양한 타입을 처리할 수 있게 합니다. 이 블로그 글에서는 TypeScript의 제네릭 개념을 기본부터 자세히 살펴보겠습니다.

## 제네릭이란?

제네릭은 타입을 마치 함수의 매개변수처럼 다루는 방법입니다. 즉, 함수나 클래스가 사용할 타입을 외부에서 지정할 수 있게 합니다. 이를 통해 타입을 미리 고정하지 않고, 필요에 따라 동적으로 지정할 수 있습니다.

### 기본 문법

간단한 제네릭 함수 예제를 살펴보겠습니다:

```typescript
function identity<T>(arg: T): T {
    return arg;
}
```

이 예제에서 `identity` 함수는 입력 값의 타입과 동일한 타입을 반환합니다. 여기서 `T`는 타입 변수로, 함수 호출 시 실제 타입으로 대체됩니다.

```typescript
let output1 = identity<string>("myString");
let output2 = identity<number>(100);
```

### 제네릭의 역할

제네릭은 다음과 같은 역할을 합니다:
1. **타입 유연성 제공**: 다양한 타입을 처리할 수 있도록 유연성을 제공합니다.
2. **타입 안전성 보장**: 컴파일 타임에 타입 오류를 검출하여 타입 안전성을 보장합니다.
3. **코드 재사용성 향상**: 동일한 로직을 다양한 타입에 대해 재사용할 수 있습니다.

## 제네릭 함수 정의하기

### 기본 예제

제네릭 함수는 다음과 같이 정의할 수 있습니다:

```typescript
function merge<T, U>(obj1: T, obj2: U): T & U {
    return { ...obj1, ...obj2 };
}

const result = merge({ name: 'Alice' }, { age: 30 });
```

여기서 `merge` 함수는 두 개의 객체를 받아서 하나로 합칩니다. `T`와 `U`는 각각 두 객체의 타입을 나타냅니다.

### 제약 조건 추가하기

제네릭에 제약 조건을 추가하여 특정 타입에 맞게 제한할 수 있습니다. 예를 들어, 객체 타입에만 적용되도록 할 수 있습니다:

```typescript
function mergeWithConstraint<T extends object, U extends object>(obj1: T, obj2: U): T & U {
    return { ...obj1, ...obj2 };
}

const result = mergeWithConstraint({ name: 'Alice' }, { age: 30 });
```

여기서 `T`와 `U`는 객체 타입이어야 한다는 제약 조건을 가지고 있습니다.

## 제네릭 클래스 정의하기

제네릭은 클래스에서도 사용할 수 있습니다:

```typescript
class GenericNumber<T> {
    zeroValue: T;
    add: (x: T, y: T) => T;

    constructor(zeroValue: T, addFunction: (x: T, y: T) => T) {
        this.zeroValue = zeroValue;
        this.add = addFunction;
    }
}

const myGenericNumber = new GenericNumber<number>(0, (x, y) => x + y);
```

여기서 `GenericNumber` 클래스는 숫자 타입뿐만 아니라 다른 타입에도 사용할 수 있습니다.

## 함수 시그니처와 제네릭의 차이점

함수 시그니처와 제네릭은 모두 함수의 타입을 정의하는 데 사용되지만, 몇 가지 차이점이 있습니다.

### 타입 고정 vs. 타입 유연성

- **함수 시그니처**: 함수가 수락하는 매개변수와 반환 값의 타입을 고정합니다. 
  ```typescript
  function add(a: number, b: number): number {
      return a + b;
  }
  ```
  여기서 `add` 함수는 오직 숫자 타입만 처리합니다.

- **제네릭**: 함수가 다양한 타입을 처리할 수 있도록 유연성을 제공합니다.
  ```typescript
  function identity<T>(arg: T): T {
      return arg;
  }
  ```
  여기서 `identity` 함수는 문자열, 숫자 등 다양한 타입을 처리할 수 있습니다.

### 코드 재사용성

- **함수 시그니처**: 특정 타입에 대한 함수 정의가 필요합니다.
  ```typescript
  type AddFunction = (a: number, b: number) => number;

  const add: AddFunction = (a, b) => a + b;
  ```

- **제네릭**: 동일한 로직을 여러 타입에 대해 재사용할 수 있습니다.
  ```typescript
  type IdentityFunction = <T>(arg: T) => T;

  const identity: IdentityFunction = (arg) => arg;
  ```

## 결론

TypeScript의 제네릭은 타입 유연성과 코드 재사용성을 제공하는 강력한 기능입니다. 제네릭을 사용하면 다양한 타입을 처리할 수 있으며, 이를 통해 코드가 더욱 견고하고 유지보수하기 쉬워집니다. 함수, 클래스, 인터페이스 등에서 제네릭을 적절히 활용하여 TypeScript 코드를 더욱 효율적으로 작성할 수 있습니다.

### 참고 자료

- [TypeScript 공식 문서](https://www.typescriptlang.org/docs/)
- [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)