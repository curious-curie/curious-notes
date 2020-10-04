---
title: "[React] HOC, Custom Hooks를 사용한 코드 재사용"
date: "2020-09-07T22:40:32.169Z"
template: "post"
draft: false
slug: "ways-to-improve-react-reusability"
category: "Javascript"
tags:
  - "Javascript"
  - "React"
  - "Web Development"
description: "코드 재사용성을 높이기 위한 방법들 중 HOC와 Custom Hooks에 대해 알아보자 ~!"
socialImage: ""
---

코드 재사용성을 높이기 위한 방법들 중 HOC와 Custom Hooks에 대해 알아보자 ~!

## HOC (Higher Order Components)

**컴포넌트를 인자로 받아 컴포넌트를 반환하는 함수**

컴포넌트를 또 다른 컴포넌트로 변환시킨다. 

```jsx
const EnhancedComponent = higherOrderComponent(WrappedComponent);
```

같은 패턴의 코드 (데이터 fetch, logging)이 다른 컴포넌트들에서 조금씩 다른 형태로 반복되는 경우에 HOC를 사용하면 재사용성을 높일 수 있다. 

```jsx
const CommentListWithSubscription = withSubscription(
  CommentList,
  (DataSource) => DataSource.getComments()
);

const BlogPostWithSubscription = withSubscription(
  BlogPost,
  (DataSource, props) => DataSource.getBlogPost(props.id)
);
```

이 코드에서 `withSubscription`이 그러한 HOC의 예시이다. 

`CommentList`와 `BlogPost`에서 같은 동작은 아니지만, DataSource 에 위치한 함수를 호출하여 데이터를 내려받고, mount 시에 listener을 달아 DataSource의 변화를 listen하여 state를 바꾼다. Unmount 시엔 listener를 해지한다. 

```jsx
// This function takes a component...
function withSubscription(WrappedComponent, selectData) {
  // ...and returns another component...
  return class extends React.Component {
    constructor(props) {
      super(props);
      this.handleChange = this.handleChange.bind(this);
      this.state = {
        data: selectData(DataSource, props)
      };
    }

    componentDidMount() {
      // ... that takes care of the subscription...
      DataSource.addChangeListener(this.handleChange);
    }

    componentWillUnmount() {
      DataSource.removeChangeListener(this.handleChange);
    }

    handleChange() {
      this.setState({
        data: selectData(DataSource, this.props)
      });
    }

    render() {
      // ... and renders the wrapped component with the fresh data!
      // Notice that we pass through any additional props
      return <WrappedComponent data={this.state.data} {...this.props} />;
    }
  };
}
```

HOC는 side-effect 없는 순수 함수이다. 인풋 컴포넌트의 아무 것도 바꾸지 않고, container component로 감쌈으로써 원래 컴포넌트를 합성한다. 

redux의 connect도 HOC를 생성해주는 헬퍼 함수라고 할 수 있다고 한다. connect 함수는 mapStateToProps 와 mapDispatchToProps 를 인자로 받아서 새로운 HOC를 반환한다. 

그러나 HOC의 단점 중 하나는 여러가지 기능을 함께 수행해야 할 때, 즉 여러 HOC를 같은 컴포넌트에 사용해야 할 때 코드가 거추장스러워질 수 있다는 것이다. 

`withMousePosition(withClock(MyComponent))`

이런 식으로 말이다. 필요한 로직의 수가 많아질 수록 배로 문제가 될 것이다. 또한 디버깅과 테스팅이 힘들다는 문제도 있다. 컴포넌트가 잘못 동작한다면, 감싸놓은 HOC를 하나하나 까보면서 디버깅해보아야 할 것이다.

함수 컴포넌트에서 라이프사이클 메서드를 사용하고 싶을 때 HOC를 이용할 수 있겠다는 생각이 든다. 그러나 그럴 필요성이 없었던 이유는 Hooks가 그 역할을 너무 잘 해주고 있기 때문인 것 같다. HOC를 실제로 사용한 적이 드물었던 이유도, custom hooks를 구현해서 이와 같은 동작을 구현할 수 있기 때문이었던 것 같다. 자연스럽게 Hooks 로 넘어가보자.

## Using Custom Hooks

hooks 환경에서는 HOC를 사용하지 않고도 `useScrollPosition` 과 같은 custom hooks를 만들어 코드 재사용성을 높일 수 있다. 

`componentDidMount, componentWillUnmount, componentDidupdate`

를 모두 `useEffect` 를 통해 구현할 수 있기 때문에 흔히 사용하는 생명주기 메서드를 모두 hooks 내에서 해결할 수 있다. 

마우스가 움직일 때마다 그 좌표를 화면에 나타내야 한다고 하자. (캔버스나 게임 개발 시에 자주 쓰일 것 같다) 여러개의 페이지에서 해당 기능이 필요하다면 HOC를 써서 해결할 수도 있지만, custom hooks function을 만들어 필요한 컴포넌트마다 가져다 쓸 수 있다.

```jsx
import React, { useState, useEffect } from 'react';

const useMouseMove = () => {
  const [coords, setCoords] = useState([0, 0]);

  useEffect(() => {
    const handler = ({ clientX, clientY }) => {
      setCoords([clientX, clientY]);
    };
    window.addEventListener('mousemove', handler);
    return () => {
      window.removeEventListener('mousemove', handler);
    };
  }, []);

  return coords;
};
```

```jsx
const MyComponent = () => {
  const [x, y] = useMouseMove();

  return (
    <>
      <div>Mouse coordinates: {x},{y}</div>
    </>
  );
}
```