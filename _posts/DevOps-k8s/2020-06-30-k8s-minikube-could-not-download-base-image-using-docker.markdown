---
layout: post
title: "[Kubernates] 쿠버네티스에서 docker를 사용해서 minikube 실행이 안될때"
date: 2020-06-30
categories: [DevOps/Kubernates]
author : "Junny"
tags : [Kubernates,minikube_not_loading]
---
# 쿠버네티스에서 docker를 사용해서 minikube 실행이 안될때
- docker가 설치되어있었고, k8s를 사용해보려고 minikube를 설치했는데, minikube start를 했는데 오류가 발생했다. 오류 내용은 <br>
```
Unfortunately, could not download the base image gcr.io/k8s-minikube/kicbase:v0.0.10
```
해당 내용의 이미지는 docker images에 다운로드 되어있었다.<br>

이 내용의 경우 아래의 명령어로  minikube를 시작할 수 있다.

```
minikube start --driver=docker --base-image-gcr.io/k8s-minikube/kicbase:v0.0.10
```

이 명령어로 실행하면 minikube가 작동하는 것을 확인할 수 있다.<br>

- 기존 설치된 docker images와 minikube의 docker images가 다른것을 확인할 수 있다.<br>
minikube의 docker images는 'minikube ssh'를 통해 접속하여 확인하면 된다.<br>

이 때, minikube와 host docker의 경로를 일치 시켜주는 명령어가 있다.<br>

host의 docker 경로를 minikube docker 환경로 변환시키는 명령어<br>
```
eval $(minikube docker-env)
```

다시 원상태로 돌리는 명령어는 다음과 같다.
```
eval $(minikube docker-env -u)
```