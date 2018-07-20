---
layout: post
title:  "[javaScript] mCustomScrollbar에서 scrollTop, scrollBottom 설정"
date:   2018-07-20
categories: javascript
author : "Junny"
permalink: /:categories/:title
---
# [javaScript] mCustomScrollbar에서 scrollTop, scrollBottom 설정

커스텀 스크롤 바 중에서 mCustomScrollbar 라는 간단한 자바스크립트 기능이 있다.

이 스크롤바를 적용하면 일반적인 $(selector).scrollTop() 기능이 작동하지 않는다.

그래서 찾아본 결과 mCustomScrollbar에 있는 스크롤 기능을 설정하면 된다.

## 사용 방법
~~~
$('#btntop').on('click',function() {	// 버튼 클릭 설정
		//스크롤이 적용된 해당 div 셀렉트
		$('.container').mCustomScrollbar("scrollTo","top",{  
		// "mCustomScrollbar에 있는 scrollTo 함수를 사용", "top, bottom" 설정
		    scrollInertia:1000 // 이동에 걸리는 시간 설정
		});
	});
$('#btnbottom').on('click',function() {	// 버튼 클릭 설정
		//스크롤이 적용된 해당 div 셀렉트
		$('.container').mCustomScrollbar("scrollTo","bottom",{  
		// "mCustomScrollbar에 있는 scrollTo 함수를 사용", "top, bottom" 설정
		    scrollInertia:1000 // 이동에 걸리는 시간 설정
		});
	});
~~~
올라가는 스크롤 시간도 설정할 수 있다. 맨위로, 맨아래로 두개의 버튼에 설정해주어야한다.

###### 참고 사이트 <a href="http://manos.malihu.gr/jquery-custom-content-scroller/">http://manos.malihu.gr/jquery-custom-content-scroller/</a>