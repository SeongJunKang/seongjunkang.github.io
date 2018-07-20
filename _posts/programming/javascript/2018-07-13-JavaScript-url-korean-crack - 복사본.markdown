---
layout: post
title:  "[javaScript] URL 한글 문자 깨짐 현상"
date:   2018-07-13
categories: javascript
author : "Junny"
permalink: /:categories/:title
---
# [JavaScript] URL 한글 문자 깨짐 현상 해결

간혹 URL에 한글을 사용할 때가 있다.  

크롬은 자동으로 URL 인코딩을 하고 보여줄 때는 한글로 보여주지만,  

익스플로러에서는 안되는 경우가 생긴다.  

클라이언트 익스플로러의 버전이 몇인지 모르기 때문에 설정 해주는 것이 좋다.  

  
방법은 간단한다.
## 사용 방법
~~~
location.href =  "/test.do?param=한글";
~~~
위와 같이 썻다고 가정한다면 다음과 같이 변경하면 된다.

~~~
location.href =  "/test.do?param="+encodeURIComponent("한글");
~~~
자바스크립트 내장 함수 encodeURIComponent를 사용하면 된다.

###### 이 포스팅은 이전 블로그에서 가져온 것입니다.
<a href="https://blog.naver.com/tjdwns8574/221308461013">https://blog.naver.com/tjdwns8574/221308461013</a>