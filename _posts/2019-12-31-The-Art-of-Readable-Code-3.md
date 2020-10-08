---
title: "읽기 좋은 코드가 좋은 코드다 [3/15]"
date: 2019-12-31 14:47:00 -0400
categories: 책 요약
---

## 핵심 아이디어
- 본인이 지은 이름을 "다른 사람들이 다른 의미로 해석할 수 있을까?"라는 질문을 던져보며 철저하게 확인해야 한다.

## 목차
  1. [예: Filter()](#예:-Filter())
  2. [예: Clip(text, length)](#예:-Clip(text,-length))
  3. [경계를 포함하는 한계값을 다룰 때는 min과 max를 사용하라](#경계를-포함하는-한계값을-다룰-때는-min과-max를-사용하라)
  4. [경계를 포함하는 범위에는 first와 last를 사용하라](#경계를-포함하는-범위에는-first와-last를-사용하라)
  5. [경계를 포함하고/배제하는 범위에는 begin과 end를 사용하라](#경계를-포함하고/배제하는-범위에는-begin과-end를-사용하라)
  6. [불리언 변수에 이름 붙이기](#불리언-변수에-이름-붙이기)
  7. [사용자의 기대에 부응하기](#사용자의-기대에-부응하기)
  8. [예: 이름을 짓기 위해서 복수의 후보를 평가하기](#예:-이름을-짓기-위해서-복수의-후보를-평가하기)

## 예: Filter()
- 대상을 고르는 것인지 제거하는 것인지 불분명함.
    ```javascript
    results = Database.all_objects.filter("year <= 2011")
    // year <= 2011 ?
    // year > 2011 ?

    // bad
    filter()

    // good
    select(), exclude()
    ```

## 예: Clip(text, length)
- 문단의 어디서부터 자르는지 불분명함.
    ```python
    # bad
    def Clip(text, length):

    # good
    def Truncate(text, max_chars)
    ```

## 경계를 포함하는 한계값을 다룰 때는 min과 max를 사용하라
- 한계를 설정하는 이름을 가장 명확하게 만드는 방법은 제한받는 대상의 이름 앞에 max_나 min_을 붙이는 것이다.
    ```python
    # bad
    CART_TOO_BIG_LIMIT = 10

    if shopping_cart.num_items() >= CART_TOO_BIG_LIMIT:
        Error("Too many items in cart.")

    # good
    MAX_ITEMS_IN_CART = 10

    if shopping_cart.num_items() > MAX_ITEMS_IN_CART:
        Error("Too many items in cart.")
    ```

## 경계를 포함하는 범위에는 first와 last를 사용하라
- stop은 여러 가지 방식으로 해석될 수 있다.
    ```python
    # bad
    print interger_range(start=2, stop=4)

    # good
    set.PrintKeys(first="Bart", last="Maggie")
    ```

## 경계를 포함하고/배제하는 범위에는 begin과 end를 사용하라
- 포함/배제가 동시에 일어나면 begin/end를 사용하는 전형적인 프로그래밍 관행이 있다.

## 불리언 변수에 이름 붙이기
- is, has, can, should와 같은 단어를 더하면 불리언값의 의미가 더 명확해진다.
    ```c++
    // bad
    bool read_password = true;

    // good
    bool need_password || bool user_is_authenticated
    ```
    ```c++
    // bad
    bool SpaceLeft()

    // good
    bool HasSpaceLeft()
    ```
- 의미를 부정하는 용어를 피하는 것이 좋다.
    ```c++
    // bad
    bool disable_ssl = false;

    // good
    bool use_ssl = true;
    ```

## 사용자의 기대에 부응하기
- 예: get*()
  - 프로그래머드들은 대개 get으로 시작되는 이름의 메소드는 '가벼운 접근자'로서 단순히 내부 멤버를 반환한다고 관행적으로 생각한다.
    ```java
    // bad
    public double getMean() {
        // 모든 샘플을 반복한 다음 total / num_samples를 반환하다.
        ...
    }

    // good
    public double computeMean() {
        ...
    }
    ```

- 예: list::size()
  - C++ 표준 라이브러리에서는 size()는 O(1)이라는 규칙을 정했다.
    ```c++
    // bad
    void ShirinkList(list<Node>&, int max_size) {
        while (list.size() > max_size) { 
            // list.size()가 O(n)연산 일경우
            // ShirinkList는 O(n^2)연산이 된다.
        }
    }

    // good
    void ShirinkList(list<Node>&, int max_size) {
        while (list.countSize() > max_size) { 
            // size() 대신 countSize() || countElements()
        }
    }
    ```

## 예: 이름을 짓기 위해서 복수의 후보를 평가하기
- 100번 실험의 내용을 그대로 복사 붙여 넣어야 할 때
- template, reuse, copy, inherit 중에서 inherit가 적합함
```python
    experiment_id: 101
    
    # bad
    the_other_experiment_id_I_want_to_reuse: 100

    # good
    inherit_from || inherit_from_experiment_id: 100
```

## References
더스틴 보즈웰, 트레버 파우커. [_읽기 좋은 코드가 좋은 코드다._](http://www.yes24.com/Product/Goods/6692314?scode=032&OzSrank=1) n.p.: 한빛미디어(주), 2012.
