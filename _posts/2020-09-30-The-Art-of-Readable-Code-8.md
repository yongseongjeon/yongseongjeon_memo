---
title: "읽기 좋은 코드가 좋은 코드다 [8/15]"
date: 2020-09-30 23:32:00 -0400
categories: 책 요약
---

## 핵심 아이디어
- 거대한 표현을 더 소화하기 쉬운 여러 조각으로 나눈다.

## 목차
  1. [커다란 하위표현을 대체하는 '설명 변수'를 도입하기.](#커다란-하위표현을-대체하는-'설명-변수'를-도입하기.)
  2. [드모르간의 법칙](#드모르간의-법칙)

## 커다란 하위표현을 대체하는 '설명 변수'를 도입하기.
- 설명 변수
  ```javascript
  // bad
  if (line.split(':')[0]) === "root":

  // good
  const username = line.split(':')[0]
  if (username == "root") {
    ...
  }
  ```

- 요약 변수
  ```javascript
  // bad
  if (request.user.id === doc.owner_id) {
    // 사용자가 이 문서를 수정할 수 있다.
  }
  if (request.user.id !== doc.owner_id) {
    // 문서는 읽기전용이다.
  }

  // good
  const user_owns_document = request.user.id === doc.owner_id;
  if (user_owns_document) {
    // 사용자가 이 문서를 수정할 수 있다.
  }
  if (!user_owns_document) {
    // 문서는 읽기전용이다.
  }
  ```
## 드모르간의 법칙
- 드모르간의 법칙 사용하기
  ```
  1) not (a or b or c ) <=> (not a) and (not c)
  2) not (a and b and c) <=> (not a) or (not b) or (not c)
  
  not을 분배하고 and/or를 바꾸자.
  ```


## References
더스틴 보즈웰, 트레버 파우커. [_읽기 좋은 코드가 좋은 코드다._](http://www.yes24.com/Product/Goods/6692314?scode=032&OzSrank=1) n.p.: 한빛미디어(주), 2012.
