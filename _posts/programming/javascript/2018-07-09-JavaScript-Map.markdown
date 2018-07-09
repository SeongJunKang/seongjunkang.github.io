---
layout: post
title:  "javaScript Map 객체 사용"
date:   2018-07-09
categories: javascript
author : "Junny"
permalink: /:categories/:title
---

# JavaScript Map 객체 사용
 
 Java의  Map처럼 자바스크립트도 map 객체가 있습니다
 간혹 사용할 일이 있기 때문에, 사용 예제를 적어두겠습니다.

## 사용 방법
~~~
//변수 선언
var map = new Map();
var key = 1;
var value = "value";
var value2 = "value2";
map.set(key,value);
console.log(map.get(key));
~~~
한가지 알아야 할 점이 있다면, 자바와 마찬가지로 키를 주의하셔야 합니다.

~~~
map.set("1",value2);
map.set(1,value);

console.log(map.get(1));
console.log(map.get("1"));
~~~
두 결과의 값이 다르게 나옵니다.  문자형과 숫자형을 혼용하면서 쓰면 헷갈릴 수 있으니 주의 하시기 바랍니다.

![map 결과](/assets/image/javascript/map/map.png)

자세한 내용은 아래의 링크를 참고하시면 됩니다.
참고 : https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Map