---
title: "[JS] ECMAScript와 ES6"
date: "2020-08-05T22:40:32.169Z"
template: "post"
draft: false
slug: "js-immutability"
category: "Javascript"
tags:
  - "Javascript"
  - "Web Development"
  - "ES6"
description: "ECMAScript와 Javascript의 연관성, 그리고 ES6의 key feature들에 대해 정리"
socialImage: ""
---
# ECMA Script, ES6

내가 즐겨쓰는 + 좋아하는 많은 문법들이 ES6 이후 새로 등장한 것들이다.

(바벨아 고마워 ... !!)

## ECMA Script

"Ecma 인터내셔널에 의해 제정된 ECMA-262 기술 규격에 의해 정의된 범용 스크립트 언어"

**스크립트 언어**가 준수해야 하는 규칙, 세부사항 및 지침을 제공한다 

Javascript는 **ECMA Script 사양을 준수하는 스크립트 언어**인 것! 

### 그럼 스크립트 언어는 뭐야?

기존에 이미 존재하는 소프트웨어를 제어하기 위한 용도로 쓰이는 언어

기존 프로그램의 존재 하에 사용 ⇒ 웹이 없다면 자바스크립트를 쓰는 의미가 없는 것. 

인터프리터 방식 사용 

- 컴파일러 X ( ⇒ js 동적 타이핑과도 연관 )
- 소스 코드 한 줄 한 줄 즉시 해석하고 바로 실행한다
- 단순하고 쉬운 문법
- 사용하기 편리하다
- 실행 속도가 느림

## ES6+ 주요 feature

- Let, Const 키워드 추가
- 화살표 함수
    - 자신의 `this`가 없이, 화살표 함수를 둘러싸는 렉시컬 범위의 `this`가 사용된다 ⇒ 화살표 함수의 바로 바깥 범위에서 this를 찾는다
- Promise 도입
    - 비동기 처리를 위한 또 다른 패턴, 콜백 헬 방지
    - pending (수행 이전) / fulfilled (수행 성공) / rejected (수행 실패) / settled (수행 성공 또는 실패)

```jsx
// Promise 객체의 생성
const promise = new Promise((resolve, reject) => {
  // 비동기 작업을 수행한다.

  if (/* 비동기 작업 수행 성공 */) {
    resolve('result');
  }
  else { /* 비동기 작업 수행 실패 */
    reject('failure reason');
  }
});
```

- 템플릿 리터럴
- 모듈

```jsx
import MyModule from "./MyModule"
import { func1, func2 } from "./MyFunc"

// MyModule.js
export default MyModule() { ... }

//MyFunc.js
export const func1 = () => { ... }
export const func2 = () => { ... }
```

- class 키워드를 사용한 클래스 선언
    - ES5에서는 프로토타입을 이용하여 클래스 구현함

```jsx
class Add {
  constructor(arg1, arg2) {
    this.arg1 = arg1;
    this.arg2 = arg2;
  }
  calc() {
    return this.arg1 + "+" + this.arg2 + "=" + (this.arg1 + this.arg2);
  }
}

var num = new Add(5, 8);
console.log(num.calc()); // 5 + 8 = 13
```

### ES8

- async await

    ⇒ 가독성 높은 비동기 처리! 

```jsx
async function 함수명() {
  await 비동기_처리_메서드_명();
}
```