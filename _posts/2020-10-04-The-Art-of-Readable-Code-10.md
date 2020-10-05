---
title: "읽기 좋은 코드가 좋은 코드다 [10/12]"
date: 2020-10-04 23:40:00 -0400
categories: 책 요약
---

## 목차
  1. [일반적인 목적의 코드를 프로젝트의 특정 코드에서 분리하라.](#일반적인-목적의-코드를-프로젝트의-특정-코드에서-분리하라.)

## 일반적인 목적의 코드를 프로젝트의 특정 코드에서 분리하라.
```javascript
// bad
ajax_post({
  url: 'http://example.com/submit',
  data: data,
  on_success: function (response_data) {
    var str = '{\n';
    for (var key in response_data) {
      str += ' ' + key + ' = ' + response_data[key] + '\n';
    }
    alert(str + '}');

    ...
  }
})
// good
var format_pretty = function (obj) {
  var str = '{\n';
  for (var key in obj) {
    str += ' ' + key + ' = ' + obj[key] + '\n';
  }
  return str + '}';
};

ajax_post({
  url: 'http://example.com/submit',
  data: data,
  on_success: function (response_data) {
    // format_pretty(response_data)
    ...
  }
})
```
### format_pretty()를 추출하면 좋은 이유
1. 함수를 호출하는 코드를 간단하게 만든다.
2. 다른곳에서도 간편하게 사용할 수 있다.
3. 필요할 떄 format_pretty 함수를 손쉽게 개선할 수 있다.


## References
더스틴 보즈웰, 트레버 파우커. [_읽기 좋은 코드가 좋은 코드다._](http://www.yes24.com/Product/Goods/6692314?scode=032&OzSrank=1) n.p.: 한빛미디어(주), 2012.
