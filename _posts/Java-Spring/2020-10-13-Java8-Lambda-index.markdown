---
layout: post
title: "[Java] Java 8 Lambda에서 index 번호 사용방법"
date: 2020-10-13
categories: [Java/Spring]
author : "Junny"
tags : [Java8, Lambda, lambda_index]
---
# [Java] Java 8 Lambda에서 index 번호 사용방법


Java 8 Lambda(람다)식으로 할 때와 기존의 for loop를 이용하는 방법을 비교해보자<br>
<br>
다음과 같은 List가 있을 때,
<br>
```
List<String> list = new ArrayList<>();
list.add("Hello");
list.add("World");
```

<br>
1. 기존의 for loop 방법<br>
```
StringBuilder builder = new StringBuilder();
for(int i = 0 ; i < list.size(); i++) {
	builder.append(list[i]);
	if (i != list.size() -1) {
		builder.append(" ");
	}
}
System.out.println(builder.toString());
```
<br>
<br>
2. 람다식의 방법
<br>
```
IntStream.range(0, list.size())
	.forEach(idx -> {
		builder.append(list[idx]);
		if (idx != list.size() -1 ) {
			builder.append(" ");
		}
	}
});
System.out.println(builder.toString());
```
