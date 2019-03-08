---
layout: post
title:  "[Jstl] JSP에서 jstl Core Lib 함수"
date:   2019-03-07
categories: jsp
author : "Junny"
permalink: /:categories/:title
---
# [Jstl] Jsp에서 jstl Core Lib 함수

Jsp에서 Tag Lib를 등록해야된다.
core가 가장 기본적인 TagLib이므로 여기에서는 core에 대한 내용을 다루겠다.
dependency는 다음과 같다.
~~~
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>servlet-api</artifactId>
			<version>2.5</version>
			<scope>provided</scope>
		</dependency>
		<dependency>
			<groupId>javax.servlet.jsp</groupId>
			<artifactId>jsp-api</artifactId>
			<version>2.1</version>
			<scope>provided</scope>
		</dependency>
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>jstl</artifactId>
			<version>1.2</version>
		</dependency>
~~~

JSP 상단에 아래의 태그를 선언해준다. prefix는 해당 태그를 사용할 때의 별명이다.
~~~
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
~~~
core 태그에서 사용할 수 있는 함수

<table>
	<tr>
		<td>태그명</td>
		<td>설명</td>
	</tr>
    	<tr>
        	<td> &lt; c:set /></td>
        	<td> 변수 선언 및 값 수정</td>
    	</tr>
    	<tr>
        	<td>&lt;c:remove /> </td>
        	<td> 변수 제거</td>
    	</tr>
    	<tr>
        	<td> &lt;c:out /> </td>
        	<td> 변수의 출력 ( 속성값 사용 가능 )</td>
    	</tr>
    	<tr>
        	<td>  &lt;c:if />  </td>
        	<td> 조건문</td>
    	</tr>
    	<tr>
        	<td> 
        				&lt;c:choose/>  
		</td>
        	<td rowspan="3"> Switch문</td>
    	</tr>
    	<tr>
        	<td> 
			&lt;c:when />
		</td>
    	</tr>
    	<tr>
        	<td> 
			&lt;c:otherwise />  
		</td>
    	</tr>
    	<tr>
        	<td> 
			&lt;c:forEach />
			</td>
				<td> 
			반복문
			</td>
    	</tr>
    	<tr>
        	<td> 
			&lt;c:forTokens /> 
			</td>
				<td> 
				구분자로 분리 후 반복문 
			</td>
    	</tr>
    	    	<tr>
        	<td> 
			&lt;c:url />
			</td>
				<td> 
				URL을 생성
			</td>
    	</tr>
    	<tr>
        	<td> 
			&lt;c:param /> 
			</td>
				<td> 
				&lt;c:url>에서 사용될 파라미터 추가 
			</td>
    	</tr>    	
    	<tr>
        	<td> 
			&lt;c:import /> 
			</td>
				<td> 
				현재 페이지에 페이지 추가
			</td>
    	</tr>
    	<tr>
        	<td> 
			&lt;c:redirect />
			</td>
				<td> 
				현재 페이지를 해당 URL로 이동
			</td>
    	</tr>
    	<tr>
        	<td> &lt;c:catch /> </td>
        	<td> 예외처리</td>
    	</tr>
</table>
