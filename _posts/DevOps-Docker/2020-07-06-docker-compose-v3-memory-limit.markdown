---
layout: post
title: "[Docker] Docker-compose 메모리 제한"
date: 2020-07-06
categories: [DevOps/Docker]
author : "Junny"
tags : [docker,docker_compose,memory_limit]
---
# Docker-compose 메모리 제한

Docker-compose를 사용하여 몇몇 프로그램을 사용하고있었는데, mssql이랑 jenkins가 메모리를 너무 잡아먹는 현상이 발생했다.
compose에서 메모리를 제한하는 deploy 설정이 있었는데, 2버전에서는 제공되지만 3버전에서는 다음과 같은 경고가 발생한다.
이는 도커 스웜을 사용하여 작동하라는 내용이다.
```
WARNING: Some services (sevicename) use the ‘deploy’ key, which will be ignored. Compose does not support ‘deploy’ configuration - use docker stack deploy to deploy to a swarm.
```

다음의 명령어로 해당 내용을 수행할 수 있다. 이 명령어는 리소스 제한을 설정하는 API v3 방식을 다시 v2 호환 속성으로 변환하려고 시도한다.
완벽한 솔루션은 아니지만 해당 메모리 제한을 두는데 사용할 수 있다.
```
docker-compose --compatibility up
```

[원본 사이트](https://nickjanetakis.com/blog/docker-tip-78-using-compatibility-mode-to-set-memory-and-cpu-limits)

