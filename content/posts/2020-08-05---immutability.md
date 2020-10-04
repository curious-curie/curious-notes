---
title: Immutability in JS 
date: "2020-08-05T22:40:32.169Z"
template: "post"
draft: false
slug: "js-immutability"
category: "Javascript"
tags:
  - "Javascript"
  - "React"
  - "Web Development"
description: "JS의 immutability, 그리고 그것이 중요한 이유"
socialImage: ""
---
# Immutability

### Primitive Types : Immutable

- Boolean
- null
- undefined
- Number
- String
- Symbol

```jsx
let str = 'hello'
str = 'world'
```

이렇게 하면 hello 문자열이 변경되는 게 아니라 world가 새로 메모리에 할당되는 것 

```jsx
let statement = 'I am an immutable value'; // string은 immutable value
let otherStr = statement.slice(8, 17);
```

이렇게 하면 statement가 가리키는 문자열을 변경한 것이 아니라 해당 문자열을 가지고 만든 새로운 문자열을 메모리에 할당 

### Object Types: Mutable

객체는 참조 형태로 전달하고 전달 받는다 ⇒ 그 상태가 변경될 수 있다 

⇒ 레퍼런스를 참조한 다른 객체에서 객체를 변경할 때 의도치 않은 변경으로 문제 발생

- mutable value는 값에 대한 메모리 주소를 참조하기 때문에 값을 변경했을 경우 해당 값을 사용하고 있는 모든 곳에서 side effect(부수 효과)가 발생하여 예상치 못한 버그를 유발할 수 있음
- 해결 방법
    - 불변 객체로 만들어 프로퍼티 변경을 방지하기
        - 변경이 필요한 경우에는 객체의 방어적 복사 (spread operator, object.assign 사용) 를 통해 새로운 객체를 생성
        - Observer 패턴으로 변경에 대응

immutable로 객체를 선언하고 사용하게 되면 객체의 메모리 주소가 불변

- 구조를 단순하게 유지
- 구조적인 공유
    - 어플리케이션 동작의 예측
    - 내부적으로 구조를 공유하고 있기 때문에 메모리 사용량 감소

**[참고]** [13. react-tutorial 고급 (불변성 - Immutability 개념)](https://blog.naver.com/backsajang420/221358585106)|**작성자** [JeromeBaek](https://blog.naver.com/backsajang420)

### 리액트에서의 Immutability

state 수정 시 setState를 통해 업데이트해야, 기존 객체의 값을 직접적으로 수정하면 안됨

- 리렌더링 되지 않음 (얕은 비교하기 때문)
- 컴포넌트 최적화 어렵다
    - 배열 직접적으로 수정한 경우 `prev.arr !== next.arr`로 비교 불가능
    - 참조하는 주소 똑같이 남아있기 때문에..
- Redux의 Reducer도 Immutability를 유지하며 동작 (새로운 state 반환!)