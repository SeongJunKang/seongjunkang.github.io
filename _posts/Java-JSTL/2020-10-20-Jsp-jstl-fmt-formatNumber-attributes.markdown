---
layout: post
title:  "[Jstl] JSP에서 formatNumber 속성 설명(JSTL formatNumber attributes)
date:   2020-10-20
categories: [Java/JSTL]
author : "Junny"
tags : [Java,Jsp,JSTL]
---
# [Jstl] JSP에서 formatNumber 속성 설명

date를 DB에서 가져오면 가져온 그대로 뿌려주기 때문에 가독성이 떨어질 수 있다.<br>
JSTL에서 format을 설정해주면 해당 설정값으로 날짜를 나타낼 수 있다.<br>
아래의 태그 라이브러리(format) fmt를 상단에 선언해줘야한다.<br>
~~~
//Standard Syntax:
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %>

//XML Syntax:
<anyxmlelement xmlns:fmt="http://java.sun.com/jsp/jstl/fmt" />
~~~


<br>
fmt에서 formatNumber 태그는 숫자에 관련된 포맷 태그입니다.


formatNumber 속성 
----------------------
|속성명|설명|필수여부|
|:---:|:---:|:---:|
|value|숫자 데이터|Y|
|type|표시할 타입 지정(NUMBER, CURRENCY, PERCENT)|N|
|pattern|사용자 정의 패턴 지정|N|
|currencyCode|ISO 4217 화폐 코드, type 속성이 "currency"일 경우에만 적용됨|N|
|currencySymbol|화폐 단위, type 속성이 "currency"일 경우에만 적용됨|N|
|groupingUsed|","로 구분기호 여부|N|
|maxIntegerdigits|화면에 표시할 숫자의 최대 자릿수|N|
|minIntegerDigits|화면에 표시할 숫자의 최소 자릿수|N|
|maxFractionDigits|화면에 표시할 소수점 이하 숫자의 최대 개수|N|
|minFractionDigits|화면에 표시할 소수점 이하 숫자의 최소 개수|N|
|var|변환된 숫자 데이터를 문자열로 할당할 변수 생성|N|
|scope|var 데이터의 스코프|N|


기본 사용법
~~~
<fmt:formatNumber type="number" value="${value}"/>
~~~



* groupingUsed 속성
- 구분기호를 표시할건지에 대한 여부
- default 값은 true

예시 :
~~~
<c:set var ="numtest" value="100200300400500600"/>
<fmt:formatNumber value="${numtest }" /> <br/>
<fmt:formatNumber value="${numtest }" groupingUsed="false" /> <br/>
~~~

결과 :
```
100,200,300,400,500,600
100200300400500600
```


**화폐 기준 출력**
~~~
<fmt:formatNumber value="${value} type="currency/>
~~~

type 속성에 currency 를 넣으면 화폐 기준으로 출력됩니다.<br>
ISO 4217은 [위키백과](https://ko.wikipedia.org/wiki/ISO_4217)를 참조하시길 바랍니다.<br>

예시 : 
~~~
// ISO 4217 currencyCode 속성을 사용한 설정
<fmt:formatNumber value="${value}" type="currency" currencyCode="KRW"/> <br/>
// currencySymbol 속성을 사용한 설정
<fmt:formatNumber value="${value}" type="currency" currencySymbol="$"/> <br/>
~~~
결과 : 
```
￦100,200,300,400,500,600
$100,200,300,400,500,600
````


**percentage**
- type이 percent일 경우 1을 100%로 출력합니다.<br>

예시:
~~~
<c:set var="value" value="1"/>
<fmt:formatNumber value="${value}"/><br/>
<fmt:formatNumber value="${value}" type="percent"/><br/>
~~~

결과 :
```
1
100%
```

**pattern 속성**
- 패턴을 지정하여 숫자 출력<br>
- 0과 #으로 숫자를 자리를 지정하여 표현합니다.<br>
- 0은 자리에 수가 없으면 0으로 표시,#은 자리에 수가 없으면 표시하지않습니다.

예시 :
~~~
<c:set var="value" value="123.4567"/>
<fmt:formatNumber value="${value}"  pattern="0,000.0"/><br />
<fmt:formatNumber value="${value}"  pattern="#,###.#"/><br />
~~~

결과 : 
```
0,123.5
123.5
```


**소수점 자리 옵션**
- minFractionDigits은 최소 소수점 자릿수 표현
- maxFractionDigits 최대 소수점 자릿수 표현(반올림)

예시:
~~~
<fmt:formatNumber value="${value}"  minFractionDigits="5"/><br />
<fmt:formatNumber value="${value}"  maxFractionDigits="2"/><br />
~~~
결과:
```
123.45670
123.46
```
