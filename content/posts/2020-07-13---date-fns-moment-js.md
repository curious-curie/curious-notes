---
title: JS Date 라이브러리, date-fns vs. moment.js
date: "2020-07-13T22:40:32.169Z"
template: "post"
draft: false
slug: "js-date-libraries"
category: "Javascript"
tags:
  - "Javascript"
  - "React"
  - "Web Development"
description: "네이버 인턴십 중 1주차 과제로 캘린더 앱을 개발하면서... date-fns와 moment js 차이점 및 장단점 비교"
socialImage: ""
---

네이버 인턴십 중 1주차 과제로 캘린더 앱을 개발하였다. <br>
날짜 조회, 일정 등록 등 날짜 관련된 기능이 굉장히 많아 날짜 연산 관련 라이브러리가 필요했는데, 예전 인턴할 때 쓰던 date-fns를 아무 생각 없이 선택했다가 moment js도 사용자 수가 굉장히 많은 것 같아 내친김에 차이점 및 장단점을 비교해보게 되었다.


# date-fns vs. moment js

### Moment.js

- OOP library
- momentjs instance를 만들어 그 객체의 멤버함수들을 이용해 기능 실행
- 하나의 연산이 필요하더라도 moment 객체 하나를 생성해야함 ⇒ 필요없는 함수와 기능 생성됨
- month, year, day 연산 등이 모두 add 함수에서 실행되기 때문에 수행되는 시간이나 코드 양 많음
- Mutable

```jsx
const startedAt = moment()
const endedAt   = startedAt.add(1, 'year')

console.log(startedAt) // > 2020-02-09T13:39:07+01:00
console.log(endedAt)   // > 2020-02-09T13:39:07+01:00
```

### date-fns

- 매개변수로 Date 객체를 받는 함수들의 집합
- 필요한 함수만 import하여 사용 가능
- day, month, year 등 구분되어있어 간단명료

- All of date-fns's code are pure functions (and simple to grok)
    - Easy to read code for debugging
    - Immutable is nice
    - No global settings
    - No plugins
    - No chaining (composition is better anyway though)
- Does not force wrapping dates
    - In order to do anything in moment, you have to wrap everything in a moment object