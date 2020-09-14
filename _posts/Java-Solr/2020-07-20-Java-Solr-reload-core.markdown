---
layout: post
title:  "[Solr] How to Solr core reload"
date:   2020-07-20
categories: [Java/Solr]
author : "Junny"
tags : [Solr_core_reload]
---
# [Solr] How to Solr core reload

Solr에서 manage-schema나 다른 설정파일을 수정했을경우, 이 방법을 모르면 solr를 재시작해야한다.

solr에서 재시작을 하지않고 core를 다시 로딩하는 방법을 찾다가 발견했다.


다음과 같은 형식의 rest api를 이용하여 사용하면된다.
```
http://localhost:8983/solr/admin/cores?action=RELOAD&core=[CORE_NAME]﻿
```



[Solr Guide Api](https://lucene.apache.org/solr/guide/7_1/coreadmin-api.html#coreadmin-reload)에 내용이 나와있다.<br>
아래는 stackoverflow의 질문 내용
[stackoverflow :: how to reload Solr core without restart](https://stackoverflow.com/questions/11555696/is-there-a-way-to-dynamically-update-a-synonym-file-without-restarting-solr-serv)