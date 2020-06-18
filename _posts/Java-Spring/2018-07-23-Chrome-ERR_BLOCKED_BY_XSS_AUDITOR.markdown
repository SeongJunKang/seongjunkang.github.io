---
layout: post
title:  "[Java] Chrome에서 ERR_BLOCKED_BY_XSS_AUDITOR 에러"
date:   2018-07-23
categories: [Java/Spring]
author : "Junny"
tags: [Chome, ERR_BOLCED_BY_XSS_AUDITOR]
---
# [Java] Chrome에서 ERR_BLOCKED_BY_XSS_AUDITOR 에러

javascript에서 jquery로 데이터를 html()를 사용해서 post로 넘기려고 하니 크롬에서 에러가 났다.


~~~
	var popPrint = window.open('', "popup", 'location=no, directories=no, resizable=no, status=no, toolbar=no, menubar=no, width=900, height=720, scrollbars=yes');
	$('#formPrint #content').val($('#Contents').html());
~~~


이런 방식으로 post를 사용해서 전송했더니 다음과 같은 에러가 발생했다.


![ERR_BLOCKED_BY_XSS_AUDITOR 에러](/assets/image/java/chrome/ERR_BLOCKED_BY_XSS_AUDITOR.PNG)


구글링을 해본결과 크롬에서 보안상으로 X-XSS-Protection을 설정해 막아놨다고 한다.
보안과 관련이 없는 데이터를 전송할 경우에는 서버단에서 리스폰즈에 X-XSS-Protection를 0으로 설정하면 된다.
이것은 보안을 푸는 행위이니 실제 비밀번호나 다른 데이터를 입력할 경우는 설정하지 말길 바란다.
Java에서 HttpServletResponse response에다가 설정했더니 됬다.

설정코드
~~~
response.addHeader("X-XSS-Protection", "0");
~~~
