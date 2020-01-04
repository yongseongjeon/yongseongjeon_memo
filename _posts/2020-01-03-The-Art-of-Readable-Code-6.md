---
title: "읽기 좋은 코드가 좋은 코드다 [6/12]"
date: 2020-01-03 19:38:00 -0400
categories: 책 요약
---

## 핵심 아이디어
- 주석은 높은 '정보 대 공간' 비율을 갖춰야 한다.

## 목차
  1. [it 이나 this 같은 대명사가 여러 가지를 가리킬 수 있다면 사용하지 말라](#it-이나-this-같은-대명사가-여러-가지를-가리킬-수-있다면-사용하지-말라)
  2. [함수의 동작을 실제로 할 수 있는 한도 내에서 명확하게 설명하라](#함수의-동작을-실제로-할-수-있는-한도-내에서-명확하게-설명하라)
  3. [신중하게 선택된 입/출력 예로 주석을 서술하라](#신중하게-선택된-입/출력-예로-주석을-서술하라)
  4. [코드가 가진 의도를 너무 자세한 내용이 아니라 높은 수준에서 개괄적으로 설명하라](#코드가-가진-의도를-너무-자세한-내용이-아니라-높은-수준에서-개괄적으로-설명하라)
  5. [같은 줄에 있는 주석으로 의미가 불분명한 함수의 인수를 설명하라](#같은-줄에-있는-주석으로-의미가-불분명한-함수의-인수를-설명하라)
  6. [많은 의미를 함축하는 단어로 주석을 간단하게 만들라](#많은-의미를-함축하는-단어로-주석을-간단하게-만들라)

## it 이나 this 같은 대명사가 여러 가지를 가리킬 수 있다면 사용하지 말라
- 모호한 대명사는 피하라
    ```javascript
    // bad

    // Insert the data into the cache, but check if it's too big first.
    // 데이터를 캐시에 넣어라. 하지만 그것이 너무 큰지 먼저 확인하라.
    
    // good

    // Insert the data into the cache, but check if the data is too big first.
    // 데이터를 캐시에 넣어라. 하지만 데이터가 너무 큰지 먼저 확인하라.

    // If the data is small enough, insert it into the cache.
    // 데이터가 충분히 작으면, 이를 캐시에 넣어라.
    ```

## 신중하게 선택된 입/출력 예로 주석을 서술하라
- 코너케이스를 설명해주는 입/출력 예를 사용하라
  ```c++
  // good

  // 입력된 'src'의 'chars'라는 접두사와 접미사를 제거한다.
  String Strip(String src, String chars) { ... }
  ```


## References
더스틴 보즈웰, 트레버 파우커. [_읽기 좋은 코드가 좋은 코드다._](http://www.yes24.com/Product/Goods/6692314?scode=032&OzSrank=1) n.p.: 한빛미디어(주), 2012.