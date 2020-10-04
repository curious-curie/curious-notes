---
title: "HTTP Method: GET vs. POST"
date: "2020-08-11T22:40:32.169Z"
template: "post"
draft: false
slug: "get-vs-post"
category: "Development"
tags:
  - "Development"
  - "HTTP method"
description: "GET vs POST, 공통점 및 차이점 간단 정리"
socialImage: ""
---

# GET vs POST

### 공통점

클라이언트가 서버에 데이터를 전달함

### GET

데이터가 URL의 뒤에 이어붙는다 

example.com?date=20190910

- 전송하는 데이터량에 제한, 사용자에게 데이터가 그대로 노출
- 한글, 특수문자의 경우 인코딩 필요
- 웹크롤러가 접근하여 실행할 가능성 ⇒ SQL query의 SELECT와 같은 단순 조회에만 이용하는 것이 좋음

### POST

HTTP body에 넣어 전달

- 사용자에게 데이터가 그대로 노출되지 않음
- 전송량 제한 X
- 암호화는 따로 없음 ⇒ 보안에는 둘 다 취약
- GET과 달리 브라우저 캐싱 불가능
- 서버의 값이나 상태를 변경하는 경우 POST로 구현