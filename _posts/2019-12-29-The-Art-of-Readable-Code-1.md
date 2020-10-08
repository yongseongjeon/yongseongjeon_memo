---
title: "읽기 좋은 코드가 좋은 코드다 [1/15]"
date: 2019-12-29 16:38:00 -0400
categories: 책 요약
---

## 핵심 아이디어
- 코드는 이해하기 쉬워야 한다.
- 코드는 다른 사람이 그것을 이해하는 데 들이는 시간을 최소화하는 방식으로 작성되어야 한다.

## 목차

  1. [무엇이 코드를 '더 좋게' 만드는가?](#무엇이-코드를-'더-좋게'-만드는가?)

## 무엇이 코드를 '더 좋게' 만드는가?
```c++
// bad
Node* node = list->head;
if (node === NULL) return;

while (node-next != NULL) {
    Print(node->data);
    node = node->next;
}
if (node != NULL) Print(node->data);

// good
for (Node* node = list->head; node != NULL; node = node->next)
    Print(node->data);
```

```c++
// bad
return exponent >= 0 ? mantissa * (1 << exponent) : mantissa / (1 << -exponent);

// good
if (exponent >= 0) {
    return mantissa * (1 << exponent);
} else {
    return mantissa / (1 << -exponent);
}
```

## References
더스틴 보즈웰, 트레버 파우커. [_읽기 좋은 코드가 좋은 코드다._](http://www.yes24.com/Product/Goods/6692314?scode=032&OzSrank=1) n.p.: 한빛미디어(주), 2012.
