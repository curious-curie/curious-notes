---
title: [Vue.js] computed vs watch vs methods
date: "2020-04-17T22:40:32.169Z"
template: "post"
draft: false
slug: "computed-vs-watch-vs-methods"
category: "Vue"
tags:
  - "Javascript"
  - "Vue"
  - "Web Development"
description: "computed vs watch vs methods
- computed: 참조하는 데이터의 변화 있을 때만 연산, 한번 연산한 값을 캐싱해놓았다가 필요한 부분에 닷 ㅣ활용
    - computed에서 참조하는 속성과 관련없는 것이 업데이트되어서 ui가 재렌더링될 때, computed property는 계산되지 않고 캐싱되어있던 데이터가 리턴됨
..."
socialImage: ""
---
# computed vs watch vs methods

- computed: 참조하는 데이터의 변화 있을 때만 연산, 한번 연산한 값을 캐싱해놓았다가 필요한 부분에 닷 ㅣ활용
    - computed에서 참조하는 속성과 관련없는 것이 업데이트되어서 ui가 재렌더링될 때, computed property는 계산되지 않고 캐싱되어있던 데이터가 리턴됨

    ⇒ 종속 대상에 따라 저장된다

    이런 식으로 아무 곳에도 의존하지 않는 속성의 경우 절대로 업데이트 되지 않음

    ```jsx
    computed: {
      now: function () {
        return Date.now()
      }
    }
    ```

    - 같은 연산 여러번 반복할 때 효율적
    - DOM에서 템플릿 표현식을 통해 참조되지 않으면 계산되지 않는다고 함 (데이터 값이 변경되어도)
- methods: 캐싱의 개념 없어 매번 재랜더링
- watch: 데이터 변화 감지하여 특정 로직 수행
    - 데이터 호출과 같이 시간이 상대적으로 더 많이 소모되는 비동기 처리에 적합

상태를 변경하고 싶다면 computed를, 그 이상의 부수 효과를 처리하고 싶으면 watch를 쓰자

> Vue는 watch 옵션을 통해 데이터 변경에 반응하는 보다 일반적인 방법을 제공합니다. 이는 데이터 변경에 대한 응답으로 비동기식 또는 시간이 많이 소요되는 조작을 수행하려는 경우에 가장 유용합니다.이는 데이터 변경에 대한 응답으로 비동기식 또는 시간이 많이 소요되는 조작을 수행하려는 경우에 가장 유용합니다.

[https://ui.toast.com/weekly-pick/ko_20190307/](https://ui.toast.com/weekly-pick/ko_20190307/)

이때 부수효과란, 직접 컴포넌트에 영향을 주지 않는 

- 데이터 가져오거나
- DOM 조작
- 로컬 저장소나 브라우저 API 사용