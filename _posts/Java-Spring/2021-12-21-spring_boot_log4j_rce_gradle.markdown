---
layout: post
title: "[Spring] Spring Boot log4j rce issue for gradle"
date: 2021-12-21
categories: [Java/Spring]
author : "Junny"
tags : [Spring boot, log4j, log4j2, log4j_rce]
---
## Log4j rec issue for gradle

이번에 log4j에서 발행한 취약점은 1~10단계중 가장 위험한 단계인 10단계에 속한다.<br>
명령어 한줄이면 그 서버에 원격으로 프로그램을 실행시킬 수 있기 때문에 조속히 대응이 필요하다.<br>


<br><br>

Gradle을 사용하고 있는 사람들은 다음의 명령어만 추가해주면 된다.

```
// log4j2 rce issue (2021-12-10)
dependencyManagement {
    imports {
        mavenBom 'org.apache.logging.log4j:log4j-bom:2.17.0'
    }
}
```

이렇게 설정후 Gralde 싱크를 맞추면 log4j의 버전이 올라가는 것을 확인할 수 있다


Maven (pom.xml)을 사용하면 다음을 추가하면 된다.
```
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.apache.logging.log4j</groupId>
            <artifactId>log4j-bom</artifactId>
            <version>2.17.0</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

빌드를 다시하면 log4j의 버전이 바뀐것을 확인할 수 있다.

자세한 내용은 (스프링 공식 사이트)[https://spring.io/blog/2021/12/10/log4j2-vulnerability-and-spring-boot]에서 확인할 수 있다.
