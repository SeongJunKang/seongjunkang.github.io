---
layout: post
title:  "[Pyhton] UnicodeDecodeError 'cp949'"
date:   2020-07-06
categories: [Python]
author : "Junny"
tags : [Python,UnicodeDecodeError,cp949]
---
# [Python] UnicodeDecodeError 'cp949'

Python에서 파일을 열때 다음과 같은 에러가 발생했다.
```
Traceback (most recent call last):
  File "E:/PyCharm/PycharmProjects/project/main.py", line 11, in <module>
    json_data = json.load(json_file)
  File "C:\Python36\lib\json\__init__.py", line 296, in load
    return loads(fp.read(),
UnicodeDecodeError: 'cp949' codec can't decode byte 0xec in position 158: illegal multibyte sequence
```

이 에러가 발생했을때, open에서 encoding을 UTF-8로 설정하면 에러가 해결된다.

~~~
f = open('list.json', 'rt', encoding='UTF-8')
~~~
