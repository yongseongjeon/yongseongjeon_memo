---
title: "읽기 좋은 코드가 좋은 코드다 [1/12]"
date: 2019-12-29 16:38:00 -0400
categories: 책 요약
---

## 목차

  1. [무엇이 코드를 '더 좋게' 만드는가?](#1.1)

## 무엇이 코드를 '더 좋게' 만드는가?
- 1.1 코드는 이해하기 쉬워야 한다.
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

- 1.2 코드는 다른 사람이 그것을 이해하는 데 들이는 시간을 최소화하는 방식으로 작성되어야 한다.

## References
더스틴 보즈웰, 트레버 파우커. _읽기 좋은 코드가 좋은 코드다._ n.p.: 한빛미디어(주), 2012.
