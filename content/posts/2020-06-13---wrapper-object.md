---
title: "[Javascript] Wrapper 객체"
date: "2020-08-05T22:40:32.169Z"
template: "post"
draft: false
slug: "js-wrapper-object"
category: "Javascript"
tags:
  - "Javascript"
  - "React"
  - "Web Development"
description: "자바스크립트의 Wrapper 객체란, 원시 타입을 객체화 시켜주는 객체형 데이터타입!"
socialImage: ""
---

# Wrapper 객체

### 원시타입을 객체화 시켜주는 객체형 데이터타입

- Number
- String
- Boolean

js의 primitive data type

⇒ number, string, boolean, undefined, null

```jsx
str = "hello"

console.log(str.length) // 5
console.log(str.charAt(0)) // h
```

원시형 데이터타입인 string이 객체마냥 메서드를 가질 수 있게 되는 이유가 바로 **Wrapper 객체** 

### Wrapper Object

원시타입의 프로퍼티에 접근하려고 할 때 생성되는 임시 객체 

- Number
- String
- Boolean

str은 문자열(원시형)

str.length를 통해 객체의 고유 메서드인 length를 이용하려 할 때 

⇒ **str = new String('hello')**라는 선언이 일시적으로 생성되어 **str을 객체화** 시키게 됨

객체화된 str이 length라는 메서드를 이용할 수 있게 되는 것