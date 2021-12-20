---
layout: post
title: "[Github action] Github Action fail when docker command use with self host"
date: 2021-12-20
categories: [DevOps/Git]
author : "Junny"
tags : [Git, Github, Github_action, Github_action_self_host, Github_action_docker]
---
- 혹시나 나중을 위해서 기록해두는 것이 좋을듯 하여 기록한다.<br>
logj 이슈 때문에 버전업을 하려고 gradle 설정을 변경해서 Git에 푸쉬했다. <br>
근데 갑자기 작동하던 액션이 갑자기 에러를 뱉는다. Gradle내용만 바꿨을 뿐인데...<br>
에러 내용은 다음과 같다 <br>
<br>

![permission_deny](/assets/image/github/github_action_docker_fail.png)
<br>
<br>

## 에러 내용
- 도커를 사용하는데, 도커를 사용할 권한이 없다고 나온다. 이전에는 잘 작동하고 있었다. 갑자기 왜 ? <br>
권한이 없나 docker 그룹을 확인하기 위해 cat /etc/group을 해봤더니 docker 그룹에 적용이 되어있었다.<br>
역시 구글신께 도움을 요청해봤다<br>
<br>

## 해결
- self host를 사용하고 있었는데 같은 내용으로 issue에 올라온 내용이 있었다. (https://github.com/actions/runner/issues/411)[https://github.com/actions/runner/issues/411]
- ~/action-runner 디렉토리에 있는 .svc 파일을 재시작
<br>
<br>
```
sudo ./svc.sh stop
sudo ./svc.sh start
```
<br>

재시작 후에 정상 작동 하는것을 확인할 수 있었다.

![permission_deny](/assets/image/github/github_action_docker_success.png)


<br><br><br><br>

