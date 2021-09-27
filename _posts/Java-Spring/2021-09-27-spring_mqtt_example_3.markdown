---
layout: post
title: "[Spring] Spring Boot MQTT Mosquitto example(3)"
date: 2021-09-27
categories: [Java/Spring]
author : "Junny"
tags : [Spring boot, mqtt, mqtt example]
---
## [Posts series]

[1.Mqtt Introduce](https://seongjunkang.github.io/java/spring/2021/09/15/spring_mqtt_example.html) <br>
[2.Mqtt publish with Spring boot](https://seongjunkang.github.io/java/spring/2021/09/16/spring_mqtt_example_2.html)<br>
[3.Mqtt subscribe with Spring boot](https://seongjunkang.github.io/java/spring/2021/09/27/spring_mqtt_example_3.html) - 현재<br>

<br>
<br>
저번 시간에 발행했던 포스팅에서 Spring boot를 이용한 MQTT publish를 진행했습니다.

이번 시간에는 발행한 MQTT 메세지를 subscribe하는 간단한 웹서버를 만들어 볼 예정입니다.
<br>

### 환경 설정 버전 정보 
```
mosquitto version: eclipse-mosquitto:1.6.15-openssl

Spring boot version: 2.5.4

Java version: openjdk 16.0.2

Gradle version: gradle-7.1.1
```
<br>
<br>
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
<br>
저번 포스팅에서 발행을 했고 이번 포스팅에는 구독만 하려고 합니다.
하나의 웹서버에서 발행 & 구독 둘 다 할 수 있습니다.

<br>
## Subscribe(구독)

- 구독은 발행보다 훨씬 간단합니다. 특정한 토픽을 감시하는 채널을 만들고, 그 채널에 메세지가 발행되었을 때, 바로 읽어오면 됩니다.

MqttSubscribeConfigutarion.java
<script src="https://gist.github.com/SeongJunKang/9530fbb2ae5b95664b109c48f624abad.js"></script>
<br>
<br>
이 설정만 해주면 메세지가 발행될 때 설정해준 메세지 핸들러에서 topic과 paylod를 받아올 수 있습니다.
<br>
<br>
