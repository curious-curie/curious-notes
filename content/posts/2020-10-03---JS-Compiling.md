---
title: "[JS] V8 엔진과 JIT 컴파일러"
date: "2020-10-03T22:40:32.169Z"
template: "post"
draft: false
slug: "js-engine-v8"
category: "Javascript"
tags:
  - "Javascript"
  - "Web Development"
description: "자바스크립트는 인터프리터 언어랬는데, 컴파일 과정을 거친다는 말이 왜 나올까?"
socialImage: ""
---

자바스크립트 엔진은 자바스크립트 코드를 실행하는 프로그램 / 인터프리터이다.

V8은 구글의 자바스크립트 엔진이다. JIT 컴파일러를 사용하여 구현되었다.

자바스크립트는 인터프리터 언어랬는데, 컴파일 과정을 거친다는 말이 왜 나올까?

필자는 자바스크립트는 컴파일 과정을 거치지 않으므로, 바벨과 같은 AST의 생성 과정을 거치지 않을 것이라고 생각했는데 단단한 오해였다.

## V8 엔진 그리고 JIT compiler

구글이 만든 자바스크립트 엔진

구글 크롬에서 사용됨. C++로 제작되었다.

V8은 웹 브라우저 내부에서 자바스크립트 수행 속도의 개선을 목적으로 고안되었다.

그래서 속도 향상을 위해 인터프리터를 사용하는 대신 Just In Time 컴파일러를 사용하여 효율적인 머신 코드로 번역한다고 한다 (!!!)

자바스크립트를 바이트코드로 컴파일하고 실행하는 방식을 사용하며, 인라인 캐싱 등의 최적화 기법을 적용하여 추가적인 속도 향상을 실현하였다.

### V8 컴파일 과정

- 파서가 소스코드를 분석한 후 **토큰**을 생성한다.
- 이 토큰을 파서가 **AST** (추상 구문 트리)로 변환시킨다 ( ⇒ 파싱! )
- Ignition이라는 인터프리터가 AST를 **바이트 코드**로 변환한다.
- 바이트코드를 실행하면서 최적화 해야 하는 데이터 (자주 쓰이는 코드)는 TurboFan을 통해 최적화된다. ⇒ Optimized Machine Code를 생성한다.
- 이 코드가 자주 쓰이지 않으면 다시 Deoptimize 되기도 한다.

### TurboFan의 최적화

V8은 TurbonFan을 이용하여 메모리 사용량 감소, 실행시간 단축, 코드 크기를 줄이고 속도 향상 시킨다.

```jsx
// v8/src/execution/rumtime-profiler.cc
OptimizationReason RuntimeProfiler::ShouldOptimize(JSFunction function, BytecodeArray bytecode) {
  // int ticks = 이 함수가 몇번 호출되었는지
  int ticks = function.feedback_vector().profiler_ticks();
  int ticks_for_optimization =
      kProfilerTicksBeforeOptimization +
      (bytecode.length() / kBytecodeSizeAllowancePerTick);
  if (ticks >= ticks_for_optimization) {
    // 함수가 호출된 수가 임계점인 ticks_for_optimization을 넘기면 뜨거워진 것으로 판단
    return OptimizationReason::kHotAndStable;
  } else if (!any_ic_changed_ && bytecode.length() < kMaxBytecodeSizeForEarlyOpt) {
    // 이 코드가 인라인 캐싱되지 않았고 바이트 코드의 길이가 작다면 작은 함수로 판단
    return OptimizationReason::kSmallFunction;
  }
  // 해당 사항 없다면 최적화 하지 않는다.
  return OptimizationReason::kDoNotOptimize;
}
```

해당 코드 및 주석 출처: [https://evan-moon.github.io/2019/06/28/v8-analysis/](https://evan-moon.github.io/2019/06/28/v8-analysis/)

- Hot And Stable한 경우 : 자주 호출되고, 코드가 변하지 않는 경우
- Small Function인 경우 : 바이트코드의 길이가 특정 기준치 이하인 경우 최적화를 진행한다
