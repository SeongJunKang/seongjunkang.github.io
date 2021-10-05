---
layout: post
title: "[Docker] Docker-compose invalid port specification error"
date: 2021-10-05
categories: [DevOps/Docker]
author : "Junny"
tags : [docker,docker-compose,invalid-port-specification]
---
# Docker-compose invalid port specification error


docker-compose를 사용해서 ubuntu를 실행시켰는데 잘실행되고 있었다.


그런데 어느날 갑자기 다음과 같은 에러가 발생했다.


```
ERROR: for ubuntu Cannot create container for service ubuntu : invalid port specification: "678682"
ERROR: Encountered errors while bringing up the project.
```


docker-compose.yml을 살펴보면

```
version: "3"
services:
    ubuntu:
        container_name: ubuntu
        image: ubuntu:20.04
        tty: true
        ports:
            - 11311:22
```

이렇게 되어있는데 에러가 발생했다.


일단 에러 메세지를 살펴보면 "678682"라는 숫자의 포트가 어떻게 나왔나 살펴보니 YAML 1.1 버전부터는 시간계산에 유용한 "base60"을 사용하여 계산한다고 한다.

60 미만의 숫자는 hh : mm : ss 총 시간 (초)으로 자동 변환되어 버린다.

```
# 678682가 나오게 된 배경
# 역변환 
(678682 - 22(60^0)) / (60^1) = 11311
# 원래 계산식
11311 * (60^1) + 22 *(60^0) = 678682
```

즉, 11311 포트를 개방할 수 없어서 발생한다는 에러라고 볼 수 있다.


docker/compose github에 같은 오류의 [issue](https://github.com/docker/compose/issues/3109)를 확인할 수 있었다.


여기에서 우리는 base60으로 할게 아니라 포트 그대로 보여주어야 하기 때문에 더블쿼트로 감싸줘야한다.


```
version: "3"
services:
    ubuntu:
        container_name: ubuntu
        image: ubuntu:20.04
        tty: true
        ports:
            - "11311:22"
```


이렇게 실행하니 원활히 실행됐다.

[docker-compose 공식 문서](https://docs.docker.com/compose/)에서 보니 ports를 더블쿼트로 감싸고 있었다.

공식문서를 잘 확인해야겠다.



