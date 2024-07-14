---
layout: post
title:  "React.memo에 대해서: 최적화된 컴포넌트 렌더링을 위한 도구"
date:   2024-07-14 23:41:22 +0900
categories: React memo
---

### React.memo: 최적화된 컴포넌트 렌더링을 위한 도구

리액트(React)는 효율적이고 빠른 사용자 인터페이스를 구축하기 위해 만들어진 라이브러리입니다. 그러나 모든 컴포넌트를 반복적으로 렌더링하면 성능 문제가 발생할 수 있습니다. 이러한 문제를 해결하기 위해 React.memo가 등장했습니다. 이 글에서는 React.memo가 무엇인지, 어떻게 사용하고 어떤 이점이 있는지 알아보겠습니다.

#### 1. React.memo란 무엇인가?

React.memo는 리액트의 고차 컴포넌트(HOC, Higher-Order Component)로, 함수형 컴포넌트의 불필요한 렌더링을 방지하는 역할을 합니다. 간단히 말해, props가 변경되지 않는 한 컴포넌트를 다시 렌더링하지 않습니다 .

#### 2. React.memo의 사용법

React.memo는 매우 간단하게 사용할 수 있습니다. 기존의 함수형 컴포넌트를 감싸기만 하면 됩니다.

```jsx
import React from 'react';

const MyComponent = (props) => {
  return <div>{props.value}</div>;
};

export default React.memo(MyComponent);
```

위 코드에서 `MyComponent`는 props가 변경되지 않는 한 다시 렌더링되지 않습니다 .

#### 3. React.memo의 동작 방식

React.memo는 얕은 비교(shallow comparison)를 통해 props의 변화를 감지합니다. 얕은 비교란 객체의 참조만을 비교하는 것을 의미합니다. 따라서, 객체나 배열이 새로운 참조로 변경되지 않는 한 동일하다고 판단합니다.

```jsx
const areEqual = (prevProps, nextProps) => {
  // custom comparison logic
  return prevProps.value === nextProps.value;
};

export default React.memo(MyComponent, areEqual);
```

위와 같이 `areEqual` 함수를 사용해 커스텀 비교 로직을 추가할 수도 있습니다 .

#### 4. React.memo의 이점

1. **성능 최적화**: 불필요한 렌더링을 방지하여 성능을 향상시킵니다.
2. **코드 간결성**: 간단하게 적용할 수 있어 코드가 복잡해지지 않습니다.
3. **메모이제이션**: props가 변경되지 않을 때 컴포넌트를 메모이제이션하여 이전 렌더링 결과를 재사용합니다 .

#### 5. React.memo의 한계

React.memo는 모든 상황에서 성능을 보장하지 않습니다. 오히려 잘못 사용하면 성능 저하를 초래할 수 있습니다. 특히, 복잡한 비교 로직이 있는 경우 오버헤드가 발생할 수 있습니다. 따라서, 실제로 성능 향상이 필요한 경우에만 사용하는 것이 좋습니다 .

#### 6. 결론

React.memo는 함수형 컴포넌트의 불필요한 렌더링을 방지하는 강력한 도구입니다. 성능 최적화가 필요한 부분에 적절히 사용하면 유용하지만, 모든 컴포넌트에 무조건 적용하기보다는 필요에 따라 신중하게 사용하는 것이 중요합니다. 올바르게 사용한다면, React.memo를 통해 더욱 빠르고 효율적인 리액트 애플리케이션을 구축할 수 있을 것입니다.

---

#### 레퍼런스

[React.memo 공식 문서](https://react.dev/reference/react/memo)