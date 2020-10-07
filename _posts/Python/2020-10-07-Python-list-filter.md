---
layout: post
title:  "[Pyhton] list filter using function"
date:   2020-10-07
categories: [Python]
author : "Junny"
tags : [Python, list, filter]
---
# [Python] list filter using function

Python에서 list를 사용해서 크롤링을 진행하고있었다.<br>
<br>
윈도우 자동 업데이트를 하면서 크롤링 하던 작업이 중간에 멈춰버림<br>
<br>
크롤링 해당하는 ID는 txt 파일로 목록을 가지고 있었는데, 약 100만개 정도여서<br>
<br>
기존에 다운로드 받은건 filter 하는 기능이 필요했다<br>
<br>
Python에서 List를 filter 하는 방법은 2가지가 있다.<br>

1. filter 내장함수 사용<br>
2. list comprehension<br>

1.filter 내장함수의 방법부터 살펴보겠다.<br>
공식 문서에 따르면 다음과 같이 나타나있다.<br>

```
filter(function, iterable)
Construct an iterator from those elements of iterable for which function returns true. iterable may be either a sequence, a container which supports iteration, or an iterator. If function is None, the identity function is assumed, that is, all elements of iterable that are false are removed.

Note that filter(function, iterable) is equivalent to the generator expression (item for item in iterable if function(item)) if function is not None and (item for item in iterable if item) if function is None.

See itertools.filterfalse() for the complementary function that returns elements of iterable for which function returns false.
```
<br>
사용 예제

- ID 목록중에서  {id}.xml의 파일이 존재하지 않는 파일만 filter하도록 진행
~~~
def file_exist(id):
	id = id.rstrip("\n")
	filePath = dir + id + ".xml"
	return os.path.isfile(filePath) == False

dir = "/usr/local/crawling/"
file = open(dir+"IdList.txt", mode="rt", encoding="utf-8")
id_list = file.readlines()

filtered_id_list = list(filter(file_exist, id_list))

print(len(id_list))
print(len(filtered_id_list))
~~~

2. list comprehension

[comprehension](http://pythonstudy.xyz/python/article/22-Python-Comprehension]에 대해서는 링크를 참조하시길 바랍니다.<br>

comprehension : 
- iterable한 오브젝트를 생성하기 위한 방법중 하나로 파이썬에서 사용할 수 있는 유용한 기능중 하나이다.



사용 예제
~~~
def file_exist(id):
	id = id.rstrip("\n")
	filePath = dir + id + ".xml"
	return os.path.isfile(filePath) == False

dir = "/usr/local/crawling/"
file = open(dir+"IdList.txt", mode="rt", encoding="utf-8")
id_list = file.readlines()

filtered_id_list = [id for id in id_list if file_exist(id)] #list comprehension

print(len(id_list))
print(len(filtered_id_list))
~~~

