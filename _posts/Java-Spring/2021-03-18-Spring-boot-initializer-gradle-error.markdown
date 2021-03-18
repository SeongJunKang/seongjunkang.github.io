---
layout: post
title: "[Spring] Spring boot Initializer Error"
date: 2021-03-18
categories: [Java/Spring]
author : "Junny"
tags : [Spring boot, intellij, Spring boot Initialzer error]
---
# [Spring] Spring boot Initializer Error


Spring boot에서 새 프로젝트를 Spring Initializer를 통해 생성했다.<br>
<br>
프로젝트가 만들어지고 빌드하는 과정에서 gradle에서 오류가 발생했다.<br>

![spring boot error](/assets/image/java/spring/spring_error_01.png)

Unable to load class 'org.gradle.api.internal.plugins.DefaultConvention'.<br>
<br>

이는 Intellij 버전과 gradle 버전이 맞지 않아서 발생하는 오류이다<br>
<br>

```
# 2021 03 18 현재
gralde 6.8.3
intellij 2018.2.8
```
<br>
2018 버전은 gradle 5버전까지 사용 가능하다<br>

다음 명령어로 wrapper의 설정을 변경하면 build가 정상적으로 이루어진다

```
gradlew wrapper --gradle-version 5.6.4
```

5.6.4는 5버전의 최신버전임

