---
layout: post
title:  "[Mybatis] DB HashMap으로 가져올때 순서 유지하는 방법"
date:   2020-09-28
categories: [Java/Spring]
author : "Junny"
tags : [Mybatis, HashMap, LinkedHashMap]
---
# [Mybatis] DB HashMap으로 가져올때 순서 유지하는 방법

Mybatis를 이용해서 HashMap으로 데이터를 가져오면 순서가 뒤바뀔 수있다.

HashMap은 순서를 유지하지 않고, key-value 값으로만 가져오기 때문이다.

다음과 같은 쿼리가 있다고 가정해보자

```
 	<select id="selectBookCountByYear" resultType="hashMap">
	SELECT 
	(SELECT COUNT(*) FROM book WHERE YEAR(regdate) = '2016') AS '2016',
	(SELECT COUNT(*) FROM book WHERE YEAR(regdate) = '2017') AS '2017',
	(SELECT COUNT(*) FROM book WHERE YEAR(regdate) = '2018') AS '2018',
	(SELECT COUNT(*) FROM book WHERE YEAR(regdate) = '2019') AS '2019',
	(SELECT COUNT(*) FROM book WHERE YEAR(regdate) = '2020') AS '2020'
 	</select>
```

해당 데이터를 호출하고 entryset으로 for문을 돌리면 

```
Map<String,Object> dataList = bookService.selectBookCountByYear();
ArrayList<Map<String,Object>> resultList = new ArrayList<>();
for (Entry<String, Object> entry : dataList.entrySet()) {
  int value = Integer.parseInt(entry.getValue().toString());
  Map<String,Object> hashMap = new HashMap<>();
  hashMap.put("name", entry.getKey());
  hashMap.put("value", entry.getValue());
  resultList.add(hashMap);
}

resultList.stream().forEach( a -> System.out.println(a.get("name")+", "+a.get("value"));
```

다음과 같은 순서를 알 수 없는 결과가 나타난다(매번 바뀜)

| name | value|
|---|:---:|
| 2017 | 2890 |
| 2016 | 1132 |
| 2019 | 3306 |
| 2018 | 1207 |
| 2020 | 4598 |


column 순서를 유지하면서 가져오는 방법은 mybatis 쿼리문에서 resultType을 변경하면된다

기존 hashMap -> java.util.LinkedHashMap

그냥 linkedHashMap을 사용하면 classNotFound Exception이 발생한다.

```
 	<select id="selectBookCountByYear" resultType="java.util.LinkedHashMap">
	SELECT 
	(SELECT COUNT(*) FROM book WHERE YEAR(regdate) = '2016') AS '2016',
	(SELECT COUNT(*) FROM book WHERE YEAR(regdate) = '2017') AS '2017',
	(SELECT COUNT(*) FROM book WHERE YEAR(regdate) = '2018') AS '2018',
	(SELECT COUNT(*) FROM book WHERE YEAR(regdate) = '2019') AS '2019',
	(SELECT COUNT(*) FROM book WHERE YEAR(regdate) = '2020') AS '2020'
 	</select>
```
순서대로 잘 작동한다.

| name | value|
|---|:---:|
| 2016 | 1132 |
| 2017 | 2890 |
| 2018 | 1207 |
| 2019 | 3306 |
| 2020 | 4598 |
