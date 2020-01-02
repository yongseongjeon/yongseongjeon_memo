---
title: "읽기 좋은 코드가 좋은 코드다 [5/12]"
date: 2020-01-02 22:47:00 -0400
categories: 책 요약
---

## 핵심 아이디어
- 주석의 목적은 코드를 읽는 사람이 코드를 작성한 사람만큼 코드를 잘 이해하게 돕는 데 있다.
- 코드에서 빠르게 유추할 수 있는 내용은 주석으로 달지 말라.

## 목차
  1. [코드 자체에서 쉽게 알아낼 수 있는 사실은 설명하지 말라](#코드-자체에서-쉽게-알아낼-수-있는-사실은-설명하지-말라)
  2. [나쁜 코드를 보정하려고 '애쓰는 주석'을 작성하지 말라](#나쁜-코드를-보정하려고-'애쓰는-주석'을-작성하지-말라)
  3. [코드가 특정한 방식으로 작성된 이유를 설명해주는 내용(감독의 설명)](#코드가-특정한-방식으로-작성된-이유를-설명해주는-내용(감독의-설명))
  4. [코드에 담긴 결함. TODO: 혹은 XXX:와 같은 표시를 사용하라](#코드에-담긴-결함.-TODO:-혹은-XXX:와-같은-표시를-사용하라)
  5. [어떤 상수가 특정한 값을 갖게 된 사연](#어떤-상수가-특정한-값을-갖게-된-사연)
  6. [코드를 읽는 사람의 생각을 예측하여 주석을 추가하라](#코드를-읽는-사람의-생각을-예측하여-주석을-추가하라)
  7. [파일이나 클래스 수준 주석에서 '큰 그림'을 설명하고 각 조각이 어떻게 맞춰지는지 설명하라](#파일이나-클래스-수준-주석에서-'큰-그림'을-설명하고-각-조각이-어떻게-맞춰지는지-설명하라)

## 코드 자체에서 쉽게 알아낼 수 있는 사실은 설명하지 말라
- 설명하지 말아야 하는 것
    ```java
    // bad
    class Account {
        public:
        // 생성자
        Account();

        // profit에 새로운 값을 설정
        void SetProfit(double profit);

        // 이 어카운트의 profit을 반환
        double GetProfit();
    };
    ```
- 설명 자체를 위한 설명을 달지 말라
    ```c++
    // bad
    
    // 주어진 이름과 깊이를 이용해서 서브트리[h1]에 있는 노드를 찾는다.
    Node* FindNodeInSubtree(node* subtree, string name, int depth);

    // good

    // 주어진 'name'으로 노드를 찾거나 아니면 NULL을 반환한다.
    // 만약 depth <= 0이면 'subtree'만 검색된다.
    // 만약 depth == N 이면 N 레벨과 그 아래만 검색된다.
    Node* FindNodeInSubtree(node* subtree, string name, int depth);
    ```

## 나쁜 코드를 보정하려고 '애쓰는 주석'을 작성하지 말라
- 나쁜 이름에 주석을 달지 마라 - 대신 이름을 고쳐라
    ```java
    // bad

    // 반환되는 항목의 수나 전체 바이트 수와 같이
    // Request가 정하는 대로 Reply에 일정한 한계를 적용한다.
    void CleanReply(request request, Reply reply);

    // good

    // 'reply'가 count/byte/등과 같이 'request'가 정하는 한계조건을 만족시키도록 한다.
    void EnforceLimitsFromRequest(request request, Reply reply);
    ```

## 코드가 특정한 방식으로 작성된 이유를 설명해주는 내용(감독의 설명)
- 생각을 기록하라
    ```javascript
    // good

    // 이 주먹구구식 논리는 몇 가지 단어를 생략할 수 있다. 상관없다. 100% 해결은 쉽지 않다.

    // 이 클래스는 점점 엉망이 되어가고 있따. 어쩌면 'ResourceNode' 하위 클래스를
    // 만들어서 정리해야 할지도 모르겠다.
    ```

## 코드에 담긴 결함. TODO: 혹은 XXX:와 같은 표시를 사용하라
- 코드에 있는 결함을 설명하라
    ```javascript
    // good

    // TODO: 더 빠른 알고리즘을 사용하라.
    // TODO(더스틴): JPEG말고 다른 이미지 포맷도 처리할 수 있어야 한다.
    ```
    | 표시      | 보통의 의미                |
    |----------|-------------------------|
    | TODO:    | 아직 하지 않은 일           |
    | FIXME:   | 오작동을 일으킨다고 알려진 코드 |
    | HACK:    | 아름답지 않은 해결책         |
    | XXX:     | 위험! 여기 큰 문제가 있다     |
    | TextMate | ESC                     |

## 어떤 상수가 특정한 값을 갖게 된 사연
- 상수에 대한 설명
    ```javascript
    // bad
    NUM_THREADS = 8

    // good
    NUM_THREADS = 8 // 이 상수값이 2 * num_processor보다 크거나 같으면 된다.

    // 합리적인 한계를 설정하라 - 그렇게 많이 읽을 수 있는 사람은 어차피 없다.
    const MAX_RSS_SUBSCRIPTIONS = 1000;

    image_quality = 0.72; // 사용자들은 0.72가 크기/해상도 대비 최선이라고 생각한다.
    ```

## 코드를 읽는 사람의 생각을 예측하여 주석을 추가하라
- 코드를 읽는 사람의 입장이 되어라
    ```java
    // good

    // 외부 서비스를 호출하여 이메일 서비스를 호출한다(1분 이후 타임아웃된다).
    void SendEmail(string to, string subject, string body);
    ```

## 파일이나 클래스 수준 주석에서 '큰 그림'을 설명하고 각 조각이 어떻게 맞춰지는지 설명하라
- 파일수준 주석
    ```javascript
    // 파일시스템에 편리한 인터페이스를 제공하는 헬퍼 함수들을 담고 있다.
    // 파일의 퍼미션과 다른 자세한 세부사항을 처리한다.
    ```
- 요약 주석
    ```python
    # 고객이 자신을 위해서 구입한 항목을 모두 찾는다.
    for customer_id in all_customers:
        for sale in all_sales[customer_id].sales:
            if sale.recipient == customer_id:
    ```

## References
더스틴 보즈웰, 트레버 파우커. [_읽기 좋은 코드가 좋은 코드다._](http://www.yes24.com/Product/Goods/6692314?scode=032&OzSrank=1) n.p.: 한빛미디어(주), 2012.
