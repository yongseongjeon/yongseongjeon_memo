---
title: "읽기 좋은 코드가 좋은 코드다 [12/15]"
date: 2020-10-07 23:40:00 -0400
categories: 책 요약
---

## 목차
  1. [코드를 더 명확하게 만드는 과정](#코드를-더-명확하게-만드는-과정)
  2. [논리를 명확하게 설명하기](#논리를-명확하게-설명하기) 

## 코드를 더 명확하게 만드는 과정
1. 코드가 할 일을 옆의 동료에게 말하듯이 평범한 영어로 묘사하라.
2. 이 설명에 들어가는 핵심적인 단어와 문구를 포착하라.
3. 설명과 부합하는 코드를 작성하라.

## 논리를 명확하게 설명하기.
```javascript
// bad
const $is_admin = is_admin_request();
if ($document) {
  if (!$is_admin && ($document['username'])) {
    return not_authorized();
  }
} else {
  if (!$is_admin) {
    return not_authorized();
  }
}

// good
if (is_admin_request()) {
  // 허가
} else if ($document && (&document['username'] === $_SESSION['username'])) {
  // 허가
} else {
  return not_authorized();
}
```
### 아래의 코드가 더 좋은 이유
1. 코드의 분량이 더 적다.
2. 부정문이 없어 논리문이 더 간단해졌다.

## References
더스틴 보즈웰, 트레버 파우커. [_읽기 좋은 코드가 좋은 코드다._](http://www.yes24.com/Product/Goods/6692314?scode=032&OzSrank=1) n.p.: 한빛미디어(주), 2012.
