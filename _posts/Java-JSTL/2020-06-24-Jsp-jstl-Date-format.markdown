---
layout: post
title:  "[Jstl] JSP에서 jstl Date Format"
date:   2020-06-24
categories: [Java/JSTL]
author : "Junny"
tags : [Java,Jsp,JSTL]
---
# [Jstl] JSP에서 jstl Date Format

date를 DB에서 가져오면 가져온 그대로 뿌려주기 때문에 가독성이 떨어질 수 있다.<br>
JSTL에서 format을 설정해주면 해당 설정값으로 날짜를 나타낼 수 있다.<br>
아래의 태그 라이브러리(format) fmt를 상단에 선언해줘야한다.<br>
~~~
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %>
~~~


예시)<br>
변환전<br>
![Unformatted date](/assets/image/java/jstl/jstl-date-unformat.png)

변환 코드<br>
~~~
<fmt:formatDate value="${date}" pattern="yyyy-MM-dd hh:mm:ss"/>
~~~

변환후<br>
![formatted date](/assets/image/java/jstl/jstl-date-format.png)<br>


fmt 태그는 숫자의 변환에서도 사용한다. 보통 3자리수 patten 으로 #,###을 이용하면 3자리마다 콤마를 붙일 때 사용한다.