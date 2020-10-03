---
title: "읽기 좋은 코드가 좋은 코드다 [9/12]"
date: 2020-10-01 23:32:00 -0400
categories: 책 요약
---

## 목차
  1. [방해되는 변수를 제거하자.](#방해되는-변수를-제거하라.)
  2. [각 변수의 범위를 최대한 작게 줄이자.](#각-변수의-범위를-최대한-작게-줄여라.)
  3. [값이 한 번만 할당되는 변수를 선호하자.](#값이-한-번만-할당되는-변수를-선호하라.)

## 방해되는 변수를 제거하자.
```javascript
// bad
now = datetime.datetime.now()
root_message.last_view_time = now

// good
root_message.last_view_time = datetime.datetime.now()
```
### now 변수가 필요없는 이유
1. 복잡한 표현을 잘게 나누지 않는다.
2. 명확성에 도움이 되지 않는다.
3. 한 번만 사용되어 중복된 코드를 압축하지 않는다.

## 각 변수의 범위를 최대한 작게 줄이자.
```javascript
// bad
submitted = false;

var submit_form = function (form_name) {
  if (submitted) {
    return; // 폼을 두 번 제출하지 말라.
  }
  ...
  submitted = true;
}

// good
var submit_form = (function () {
  var submitted = false; // 주의: 아래에 있는 함수만 접근할 수 있다.

  return function (form_name) {
    if (submitted) {
      return; // 폼을 두 번 제출하지 말라.
    }
    ...
    submitted = true;
  }
}());
```
- 전역변수를 클로저 내부에 집어넣었다.

## 값이 한 번만 할당되는 변수를 선호하자.
- 값이 한 번만 할당되는 const, final 등의 변수는 훨씬 이해하기 쉽다.

## References
더스틴 보즈웰, 트레버 파우커. [_읽기 좋은 코드가 좋은 코드다._](http://www.yes24.com/Product/Goods/6692314?scode=032&OzSrank=1) n.p.: 한빛미디어(주), 2012.
