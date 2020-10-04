---
title: "[React] Redux의 Immutability"
date: "2020-09-21T22:40:32.169Z"
template: "post"
draft: false
slug: "immutability-in-redux"
category: "React"
tags:
  - "React"
  - "Frontend"
  - "Javascript"
description: "리덕스에서 Immutability가 중요한 이유"
socialImage: ""
---

### combineReducers의 shallow equality check

`combineReducers` 는 reference 변화를 추적하는 shallow equality check를 수행한다.

React-redux의 `connect` 또한 `mapStateToProps`의 리턴 값들과 root state의 reference 변화에 반응하는 shallow check 를 수행한다.

### Redux에서의 얕은 비교

리덕스는 `combineReducers` 함수에서 얕은 비교를 해서 바뀐 root state 객체 또는 아무런 변화가 없다면 현재 root state 객체를 리턴한다.

`combineReducers` 는 `reducers` 를 인자로 받아서 동작한다.

```jsx
combineReducers({ todos: myTodosReducer, counter: myCounterReducer });
```

- `todos` 와 `counter` 은 개별 state의 키
- `myTodosReducer`와 `myCounterReducer` 은 리듀서 함수로, 해당 키에 대한 state의 역할

`combineReducers` 는 이 키/값 쌍들에 대해 순회하면서,

- 해당 키가 참조하는 현재 state에 대한 참조를 만들고
- 해당 리듀서를 호출하면서 state를 전달
- 리듀서가 리턴한 변화 여부를 모르는 새로운 state에 대한 참조를 만듦

이후 `combineReducers` 는 새로운 state 객체를 만들게 되는데, 이 때 state들의 변화 여부를 판단할 때 얕은 비교를 수행하는 것이다!

얕은 비교를 수행한 후에 변화가 있으면 `hasChanged` 를 true로 바꾸어 새로 만들어진 state object를 리턴시킨다. false이면 현재 state object가 그대로 리턴된다.

같은 참조값을 가진다면, combineReducers는 새로운 state object를 리턴하지 못할 것이다.
