---
title: "[React] React Lifecycle (컴포넌트 생명주기)"
date: "2020-09-10T22:40:32.169Z"
template: "post"
draft: false
slug: "js-immutability"
category: "Javascript"
tags:
  - "Javascript"
  - "React"
  - "Web Development"
description: "복습 복습 복습..!"
socialImage: ""
---
# React 컴포넌트 생명주기

복습 복습 복습..! 

![https://miro.medium.com/max/1400/1*CfaYxw2J1ysUZlPOZ_ecDA.jpeg](https://miro.medium.com/max/1400/1*CfaYxw2J1ysUZlPOZ_ecDA.jpeg)

### 리액트 17.0 부터 바뀐 Lifecycle

- (**deprecated)** componentWillMount, componentWillReceiveProps, componentWillUpdate
- (**added)** getDerivedStateFromProps, getSnapShopBeforeUpdate
    - getDerivedStateFromProps: render 직전, props 변화에 따라 state 수정해야 할 때
    - getSnapshotBeforeUpdate: render() 직후 실제 DOM에 적용되기 전에 호출, DOM 변화 일어나기 직전의 DOM 상태를 가져올 수 있음

### Mount

Constructor ⇒ getDerivedStateFromProps ⇒ render ⇒ componentDidMount

컴포넌트가 처음 실행되는 단계.

컴포넌트가 생성되고 DOM에 주입되는 것을 의미하며, 처음에 한번만 실행됨

- **constructor**
    - 컴포넌트가 mount되기 전에 실행
    - state, method binding
- **getDerivedStateFromProps**
    - 변경된 props를 state에 반영하는 작업을 처리
- **render**
    - 렌더링

        ⇒ props, state를 계산하고 DOM에 그려준다 (가상돔 이용하여 비교 후 실제 돔에 반영)

- **componentDidMount**
    - 컴포넌트가 만들어지고 렌더링 된 직후에 호출
    - 외부 라이브러리 연동, axios 등 데이터 요청, 스크롤 설정 등 DOM 관련 작업 수행

### Update

state, props가 변경될 때 update 가 진행되고 다시 렌더링된다

`New Props, setState(), forceUpdate()`에 의해 실행된다

즉 부모 컴포넌트로부터 갱신된 Props를 받거나, setState를 활용해 상태값을 변경하였을 때, 또는 forceUpdate로 강제로 update 시킬 때 실행되는 단계이다

- **getDerivedStateFromProps (props 갱신으로 update 될 때)**
    - 변경된 props를 state에 반영하는 작업을 처리
- **shouldComponentUpdate**
    - props, state 변경 시에 리렌더링 여불르 결정하기 때문에, 이 함수를 통해 최적화가 가능하다
    - 부모 컴포넌트가 리렌더링될 때 자식 컴포넌트에선 변한 게 없는경우 false를 리턴하여 렌더링을 막을 수 있다
- **render**
    - DOM update
- **componentDidUpdate**
    - update가 이루어지고 리렌더링 직후 실행된다
    - 최초 마운트 시엔 실행되지 않는다
    - `prevProps, prevState, snapshot`을 인자로 받는다 ⇒ 이전 상태 / props 와 현재 상태값을 비교하여 무언가 작업을 수행하고 싶을 때 사용할 수 있다.
    - 여기서 setState()할 때 주의해야 함, 무한루프에 빠질 수 있기 때문
    - `setState ⇒ componentDidUpdate ⇒ setState...`

### Unmount

해당 컴포넌트가 DOM 상에서 제거될 때 실행되는 lifecycle 

- **componentWillUnmount**
    - 비동기 API 제거, 이벤트 리스너 제거 등을 수행할 때 사용한다