---
layout: post
title:  "TypeScript의 `readonly` 특성에 대해 알아보자"
date:   2024-07-18 23:46:47 +0900
categories: Typescript readonly
---

# 시작하며

TypeScript를 배우기 시작한 초심자라면, `readonly` 특성을 이해하는 것이 필수입니다. 이 특성은 객체의 프로퍼티나 배열의 요소를 변경 불가능하게 만들어 코드의 안정성을 크게 향상시킵니다. 이제 이 개념을 자세히 파헤쳐보겠습니다.

#### 객체의 `readonly` 프로퍼티

객체의 프로퍼티를 `readonly`로 선언하면, 해당 프로퍼티는 초기화 이후에 변경할 수 없습니다. 이는 객체를 불변 상태로 유지하여 예상치 못한 변경을 방지하는 데 유용합니다.

```typescript
interface Person {
  readonly name: string;
  age: number;
}

const person: Person = {
  name: "Alice",
  age: 30
};

person.age = 31; // 문제 없음
person.name = "Bob"; // 오류 발생: name은 readonly 프로퍼티입니다.
```

위 예제를 보면, `Person` 인터페이스의 `name` 프로퍼티는 `readonly`로 선언되었습니다. 따라서 `person` 객체가 생성된 후 `name` 값을 변경하려고 하면 TypeScript가 오류를 발생시킵니다.

#### 배열의 `readonly` 요소

배열을 다룰 때도 `readonly` 특성을 적용할 수 있습니다. `ReadonlyArray<T>` 타입을 사용하면 배열의 요소들을 수정할 수 없습니다.

```typescript
let numbers: ReadonlyArray<number> = [1, 2, 3];

numbers.push(4); // 오류 발생: push 메서드는 사용 불가
numbers[0] = 10; // 오류 발생: readonly 인덱스 시그니처이므로 수정할 수 없음
```

이처럼 `ReadonlyArray<number>` 타입으로 선언된 `numbers` 배열은 요소를 추가하거나 변경할 수 없습니다. 이는 배열을 불변 상태로 유지하여, 원치 않는 데이터 변경을 방지합니다.

#### 클래스의 `readonly` 멤버

클래스에서도 `readonly`를 사용할 수 있습니다. 클래스 멤버를 `readonly`로 선언하면, 인스턴스가 생성된 후 해당 멤버를 변경할 수 없습니다.

```typescript
class Car {
  readonly brand: string;
  readonly model: string;
  year: number;

  constructor(brand: string, model: string, year: number) {
    this.brand = brand;
    this.model = model;
    this.year = year;
  }
}

const myCar = new Car("Toyota", "Corolla", 2020);
myCar.year = 2021; // 문제 없음
myCar.brand = "Honda"; // 오류 발생: brand는 readonly 멤버입니다.
```

위 예제에서 `Car` 클래스의 `brand`와 `model` 멤버는 `readonly`로 선언되었습니다. 따라서 `myCar` 인스턴스가 생성된 후 이 멤버들의 값을 변경하려고 하면 오류가 발생합니다.

### 왜 `readonly`를 사용해야 할까?

`readonly` 특성을 사용하면 다음과 같은 장점이 있습니다:

1. **코드의 무결성 유지**: 데이터가 예기치 않게 변경되는 것을 방지합니다.
2. **가독성 향상**: 코드의 의도를 명확히 전달합니다. 다른 개발자들이 코드를 읽을 때, 어떤 프로퍼티가 변경 불가능한지 쉽게 파악할 수 있습니다.
3. **디버깅 용이성**: 불변 데이터를 통해 디버깅이 쉬워집니다. 데이터가 어디서 어떻게 변경되었는지 추적할 필요가 없습니다.

TypeScript의 `readonly` 특성은 코드의 안정성과 예측 가능성을 높이는 데 중요한 역할을 합니다. 이제 당신도 이 강력한 도구를 활용하여 더 견고한 코드를 작성할 수 있을 것입니다.

### 참고 문헌

- TypeScript Handbook: [Readonly Properties](https://www.typescriptlang.org/docs/handbook/2/objects.html)
- TypeScript Documentation: [ReadonlyArray](https://www.typescriptlang.org/docs/handbook/utility-types.html#readonlyarraytype)