---
layout: post
title: "[Docker] Docker-compose 지정 위치에 있는 compose 파일실행"
date: 2021-01-29
categories: [DevOps/Docker]
author : "Junny"
tags : [docker,docker_compose,dokcer-compose_different_file]
---
# Docker-compose 지정 위치에 있는 compose 파일실행


docker-compose를 여러개로 만들어 그룹적으로 관리할 수 있다.<br>
<br>
jenkins에서 pipeline을 통해 빌드한 파일을 script를 통해 docker-compose를 지정한 위치의 파일을 사용하려고할 때 사용했다.<br>


다음의 명령어를 사용하면 된다
```
docker-compose -f ${특정경로}/docker-compose.yml up -d
ex)
docker-compose -f /usr/local/service/docker-compose.yml up -d
```

현재 위치에 있는 docker-compose.yml을 사용할 경우 -f 옵션를 생략할 수 있다.


-f 는 특정 파일을 사용 설정이다<br>
-d 는 백그라운드 실행 설정이다<br>
up / down 은 compose 를 실행/종료할 때 사용하는 명령어다.<br>



이외의 명령어는 "docker-compose --help" 를 사용하면 확인할 수 있다.

```
Usage:
  docker-compose [-f <arg>...] [--profile <name>...] [options] [--] [COMMAND] [ARGS...]
  docker-compose -h|--help

Options:
  -f, --file FILE             Specify an alternate compose file
                              (default: docker-compose.yml)
  -p, --project-name NAME     Specify an alternate project name
                              (default: directory name)
  --profile NAME              Specify a profile to enable
  -c, --context NAME          Specify a context name
  --verbose                   Show more output
  --log-level LEVEL           Set log level (DEBUG, INFO, WARNING, ERROR, CRITICAL)
  --ansi (never|always|auto)  Control when to print ANSI control characters
  --no-ansi                   Do not print ANSI control characters (DEPRECATED)
  -v, --version               Print version and exit
  -H, --host HOST             Daemon socket to connect to

  --tls                       Use TLS; implied by --tlsverify
  --tlscacert CA_PATH         Trust certs signed only by this CA
  --tlscert CLIENT_CERT_PATH  Path to TLS certificate file
  --tlskey TLS_KEY_PATH       Path to TLS key file
  --tlsverify                 Use TLS and verify the remote
  --skip-hostname-check       Don't check the daemon's hostname against the
                              name specified in the client certificate
  --project-directory PATH    Specify an alternate working directory
                              (default: the path of the Compose file)
  --compatibility             If set, Compose will attempt to convert keys
                              in v3 files to their non-Swarm equivalent (DEPRECATED)
  --env-file PATH             Specify an alternate environment file

Commands:
  build              Build or rebuild services
  config             Validate and view the Compose file
  create             Create services
  down               Stop and remove resources
  events             Receive real time events from containers
  exec               Execute a command in a running container
  help               Get help on a command
  images             List images
  kill               Kill containers
  logs               View output from containers
  pause              Pause services
  port               Print the public port for a port binding
  ps                 List containers
  pull               Pull service images
  push               Push service images
  restart            Restart services
  rm                 Remove stopped containers
  run                Run a one-off command
  scale              Set number of containers for a service
  start              Start services
  stop               Stop services
  top                Display the running processes
  unpause            Unpause services
  up                 Create and start containers
  version            Show version information and quit
  
```