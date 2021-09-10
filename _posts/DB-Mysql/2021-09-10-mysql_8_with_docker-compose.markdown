---
layout: post
title: "[Mysql] Docker compose를 이용한 local mysql8 설치"
date: 2021-09-10
categories: [DataBase/Mysql]
author : "Junny"
tags : [mysql, docker, docker-compose, mysql8]
---
# [Mysql] Docker compose를 이용한 local mysql8 설치

선행으로 Windows OS의 경우 WSL2를 기본으로 도커가 사용하고 있습니다.

WSL2를 사용하지 않으면, 도커 데스크탑에서 `Use the WSL 2 based Engine`을 체크 해제해야합니다.

WSL2로 접속하여 docker가 작동하는지 확인해야합니다.

현재 도커 버전
```
$ docker version
Client: Docker Engine - Community
 Cloud integration: 1.0.17
 Version:           20.10.8
 API version:       1.41
 Go version:        go1.16.6
 Git commit:        3967b7d
 Built:             Fri Jul 30 19:54:02 2021
 OS/Arch:           linux/amd64
 Context:           default
 Experimental:      true

Server: Docker Engine - Community
 Engine:
  Version:          20.10.8
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.16.6
  Git commit:       75249d8
  Built:            Fri Jul 30 19:52:10 2021
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.4.9
  GitCommit:        e25210fe30a0a703442421b0f60afac609f950a3
 runc:
  Version:          1.0.1
  GitCommit:        v1.0.1-0-g4144b63
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
```

docker가 설치되어 있다면, 도커 컴포즈도 설치가 되어있는지 확인합니다.

```
$ docker-compose version
Docker Compose version v2.0.0-rc.2
```

자 이제 도커 컴포즈에서 mysql에 해당하는 옵션을 주어 서비스를 지정해야합니다.

```
vi docker-compose.yml

version: "3"
services:
    mysql:
        container_name: mysql8
        image: mysql:8.0.26
        environment:
            MYSQL_DATABASE: test
            MYSQL_ROOT_PASSWORD: test01
            MYSQL_ROOT_HOST: '%'
        ports:
            - 3306:3306
```

도커 컴포즈 설정이 완료 되었으면 다음의 명령어로 mysql container를 실행할 수 있습니다.

```
docker-compose up -d
```

-d 옵션으로 데몬으로 백그라운드 실행할 수 있습니다.

옵션에 대한 자세한 사항은 [공식 홈페이지](https://docs.docker.com/compose/reference/) 에서 확인할 수 있습니다. 