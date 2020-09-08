---
title: Intersection Observer
date: "2020-07-12T22:40:32.169Z"
template: "post"
draft: false
slug: "intersection-observer"
category: "FRONTEND"
tags:
  - "Javascript"
  - "React"
  - "Web Development"
description: "타겟 엘레멘트와 타겟의 부모 혹은 상위 엘레멘트의 뷰포트가 교차되는 부분을 비동기적으로 관찰하는 API, 결국 타겟 element가 화면에 노출되었는지 여부 구독하는 방법"
socialImage: ""
---
# Intersection Observer

타겟 엘레멘트와 타겟의 부모 혹은 상위 엘레멘트의 뷰포트가 교차되는 부분을 비동기적으로 관찰하는 API ⇒ 결국 타겟 element가 화면에 노출되었는지 여부 구독하는 방법

네이버 인턴십 1주차 과제에서 Intersection Observer을 사용한 무한스크롤을 구현했다.
이전까지는 scroll event listener을 활용한 구현만 했었는데, 새로 알게 된 부분이라 정리해보았다. 

### - methods

`IntersectionObserver.observe(target)`: 관찰 시작

`IntersectionObserver.unobserve(target)`: 관찰 종료

`IntersectionObserver.disconnect(target)`: 관찰 멈추기

1. `Intersection Observer` 객체를 생성하면서, `Callback Function` 과 `option` 을 전달한다.
2. `Intersection Observer` 에서 observe 로 구독할 `Target Element` 를 추가한다.
3. `Target Element` 가 options.threshold 로 정의한 **Percent**(%) 만큼 화면에 노출 혹은 제외 되면, entries 배열 에 추가하고, `Callback Function` 을 호출한다.
4. `Callback Function` 에서 전달 받은 entries 배열을 확인하면서, **isIntersecting** 으로 노출 여부를 확인한다.
5. 만약 더이상 `Target Element` 를 구독할 필요가 없다면, IntersectionObserver 에서 **unobserve** 로 제거 할 수 있다.

## 왜 쓸까?

window.addEventListener을 이용한 스크롤 이벤트 구현할 때의 비효율성을 어느 정도 해결해준다. 

### 1. 호출 수 제한 방법 debounce, throttle을 사용하지 않아도 된다.

`debounce`와 `throttle`은 스크롤 이벤트로 인해 발생하는 불필요한 함수 호출 수를 컨트롤할 필요가 있음.

console.log가 수도없이 호출됨 

```
window.addEventListener('scroll', function() {
   return console.log('scroll!');
});
```

### 2. reflow를 하지 않는다.

스크롤 이벤트에서는 현재의 높이 값을 알기 위해`offsetTop` 을 사용하는데 정확한 값을 가져오기 위해 매번 layout을 새로 그리게 된다.

⇒ 렌더 트리를 재생성 하는 것이기 때문에 브라우저 성능 저하