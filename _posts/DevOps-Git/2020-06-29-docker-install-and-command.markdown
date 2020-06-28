---
layout: post
title: "[Docker] docker 설치 및 명령어 모음 "
date: 2020-06-29
categories: [DevOps/Git]
author : "Junny"
tags : [docker,docker_install,docker_command]
---
# Docker 설치 및 명령어

## 1. 도커 설치하기

Docker는 리눅스 배포판 종류를 자동으로 인식해서 패키지를 설치해주는 스크립트를 제공합니다.
```
$ sudo wget -qO- https://get.docker.com/ | sh
```
저는 MacOS용 설치 [도커 설치 for MacOS](https://hub.docker.com/editions/community/docker-ce-desktop-mac/)로 설치했습니다.

## 2. 도커 버전확인

```
docker --version
```
결과 값

![docker --version img](./img/docker_version.png)<br>

아래는 docker로 진행된 내용입니다.

## 3. 실행된 도커 컨테이너로 접속하기

```
docker exec -it [container명] /bin/bash 혹은 "bash"
```

## 4. docker run에 사용되는 명령어 모음
-c, --cpu-shares=0: CPU 자원 분배 설정입니다. 설정의 기본 값은 1024이며 각 값은 상대적으로 적용됩니다. <br>
-d, --detach=false: Detached 모드입니다. 보통 데몬 모드라고 부르며 컨테이너가 백그라운드로 실행됩니다.  <br>
-e, --env=[]: 컨테이너에 환경 변수를 설정합니다. 보통 설정 값이나 비밀번호를 전달할 때 사용합니다. <br>
--entrypoint="": Dockerfile의 ENTRYPOINT 설정을 무시하고 강제로 다른 값을 설정합니다. <br>
--expose=[]: 컨테이너의 포트를 호스트와 연결만 하고 외부에는 노출하지 않습니다. <br>
-i, --interactive=false: 표준 입력(stdin)을 활성화하며 컨테이너와 연결(attach)되어 있지 않더라도 표준 입력을 유지합니다. 보통 이 옵션을 사용하여 Bash에 명령을 입력합니다. <br>
--link=[]: 컨테이너끼리 연결합니다. &lt;컨테이너 이름&gt;:&lt;별칭&gt; 형식입니다. <br>
-m, --memory="": 메모리 한계를 설정합니다. &lt;숫자&gt;&lt;단위&gt; 형식이며 단위는 b, k, m, g를 사용할 수 있습니다.<br>
--rm=false: 컨테이너 안의 프로세스가 종료되면 컨테이너를 자동으로 삭제합니다. -d 옵션과 함께 사용할 수 없습니다.<br>
-t, --tty=false: TTY 모드(pseudo-TTY)를 사용합니다. Bash를 사용하려면 이 옵션을 설정해야 합니다. 이 옵션을 설정하지 않으면 명령을 입력할 수는 있지만 셸이 표시되지 않습니다. <br>
-u, --user="": 컨테이너가 실행될 리눅스 사용자 계정 이름 또는 UID를 설정합니다. <br>
-v, --volume=[]: 데이터 볼륨을 설정입니다. 호스트와 공유할 디렉터리를 설정하여 파일을 컨테이너에 저장하지 않고 호스트에 바로 저장합니다.<br>
-w, --workdir="": 컨테이너 안의 프로세스가 실행될 디렉터리를 설정합니다.<br>
--name="": 컨테이너에 이름을 설정합니다.<br>
--net="bridge": 컨테이너의 네트워크 모드를 설정합니다.<br>
&nbsp;◎ bridge: Docker 네트워크 브리지에 새 네트워크를 생성합니다.<br>
&nbsp;◎ none: 네트워크를 사용하지 않습니다.<br>
&nbsp;◎ container:<컨테이너 이름, ID>: 다른 컨테이너의 네트워크를 함께 사용합니다.<br>
&nbsp;◎ host: 컨테이너 안에서 호스트의 네트워크를 그대로 사용합니다. 호스트 네트워크를 사용하면 D-Bus를 통하여 호스트의 모든 시스템 서비스에 접근할 수 있으므로 보안에 취약해집니다.<br>

## 5. 도커 컨테이너 메모리 사용량 확인
docker stats --format "table {{.Name}}\t{{.Container}}\t{{.CPUPerc}}\t{{.MemUsage}}"

###### [출처: 가장 빨리 만나는 Docker 20장 - 28. run](http://pyrasis.com/book/DockerForTheReallyImpatient/Chapter20/28)

## docker로 진행한 내용
### [tomcat을 이용한 war 배포하기](https://github.com/SeongJunKang/doicker_practice/tree/master/tomcat)
### [spring boot 배포하기](https://github.com/SeongJunKang/doicker_practice/tree/master/spring_boot)
### [docker compose를 사용하여 spring boot 예시](https://github.com/SeongJunKang/doicker_practice/tree/master/docker-compose)
### [docker로 jenkins 설치하기](https://github.com/SeongJunKang/doicker_practice/tree/master/jenkins)
### [Solr 설치 및 spring boot 연동](https://github.com/SeongJunKang/doicker_practice/tree/master/solr)
<br>