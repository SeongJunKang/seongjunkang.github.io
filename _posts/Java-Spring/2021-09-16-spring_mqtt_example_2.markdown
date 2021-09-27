---
layout: post
title: "[Spring] Spring Boot MQTT Mosquitto example(2)"
date: 2021-09-16
categories: [Java/Spring]
author : "Junny"
tags : [Spring boot, mqtt, mqtt example]
---
## [Posts series]

[1.Mqtt Introduce](https://seongjunkang.github.io/java/spring/2021/09/15/spring_mqtt_example.html)<br>
[2.Mqtt publish with Spring boot](https://seongjunkang.github.io/java/spring/2021/09/16/spring_mqtt_example_2.html) - 현재<br>
[3.Mqtt subscribe with Spring boot](https://seongjunkang.github.io/java/spring/2021/09/27/spring_mqtt_example_3.html)<br>

<br>


[ [지난번 포스팅](https://seongjunkang.github.io/java/spring/2021/09/15/spring_mqtt_example.html) ]에서
MQTT에 대한 기본적인 동작과 설치에 대해서 다뤘습니다.

이번 포스팅은 Spring boot를 이용한 MQTT연동 방식에 대해 알아보려고합니다.

환경 설정 버전 정보 
```
mosquitto version: eclipse-mosquitto:1.6.15-openssl

Spring boot version: 2.5.4

Java version: openjdk 16.0.2

Gradle version: gradle-7.1.1
```

MQTT를 이용한 메세징 전달을 위해 다음의 라이브러리를 빌드툴에 추가합니다.
```
# Gradle
implementation 'org.springframework.integration:spring-integration-mqtt'
implementation 'org.springframework.integration:spring-integration-stream'
```
```
# Maven
<dependency>
    <groupId>org.springframework.integration</groupId>
    <artifactId>spring-integration-mqtt</artifactId>
    <version>5.5.3</version>
</dependency>
<dependency>
    <groupId>org.springframework.integration</groupId>
    <artifactId>spring-integration-stream</artifactId>
    <version>5.5.3</version>
</dependency>
```

발행과 구독을 구분하기 위해서 두 개의 웹서버에서 발행 & 구독을 구현하려고 합니다.
발행과 구독을 하나의 웹서버에 작성해도 됩니다.

## Publish(발행)
**Mqtt에 대한 설정 파일**

MqttConfigutarion.java
<script src="https://gist.github.com/SeongJunKang/c333e64bda6e2bcc492908d0f363dd90.js"></script>


**Mqtt에 데이터를 발행할 게이트웨이 설정**
MqttGateway.java
<script src="https://gist.github.com/SeongJunKang/9ffffe185c5cc9731ff476686b44e369.js"></script>

configuration과 gateway설정이 끝났다면 발행을 테스트 코드를 통해 발행을 테스트할 수 있습니다.

MqttPublishTest.java
<script src="https://gist.github.com/SeongJunKang/5f0aafb736be6a90624cf89a0d06142b.js"></script>

MQTT Explorer를 통해 메세지가 정상적으로 발행됐는지 확인할 수 있습니다.

![MQTT Explorer_check_msg](/assets/image/java/spring/2021-09-16_mqtt_explorer_publish_check.png)

이번 포스팅에서는 Spring boot에 MQTT 메세지 발행(publish)에 대해서 작성해보았습니다.

다음 포스팅에는 구독(Subscribe)에 대한 설정 및 데이터에 대한 확인할 하도록 하겠습니다.
