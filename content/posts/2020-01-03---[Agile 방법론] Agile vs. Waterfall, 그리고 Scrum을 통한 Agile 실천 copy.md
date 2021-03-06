---
title: "[Agile 방법론] Agile vs. Waterfall, 그리고 Scrum을 통한 Agile 실천"
date: "2020-01-03T15:46:37.121Z"
template: "post"
draft: false
author: true
slug: "agile-methodology"
category: "Development"
tags:
  - "Development"
  - "Development Strategy"
  - "Agile"
description: "Waterfall vs. Agile

폭포수 모델 (waterfall model)과 애자일 모델 (Agile model)은 가장 대표적인 프로젝트 방법론 두가지라고 볼 수 있습니다. 차이점을 설명하기에 앞서, 아래 이미지를 보시면 대략적인 두 방법론의 차이점을 아실 수 있을 것 같습니다... "
socialImage: ""
---

## Waterfall vs. Agile

폭포수 모델 (waterfall model)과 애자일 모델 (Agile model)은 가장 대표적인 프로젝트 방법론 두가지라고 볼 수 있습니다. 차이점을 설명하기에 앞서, 아래 이미지를 보시면 대략적인 두 방법론의 차이점을 아실 수 있을 것 같습니다. 

![Waterfall vs. Agile](https://i1.wp.com/ouriken.com/blog/wp-content/uploads/2019/11/Untitled-design-2.png?w=736)

이미지 출처: http://ouriken.com/blog/which-one-is-right-for-you-waterfall-or-agile/



## Waterfall Model 

가장 처음 등장한 프로세스 방법론으로, 정해진 순서에 따라 단계가 진행되는 <strong>순차적 (sequential) 모델</strong>입니다.

이전 단계의 출력물이 다음 단계의 입력으로 들어가는 형태이기 때문에 다음 단계의 작업을 실행하기 위해서는 이전 단계가 무조건 종료되어있어야 한다는 특징을 가집니다. 

정해진 순서에 따라 각 파트의 업무가 분리되어 진행되기 때문에 관리와 스케쥴 설정이 용이하고 이해가 쉽다는 장점이 있습니다. 워터폴 방식으로 프로젝트를 진행하면 진행 프로세스가 명확하고, 중첩되어 진행되지 않기 때문에 혼동을 방지하고 실수를 최소화하기 할 수 있습니다. 

그러나 각각의 단계에 소요될 시간과 비용에 대한 추정이 쉽지 않고, 테스팅 단계에서 다시 이전 단계로 돌아가 고객의 의도와 맞지 않는 부분을 수정하기 어렵다는 단점을 가집니다. 또한 디자인이 구현되거나 개발을 통한 기능 구현이 완료되어 고객이 확인하기 전까지는 고객은 기존 요구사항이 실제 프로젝트에 어떻게 반영되고 있는지 알기 어렵습니다. 디자인과 개발 단계가 끝나고 나서야 고객은 실제 서비스를 확인할 수 있는 경우가 많은데, 그때가 되어서야 수정 요청이 발생하기 시작하고, 이미 지나온 많은 단계들을 다시 되돌아가 고객의 요청을 반영하기 위해서는 큰 비용과 시간적 문제가 발생합니다. 



## Agile Model

애자일 모델은 폭포수 모델의 단점을 보완하기 위해 등장한 프로세스 모델입니다. 

> Agile: 1. 날렵한, 민첩한   2. (생각이) 재빠른, 기민한

Agile의 사전적인 정의에서도 알 수 있듯, 애자일 방법론은 좋은 것을 빠르게 취하고 낭비를 최소화하는 것과 변화에 대한 민첩한 대응을 강조합니다. 

전체적인 프로세스를 정의하고 문서를 통해 프로세스나 일정의 정의를 주도하는 waterfall model과 달리 agile model은 짧은 주기로 소프트웨어를 개발하면서 이슈 사항들을 바로 바로 제어하고 커뮤니케이션의 비용을 최소화하고자 합니다. 

일정한 주기를 가지고 끊임없이 프로토타입을 만들어내며 요구사항을 더하거나 수정하며 프로젝트를 진행하기 때문에 고객과 커뮤니케이션하고 요구사항을 반영할 여지가 커진다는 장점을 가지고 있습니다. 길고 연속된 단계로 개발되는 대신 반복적인 주기를 가지기 때문에 프로젝트의 방향이나 진행상황을 자주 검토할 수 있게 해주며, 초기에 버그를 고치고 수정하면서 개발을 진행할 수 있습니다.

 

## 대표적인 Agile 방법론, SCRUM 

스크럼은 애자일의 실천 도구 중 하나라고 볼 수 있습니다. 스크럼은 럭비에서 경기를 재개하기 위해 8명( 또는 6명)의 팀원들이 서로 밀착하여 형성하는 전술 대형을 가리킵니다. 이러한 용어가 개발 프로세스에서 사용되는 것은 
> "팀이라는 단어가 주는 의미를 개발 팀에 적용하여 효율적인 성과를 얻기 위함"
이라고 합니다. 

스크럼은 5-9명으로 구성되는 소규모의 다기능팀이 제품 개발을 완성하기 위해 <strong>스프린트(sprint)</strong> 라고 불리는 업무 주기를 반복하는 식으로 진행됩니다. 스프린트는 반복적인 개발 주기로, 계획 회의부터 리뷰가 진행되는 날짜 까지의 기간을 한 스프린트로 정하게 됩니다. 일반적으로 30일정도의 주기가 권장되지만 진행 상황에 따라 1주~4주의 유연성을 가집니다. 

Scrum의 진행 과정 및 구성 요소는 다음과 같습니다: 

![scrum-process](https://miro.medium.com/max/1920/0*tldQVMrGJ_vFIDlB.jpg)

이미지 출처 : https://brainhub.eu/blog/differences-lean-agile-scrum/

### Scrum Process의 구성 

#### 제품 백로그(Product Backlog)

- 제품 완성에 필요한 특성, 기능, 개선점 등 제품의 요구사항을 우선순위에 따라 나열한 목록
- Product Owner(제품 책임자)가 작성하며, 확정, 고정된 것이 아니라 지속적으로 업데이트됨
- 하나의 스프린트가 끝나면 업데이트하여 다음 회의때 제시되어야 함 

#### 스프린트 백로그(Sprint Backlog)

- 스프린트 회의 시 결정되는 것, 요구사항을 각각의 과업으로 구체화 한 문서 
- 하나의 스프린트 동안 완료할 과제들의 목록

![Sprint Backlog](https://scrumorg-website-prod.s3.amazonaws.com/drupal/inline-images/2017-03/SprintBacklog_0.png)

[스프린트 백로그 예시] 이미지 출처:https://www.scrum.org/resources/what-is-a-sprint-backlog  

#### 일일 스크럼 (Daily Scrum)

- 스프린트 기간에 매일 하는 회의
- 어제 한일, 오늘 할 일, 해결해야 할 문제 요소를 공유
- 모든 참여자가 참여하며 보고가 아닌 수평적인 공유 차원에서 진행되어야 함 

#### 스프린트 리뷰 (Sprint Review)

- 스프린트 종료 후 개발된 제품을 고객을 포함한 이해 관련자에게 보여주면서 데모를 수행하는 것 
- 제품 오너는 고객의 평가, 피드백과 스프린트 리뷰에서 도출된 여러 개선사항을 정리하여 다음 스프린트에 반영될 수 있도록 정리해야 한다 

#### 스프린트 회고 (Sprint Retrospective)

- 스프린트가 끝나는 시점이나 일정 주기로 진행되며 회고를 통해 프로젝트 진행에 있어 좋았던 점과 개선점을 도출, 이를 개선할 수 있는 방법을 모색한다 



### Scrum Team의 구성

스크럼 팀은 프로젝트 수행에 필요한 역량을 갖춘 팀으로 관련된 모든 부서로부터 팀원이 구성되고 다 같이 과제를 수행하게 됩니다. 스크럼 팀은 제품 책임자, 스크럼 마스터, 개발 팀으로 구성됩니다.

#### 제품 책임자 (Product Owner)

- 목표를 충족시키는 제품을 만들기 위해 제품 백 로그를 관리하고 제품을 검토

#### 스크럼 마스터 (Scrum Master)

- 개발 팀원들이 목표 달성과 과업에 집중할 수 있도록 팀의 문제를 해결 
- 스크럼의 가치와 실천법을 바탕으로 현장에 맞는 실천법을 정립하여 프로젝트에서 실행될 수 있도록 팀을 이끔 
- 일일 스크럼 회의를 진행하여 진행도를 모니터링
- 팀의 성공적인 목표달성을 돕기 위한 조력자 역할

![Scrum Team](https://www.visual-paradigm.com/servlet/editor-content/scrum/what-is-scrum-team/sites/7/2018/10/what-is-scrum-team.png)

이 글은 https://www.process.st/waterfall-vs-agile/, https://www.scrum.org를 참고하여 작성되었습니다. 

Curie Yoo (imported original post from travelflan dev-blog)