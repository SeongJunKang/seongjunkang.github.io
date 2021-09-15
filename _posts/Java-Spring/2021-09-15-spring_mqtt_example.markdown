---
layout: post
title: "[Spring] Spring Boot MQTT Mosquitto example(1)"
date: 2021-09-15
categories: [Java/Spring]
author : "Junny"
tags : [Spring boot, mqtt, mqtt example]
---
# [Spring] Spring Boot MQTT Mosquitto example(1)

## MQTT Broker 소개
MQTT(Message Queuing Telemetry Transport)란 발행-구독 기반의 메세징 프로토콜 중 하나입니다.

MQTT는 TCP/IP 프로토콜 위에서 동작하며, **Pulbish(발행)** - **Broker(브로커)** - **Subscribe(구독)** 의 구조 형태를 띄고 있습니다.

![MQTT structure img](/assets/image/java/spring/2021-09-15_mqtt_structure.png)

메세지를 브로커(Broker)에게 발행(Publish)하면 토픽(Topic)에 해당하는 모든 구독자(Subscribe)에게 메세지가 전달됩니다.

여기서 **토픽(Topic)** 은 특정 채널을 의미하며, 계층구조를 갖습니다. 계층별 구분은 슬래시(/)로 합니다.

![MQTT topic img](/assets/image/java/spring/2021-09-15_mqtt_topic.png)

**QoS(Quality of Service)**
- MQTT는 시스템에 참여하는 장치들의 처리 능력, 네트워크 대역폭, 메시지 오버헤드 등 주변상황에 맞게 시스템이 동작할 수 있도록 3단계 QoS(Quality of Service) 를 제공합니다.
  - 0 (최대한번): 메시지는 최대 한 번 전달되거나 전혀 전달되지 않습니다. 이 네트워크 간 전달은 수신확인되지 않습니다.
 메시지는 저장되지 않습니다. 클라이언트 연결이 끊어지거나 서버가 실패하는 경우 메시지는 손실될 수 있습니다.
 QoS=0은 가장 빠른 전송 모드입니다. 이 모드는 "실행 후 삭제"라고도 합니다.

  - 1 (최소한번): 메시지는 항상 최소 한 번 전달됩니다. 송신자가 수신확인을 수신하지 않는 경우, 메시지는 수신확인이 수신될 때까지 DUP 플래그가 설정되어 다시 송신됩니다. 따라서 수신자에게 동일한 메시지가 여러 번 전송되고 이를 여러 번 처리할 수도 있습니다.
  메시지가 처리될 때까지 송신자와 수신자는 메시지를 로컬에 저장해야 합니다.

  - 2 (정확히 한 번): 메시지는 항상 정확히 한 번만 전송됩니다.
  메시지가 처리될 때까지 송신자와 수신자는 메시지를 로컬에 저장해야 합니다.
  QoS=2는 가장 안전하지만 가장 느린 전송 모드입니다. 메시지가 송신자에서 삭제되기 전에 송신자와 수신자 사이에 최소 두 쌍의 전송이 발생합니다. 메시지는 첫 번째 전송 후에 수신자 측에서 처리될 수 있습니다. 
  
## MQTT Broker 설치
MQTT는 서버-클라이언트 구조가 아니기 때문에, 브로커를 설치해야합니다.

브로커의 종류로 다양한 프로그램들이 개발되어 있습니다. (ActiveMQ, Apollo, IBM Message Sight, Mosquitto, RabbitMQ 등)

- 자세한 내용은 [MQTT 공식 Github](https://github.com/mqtt/mqtt.org/wiki/server-support) 에 비교 자료가 있습니다. 

저는 도커를 이용해서 Mosquitto 브로커를 띄웠습니다. Mosquitto는 최소한의 전력과 패킷량으로 통신하는 프로토콜입니다. 주로 M2M, IoT분야에서 사용됩니다.

![MQTT docker img](/assets/image/java/spring/2021-09-15_mqtt_docker_compose_img.png)

## MQTT Explorer 설치

메세지가 들어오는지 확인할 수 있도록 [MQTT Explorer](http://mqtt-explorer.com)을 설치했습니다.

MQTT Explorer는 반드시 필요한건 아닙니다.

이로써 Mosquitto 브로커 설치 완료되었습니다. 
Spring Boot를 이용한 publish, subscribe 설정 및 결과 확인은 다음편에서 계속하겠습니다.