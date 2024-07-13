---
layout: post
title:  "리액트에서의 리팩터링에 대해서"
date:   2024-07-13 23:00:22 +0900
categories: React Refactoring
---

### 리액트 리팩터링: 코드 품질 향상의 비결

리액트 프로젝트를 진행하다 보면 '리팩터링'이라는 단어를 많이 듣게 됩니다. 그렇다면, 리팩터링이란 무엇이고, 왜 중요한 걸까요? 리팩터링은 기능을 바꾸지 않으면서 코드의 구조를 개선하는 작업을 말합니다. 이는 단순히 코드의 가독성을 높이는 것을 넘어, 유지보수성을 극대화하고 버그를 줄이는 데 필수적입니다. 이제, 리액트 프로젝트에서 효과적으로 리팩터링하는 방법을 살펴보겠습니다.

#### 1. 클래스형 컴포넌트를 함수형 컴포넌트로 전환

클래스형 컴포넌트를 함수형 컴포넌트로 변환하는 것은 리팩터링의 첫 걸음입니다. `useEffect`와 같은 훅을 활용하면 `componentDidMount`와 같은 생명주기 메서드를 간단히 대체할 수 있습니다. 이는 코드의 간결성을 높이고, 성능 개선에도 기여합니다【7†source】【9†source】.

```jsx
// Before: Class Component
class BookList extends React.Component {
  componentDidMount() {
    this.props.fetchBooks(this.props.bookGenre);
  }

  componentDidUpdate(prevProps) {
    if (prevProps.bookGenre !== this.props.bookGenre) {
      this.props.fetchBooks(this.props.bookGenre);
    }
  }
}

// After: Functional Component with Hooks
const BookList = ({ bookGenre, fetchBooks }) => {
  useEffect(() => {
    fetchBooks(bookGenre);
  }, [bookGenre]);
};
```

#### 2. 상태 관리 개선

`useReducer` 훅을 사용하여 상태 관리를 개선할 수 있습니다. 이는 상태 업데이트 로직을 중앙화하고 가독성을 높이는 데 도움을 줍니다. 다수의 `useState` 훅을 사용하는 대신, `useReducer`를 사용하여 상태 변경을 일관되게 관리할 수 있습니다【7†source】.

```jsx
const [state, setState] = useReducer((state, newState) => ({ ...state, ...newState }), {
  data: null,
  error: null,
  loaded: false,
  fetching: false,
});
```

#### 3. 코드 중복 제거

반복되는 코드를 재사용 가능한 컴포넌트나 커스텀 훅으로 추출하여 DRY(Do not Repeat Yourself) 원칙을 따르는 것이 중요합니다. 이는 코드 유지보수를 용이하게 하고, 코드베이스의 청결도를 높입니다【9†source】.

```jsx
// Custom Hook Example
const useFetchBooks = (bookGenre) => {
  useEffect(() => {
    fetchBooks(bookGenre);
  }, [bookGenre]);
};
```

#### 4. 코드 분리

큰 컴포넌트를 작은 컴포넌트로 분리하여 코드의 모듈성을 높이세요. 이는 단일 책임 원칙(Single Responsibility Principle)을 준수하게 합니다. 큰 컴포넌트는 관리하기 어렵고, 작은 컴포넌트로 분리하면 재사용성과 유지보수성을 크게 향상시킬 수 있습니다【8†source】.

#### 5. 스타일과 헬퍼 함수 분리

스타일과 헬퍼 함수를 별도의 파일로 분리하는 것은 코드의 가독성을 높이는 데 매우 효과적입니다. 특히 큰 프로젝트에서는 이런 접근 방식이 더욱 중요합니다【8†source】.

```jsx
// Example File Structure
src/
  components/
    BookList/
      BookList.jsx
      BookList.styles.js
      BookList.helpers.js
```

#### 6. 적절한 변수 및 컴포넌트 이름 사용

변수와 컴포넌트 이름을 명확하고 설명 가능하게 지정하는 것은 코드의 가독성을 높이고, 팀원 간의 원활한 커뮤니케이션을 가능하게 합니다. 애매한 이름은 코드 이해를 어렵게 하며, 이는 유지보수를 복잡하게 만듭니다【9†source】.

#### 7. 화살표 함수 사용 줄이기

렌더 메서드 내에서 화살표 함수를 사용하는 것을 피하세요. 이는 성능 문제를 야기할 수 있으며, 함수는 클래스의 메서드로 정의하여 사용하는 것이 좋습니다【9†source】.

```jsx
// Avoid this
render() {
  return (
    <button onClick={() => this.setState({ flag: true })}>Click me</button>
  );
}

// Use this
changeFlag = () => this.setState({ flag: true });
render() {
  return (
    <button onClick={this.changeFlag}>Click me</button>
  );
}
```

리팩터링은 단순히 코드의 외형을 바꾸는 것이 아니라, 전체적인 코드 품질을 높이는 과정입니다. 이러한 과정을 통해 더 나은 코드베이스를 구축하고, 유지보수성을 극대화할 수 있습니다. 


리액트 리팩터링의 더 많은 예제와 팁 : [LogRocket 블로그](https://blog.logrocket.com), [Code Pieces](https://code.pieces.app), [Keenethics](https://keenethics.com)