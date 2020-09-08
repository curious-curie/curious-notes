---
title: [React] Mobx 리뷰 및 사용기, Redux와 비교
date: "2020-08-20T22:40:32.169Z"
template: "post"
draft: false
slug: "mobx-review"
category: "React"
tags:
  - "Javascript"
  - "React"
  - "Web Development"
description: "네이버 인턴십 6주차 과제를 진행하고 나서 쓴 Mobx 리뷰"
socialImage: ""
---
# Mobx Review

네이버 인턴십 6주차 과제를 진행하고 나서 쓴 Mobx 리뷰

- 기존에 Redux를 사용하여 개발한 라이브 방송 다시보기 및 실시간 채팅 뷰어
- 같은 프로젝트를 Redux 대신 Mobx를 사용하여 개발해보았다

![Mobx%20Review%2002a6948d4c3e46d1aaee1bbe94d6e16c/Untitled.png](Mobx%20Review%2002a6948d4c3e46d1aaee1bbe94d6e16c/Untitled.png)

### 기본 구조

- Observable : 관찰받고 있는 STATE
- Computed: state 이용하여 연산된 값
- Action: 상태에 변화를 일으키는 행동
- Reaction: observable의 변화에 반응하여 일어남
    - autorun : autorun 통해 observable 관찰하고 필요한 리액션 실행
        - console 찍는 등 side effect 내포할 땐 computed 대신 autorun 사용
    - 리액트 내에서는 리액트 내부 API로 해결 가능하기 때문에 빈번히 사용되진 않음

⇒ 개인적으로 Vue 및 Vue의 상태관리 라이브러리인 vuex와 비슷한 점이 많다고 생각.

Vuex가 리덕스와 Mobx를 짬뽕시켜놓은 느낌

Mobx ⇒ Vuex

Observable ⇒ State

Action ⇒ Action + Mutation 

Autorun ⇒ Watch (Vue)

### 코드 비교 (video url fetching action)

### redux ver.

```java
const GET_VIDEO_URL = 'video/GET_VIDEO_URL';
const GET_VIDEO_URL_SUCCESS = 'video/GET_VIDEO_URL_SUCCESS';
const GET_VIDEO_URL_ERROR = 'video/GET_VIDEO_URL_ERROR';

// action
export const getVideoUrl = (vid) => async (dispatch) => {
  dispatch({ type: GET_VIDEO_URL });
  try {
    const video = await api.getVideoURL(vid);
    dispatch({ type: GET_VIDEO_URL_SUCCESS, video });
  } catch (e) {
    dispatch({ type: GET_VIDEO_URL_ERROR, error: e });
  }
};

// reducer
export default function videoReducer(state = initialState, action) {
  switch (action.type) {
    case GET_VIDEO_URL:
      return {
        data: null,
        error: false,
        loading: true,
      };
    case GET_VIDEO_URL_SUCCESS: {
      return {
        data: action.video,
        error: false,
        loading: false,
      };
    }
    case GET_VIDEO_URL_ERROR:
      return {
        loading: false,
        data: null,
        error: action.error,
      };
    default:
      return state;
  }
}
```

### mobx ver.

```java
class VideoStore {
  @observable data = {};
  @observable error = null;

  @action
  getVideoUrl = async (vid) => {
    try {
      const video = await api.getVideoURL(vid);
      this.data = { ...video };
    } catch (e) {
      this.error = e;
    }
  };
}
```

## 내가 느낀 장점

### 코드가 간결, 쉽다

- 불변성 유지 불필요 ⇒ Immutable 이슈 X
    - 이렇게 할 필요가  없다

```jsx
const myReducer = (state, action) => ({
  ...state,
  depth1: {
    ...state.depth1,
    depth2: {
      ...state.depth1.depth2,
      depth3: {
        ...state.depth1.depth2.depth3,
        depth4: action.payload
      },
    },
  },
})
```

- action type 선언 및 reducer 에서 action type에 따른 return state 정의할 필요 X
- **데코레이터**를 사용한 간결한 코드 작성
- 리덕스보다 처음에 이해하기 쉽다
    - 리듀서, 액션, 디스패치... 개념 파악하는게 어려웠는데 그에 비해 훨씬 쉽고 명확

### 객체지향 친화적

- store의 구성요소 및 역할 파악이 쉬움 ⇒ 가독성  👍🏻
- java class와 비슷한 느낌
    - config 설정으로 state를 setter 통해서만 변경할 수 있도록 캡슐화 가능
        - side effect 최소화

### 타 Library 필요성이 낮아짐

- 비동기 동작, 액션 내 액션을 실행시키기 위한 thunk 등의 미들웨어 불필요
    - 비동기 동작은 액션에 async 처리,
    - 액션 내 액션은 runInAction 등 내장된 기능을 활용하여 모두 해결 가능
- Computed의 편리함 !
    - state의 값을 이용해서 필터링하거나 연산된 값을 반환하기 위해 reselect 등의 라이브러리를 사용하거나 뷰단에서 연산하지 않아도 편리하게 스토어 내에서 연산값을 반환 가능하다
    - 편하다...!!!!

### 똘똘한 성능 - memoization...

- Memoization
    - computed 연산 시 **캐싱**
        - state 값이 변하지 않을 시엔 캐싱 되어있던 기존 값을 반환
    - redux 사용 시 reselect를 이용하여 처리해야했던 부분들을 알아서 해준다
        - observer는 자기가 쓰는 값이 무엇인지 알아서 기억하고, 렌더해야 할 요인이 되는 값들을 자동적으로 추적한다

- 액션 수행 시의 트랜잭션
    - 상태 변경을 하나의 단위로 묶어 트랜잭션을 수행
    - 리액션 내에 여러가지 observable를 참조하고 있고, 해당 observable 들의 변화를 일으키는 액션이 수행될 때, 각각의 observable이 변화할 때 마다 리액션이 일으켜지는게 아니라 한 액션에서 모든 동작이 끝났을 때 리액션을 일으킴
    - 렌더링 성능(횟수)에서 큰 차이

## 내가 느낀 단점

### 레퍼런스 가뭄

- 특히 Hooks와 함께 사용하는 mobx v6 (mobx-react-lite) 는 레퍼런스가 너무 없다...
- 공식문서에도 예제가 친절하게 풍부하진 않은 느낌

### 버전 별 차이

- 5.x 이상버전: es6 환경에서 구동
- 프록시를 지원하는 브라우저에서만 사용가능 (IE 사용불가)
- observable 오브젝트는 콘솔에 찍으면 proxy 오브젝트로 찍히는데, 디버깅 시에 조금 불편함
    - toJS 내장함수 사용해서 변환시켜야 원래 object 모양으로 보임
- 브라우저 지원 문제에 따라 4.x 버전을 사용하게 되면 함수 컴포넌트와 호환 불가
    - 결국 브라우저 지원을 포기하던가, 구조를 바꾸던가 해야함..ㅠㅠ

### 리덕스보다 덜 견고한 느낌

- 액션 단에서 `this.어쩌구 = { ... }` 이렇게 state를 바로 바꾸는게 어떻게 보면 엄청 편한데 나중에 유지 보수 하거나 디버깅시에는 어려울 수 있을 것 같음
- 리덕스는 구조가 딱 틀에 맞추어져 있고 거기에 맞게 코딩을 해야 하는게 번거롭지만, 그것때문에 코드의 견고함이나 안정성이 높아지는 듯

### DevTool이 별로다

- redux devtool처럼 다양한 기능 제공 X
- 가독성도 ↓