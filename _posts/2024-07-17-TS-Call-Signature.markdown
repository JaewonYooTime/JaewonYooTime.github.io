---
layout: post
title:  "타입스크립트 함수 시그니처(Call Signature) 정리 & 예제: 타입과 인터페이스에 초점"
date:   2024-07-17 13:29:14 +0900
categories: Typescript Call-Signature Type Interface
---

# 시작하며

TypeScript에서 함수 시그니처(call signature)는 함수의 형태를 정의하고 특정 계약을 준수하도록 하는 강력한 기능입니다. 이는 특히 대규모 코드베이스에서 타입 안전성과 명확성을 유지하는 데 유용합니다. 이 블로그 글에서는 TypeScript의 함수 시그니처 개념을 기본부터 자세히 살펴보겠습니다.

## 함수 시그니처란?

TypeScript에서 함수 시그니처는 함수가 수락하는 입력(매개변수)과 생성하는 출력(반환 값)의 타입을 정의하는 방법입니다. 이는 함수의 청사진으로 작동하여 이 시그니처와 일치하는 모든 함수가 동일한 매개변수 타입과 반환 타입을 가지도록 합니다.

### 기본 문법

간단한 함수 시그니처 예제를 살펴보겠습니다:

```typescript
function add(a: number, b: number): number {
    return a + b;
}
```

이 예제에서 `add`는 두 개의 숫자 매개변수 `a`와 `b`를 받아서 숫자를 반환하는 함수입니다. 여기서 함수 시그니처는 `(a: number, b: number) => number`입니다. 

함수 시그니처는 다음과 같은 부분으로 구성됩니다:
- 함수 이름: `add`
- 매개변수 목록: `(a: number, b: number)`
- 반환 타입: `: number`

### 함수 시그니처의 역할

함수 시그니처는 다음과 같은 역할을 합니다:
1. **타입 안전성 보장**: 함수가 예상된 매개변수 타입과 반환 타입을 가지도록 보장합니다.
2. **코드 명확성**: 함수가 어떤 매개변수를 받고 어떤 값을 반환하는지 명확하게 정의합니다.
3. **자동 완성 지원**: TypeScript의 타입 정보를 바탕으로 IDE에서 자동 완성 기능을 지원합니다.
4. **문서화**: 함수 시그니처 자체가 함수의 사용 방법을 설명하는 역할을 합니다.

## 함수 시그니처 정의하기

### 타입 별칭 사용하기

TypeScript에서는 타입 별칭을 사용하여 함수 시그니처를 정의할 수 있습니다. 이는 동일한 함수 시그니처를 여러 곳에서 재사용할 때 유용합니다.

```typescript
type AddFunction = (a: number, b: number) => number;

const add: AddFunction = (a, b) => a + b;
```

여기서 `AddFunction`은 두 숫자를 받아서 숫자를 반환하는 함수의 타입 별칭입니다. `add` 함수는 이 타입을 할당받습니다.

타입 별칭을 사용하면 함수 시그니처를 명확히 정의할 수 있으며, 이는 코드의 가독성과 유지보수성을 높이는 데 도움이 됩니다.

### 인터페이스 사용하기

인터페이스를 사용하여 함수 시그니처를 정의할 수도 있습니다. 이 접근 방식은 여러 메서드가 있는 객체를 다룰 때 특히 유용합니다.

```typescript
interface MathOperations {
    add: (a: number, b: number) => number;
    subtract: (a: number, b: number) => number;
}

const operations: MathOperations = {
    add: (a, b) => a + b,
    subtract: (a, b) => a - b,
};
```

이 예제에서 `MathOperations` 인터페이스는 `add`와 `subtract` 함수의 시그니처를 정의합니다. 인터페이스를 사용하면 객체의 구조를 명확히 정의할 수 있으며, 여러 메서드를 포함하는 복잡한 객체에서도 타입 안전성을 유지할 수 있습니다.

## 타입 별칭과 인터페이스의 차이점

타입 별칭과 인터페이스는 모두 TypeScript에서 타입을 정의하는 데 사용되지만, 몇 가지 차이점이 있습니다.

### 확장성

인터페이스는 확장할 수 있지만, 타입 별칭은 확장할 수 없습니다. 이는 인터페이스가 더 큰 객체나 구조를 정의하는 데 유용하다는 것을 의미합니다.

```typescript
interface BasicOperations {
    add: (a: number, b: number) => number;
}

interface AdvancedOperations extends BasicOperations {
    subtract: (a: number, b: number) => number;
}

const operations: AdvancedOperations = {
    add: (a, b) => a + b,
    subtract: (a, b) => a - b,
};
```

### 복잡한 타입 정의

타입 별칭은 유니온 타입이나 튜플 등 복잡한 타입을 정의하는 데 유용합니다.

```typescript
type StringOrNumber = string | number;
type Point = [number, number];

const value: StringOrNumber = "Hello";
const point: Point = [10, 20];
```

타입 별칭을 사용하면 다양한 타입 조합을 간단하게 정의할 수 있습니다.

## 결론

TypeScript의 함수 시그니처는 타입 안전성과 코드 명확성을 제공하는 강력한 기능입니다. 매개변수와 반환 값의 타입을 정의함으로써 함수가 특정 계약을 준수하도록 할 수 있으며, 이를 통해 코드가 더욱 견고하고 유지보수하기 쉬워집니다. 타입 별칭과 인터페이스를 활용하면 다양한 상황에서 타입을 명확하게 정의할 수 있으며, 이를 통해 TypeScript 스킬을 크게 향상시킬 수 있습니다.

### 참고 자료

- [TypeScript 공식 문서](https://www.typescriptlang.org/docs/)
- [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
