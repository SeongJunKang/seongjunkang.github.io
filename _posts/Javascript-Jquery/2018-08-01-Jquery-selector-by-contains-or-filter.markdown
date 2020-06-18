---
layout: post
title:  "[Jquery] 문자열을 포함한 또는 동일한 Selector"
date:   2018-08-01
categories: [JavaScript/Jquery]
author : "Junny"
---
# [Jquery] 문자열을 포함한 또는 동일한 Selector


이번에 포스팅할 것은 Jquery를 사용하여 selector에 들어있는 문자열로 선택하는 선택하는 방법이다.  
셀렉터를 사용해 문자열이 포함되는 것만 선택할 수 있다.

## 사용 방법
1.  :contains 를 사용하는 방법
~~~
$('a:contains("문자열")');
~~~
'문자열' 이 들어간 모든 \<a>태그를 선택한다.

2. filter를 사용하는 방법
~~~
$('a').filter(function()  {  
	return  $(this).text()  ===  "문자열";  
});
~~~
해당 텍스트와 완전히 동일한 것만 선택해주는 방법이다.
filter는 text 말고도 hasClass와 같은 다른 방법으로도 응용이 가능하니 알아두면 좋다.
<br>
<br>

###### 내 네이버 블로그 <a href="https://blog.naver.com/tjdwns8574/221330571116/">https://blog.naver.com/tjdwns8574/221330571116</a>