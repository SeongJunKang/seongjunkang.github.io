---
layout: post
title: "[Querydsl] Querydsl로 Mysql group_concat 사용하기"
date: 2022-09-16
categories: [Java/Spring]
author : "Junny"
tags : [Spring boot, mysql, querydsl, group_concat]
---
## Querydsl을 이용한 group_concat 사용하기

<p>
일반 설정으로 querydsl에서 group_concat을 사용할 수 없다.<br>
group_concat을 사용하기 위해서는 mysql dialect를 customize해야한다.
</p>
<br>

<p>
mysql 버전에 따라 다르지만 필자는 mysql8 버전을 사용하고 있다.<br>
따라서 database-platform을 org.hibernate.spatial.dialect.mysql.MySQL8SpatialDialect 클래스를 사용하고 있다.
이 클래스를 상속해서 다음과 같이 설정을 추가하면된다.
</p>
<br>
```
public class Mysql8CustomDialect extends MySQL8SpatialDialect {
    public Mysql8CustomDialect() {
        super();
        registerFunction("group_concat", new StandardSQLFunction("group_concat", StandardBasicTypes.STRING));
    }
}
```
<br>
그리고 나서 application.yml의 database-platform 설정 부분에 위에서 작성한 클래스의 패키지까지 작성한다.
<br>
```
spring:
  ...
  jpa:
    ...
    database-platform: com.example.querydsl.config.Mysql8CustomDialect
    ...
```
<br>
<p>
이제 설정은 끝났다. 이제 repository로 이동하여 querydsl에서 사용하면된다.<br>

Expressions.stringTemplate을 이용하여 사용하면된다.
</p>
사용예시)
```
queryFactory
        .select(fruit.type, Expressions.stringTemplate("group_concat({0})", fruit.name))
        .from(fruit)
        .groupBy(fruit.type)
        .fetch()
```
<br>
참고 사이트<br>
1) [JPA + Querydsl group_concat 사용법](https://cheese10yun.github.io/jpa-query-dsl-group-concat/)<br>

