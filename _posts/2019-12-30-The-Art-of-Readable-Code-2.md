---
title: "읽기 좋은 코드가 좋은 코드다 [2/15]"
date: 2019-12-30 18:05:00 -0400
categories: 책 요약
---

## 핵심 아이디어
- 이름에 정보를 담아내라.
- 재치 있는 이름보다 명확하고 간결한 이름이 더 좋다.

## 목차

  1. [특정한 단어 고르기](#특정한-단어-고르기)
  2. [tmp나 retval 같은 보편적인 이름 피하기](#tmp나-retval-같은-보편적인-이름-피하기)
  3. [추상적인 이름보다 구체적인 이름을 선호하라](#추상적인-이름보다-구체적인-이름을-선호하라)
  4. [추가적인 정보를 이름에 추가하기](#추가적인-정보를-이름에-추가하기)
  5. [이름은 얼마나 길어야 하는가?](#이름은-얼마나-길어야-하는가?)
  6. [이름 포맷팅으로 의미를 전달하라](#이름-포맷팅으로-의미를-전달하라)

## 특정한 단어 고르기
- 매우 구체적인 단어를 선택
    ```python
    
    # bad
    def GetPage(url): # ???

    # good
    def FetchPage(url): # 인터넷에서 가져오는 페이지
    def DownloadPage(url): # 인터넷에서 가져오는 페이지
    ```

    ```java
   class BinaryTree {
       // bad
       int Size(); // ???
       
       // good
       int Height(); // 트리의 높이
       int NumNodes(); // 노드의 개수
       int MemoryBytes(); // 트리의 메모리 사용량
   };
    ```

    ```java
    class Thread {
        // bad
        void Stop();

        // good
        void Kill(); // 다시는 되돌릴 수 없는 최종 동작을 수행할 경우
        void Pause(); // Resume()을 호출하여 다시 돌이킬 수 있는 동작일 경우
    }
    ```

    ```python
    # bad
    send

    # alternative
    deliver, dispatch, announce, distribute, route

    # bad
    find

    # alternative
    search, extract, locate, recover

    # bad
    start

    # alternative
    launch, create, begin, open

    # bad
    make

    # alternative
    create, set up, build, generate, compose, add, new
    ```

## tmp나 retval 같은 보편적인 이름 피하기
- 변수값을 설명하는 이름을 사용하라.
    ```javascript
    let euclidean_norm = (v) => {
        let retval = 0.0;
        for (let i = 0; i < v.length; i++) 
            retval += v[i] * v[i];
        return Math.sqrt(retval);

        // bad
        let retval

        // good
        let sum_squares
    }
    ```

- cf) 두 변수를 교환하는 전형적인 알고리즘
    ```javascript
    if (right < left) {
        tmp = right;
        right = left;
        left = tmp;
    }
    ```

- tmp라는 이름은 짧게 임시적으로만 존재하고, 존재 자체가 변수의 가장 중요한 용도일 때에 한해서 사용해야 한다.

- 루프반복자의 더 좋은 이름
    ```c++
    for (int i = 0; i < clubs,size(); i++)
        for (int j = 0; j < clubs[i].members.size(); j++)
            for (int k = 0; k < users.size(); k++)
                if (clubs[i].members[k] == users[j])
                    cout << "user[" << j << "] is in club[" << i << end1;
    
    // bad
    i, j, k

    // good
    club_i, members_i, users_i or ci, ui, mi
    ```

- tmp, it, retval 같은 보편적인 이름을 사용하려면, 꼭 그렇게 해야 하는 이유가 있어야 한다.

## 추상적인 이름보다 구체적인 이름을 선호하라
```javascript
// bad
const serverCanStart()

// good
const canListenOnPort()
```

## 추가적인 정보를 이름에 추가하기
```c++
// bad
string id;

// good
string id; // Example: "af84ef845cd8"
```
- 단위를 포함하는 값들
    ```javascript
    let start = (new Data()).getTime(); // 페이지의 맨 위

    // bad
    let elased = (new Data()).getTime() - start; // 페이지의 맨 아래

    // good
    let elased_ms = (new Data()).getTime() - start; // 페이지의 맨 아래

    document.writeIn("Load time was: " + elased_ms / 1000 + " seconds");
    ```

    ```javascript
    // bad
    delay

    // good
    delay_secs

    // bad
    size

    // good
    size_mb

    // bad
    limit

    // good
    max_kbps

    // bad
    angle

    // good
    degrees_cw
    ```

- 다른 중요한 속성 포함하기
    ```javascript
    상황: 패스워드가 'plaintext'에 담겨 있고, 추가적인 처리를 하기 전에 반드시 암호화되어야 한다.
    
    // bad
    const password
    
    // good
    const plaintext_password

    상황: 사용자에게 보여지는 설명문이 화면에 나타나기 전에 이스케이프 처리가 되어야 한다.

    // bad
    const comment

    // good
    const unexcaped_comment

    상황: html의 바이트가 UTF-8으로 변환되었다.

    // good
    const html

    // bad
    const html_utf8

    상황: 입력데이터가 'url encoded'되었다.

    // bad
    const data

    // good
    const data_urlenc
    ```

## 이름은 얼마나 길어야 하는가?
- 좁은 범위에서는 짧은 이름이 괜찮다.
    ```c#
    if (debug) {
        map<string,int> m;
        LookUpNamesNumbers(&m);
        Print(m);
    }
    ```
- 긴 이름 입력하기
- 약어와 축약형: 팀에 새로 합류한 사람이 이해할 수 있는가?
    ```javascript
    // bad
    const BEManager

    // good
    const BackEndManger
    ```

- 불필요한 단어 제거하기
    ```javascript
    // bad
    ConverToString(), DoServeLoop()

    // good
    ToString(), ServeLoop()
    ```

## 이름 포맷팅으로 의미를 전달하라
- CamelCase
- '생성자'를 대문자로, 다른 평범한 함수는 소문자로 표기
    ```javascript
    var x = new DatePicker(); // 생성자 함수
    var y = pageHeight(); // 평범한 함수
    ```
- jQuery의 결과를 저장하는 변수 앞에 $붙이는 관습
    ```javascript
    ar $all_images = $("img"); // $all_images는 jQuery의 객체
    ar height = 250;
    ```
- HTML/CSS 밑줄로 id 구분, 대시로 class 구분
    ```html
    <div id="middle_column" class="main-content"> ...
    ```

## References
더스틴 보즈웰, 트레버 파우커. [_읽기 좋은 코드가 좋은 코드다._](http://www.yes24.com/Product/Goods/6692314?scode=032&OzSrank=1) n.p.: 한빛미디어(주), 2012.
