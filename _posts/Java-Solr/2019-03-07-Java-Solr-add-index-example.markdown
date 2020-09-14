---
layout: post
title:  "[Solr] Java에서 Solr 실시간 인덱싱(SolrJ real time indexing)"
date:   2019-03-07
categories: [Java/Solr]
author : "Junny"
tags : [SolrJ, Lucene, SolrIndex]
---
# [Solr] Java에서 Solr 실시간 인덱싱

Java에서 Apache Solr를 이용한 쿼리 생성 및 리퀘스트와 리스폰즈 결과받기.
Maven을 이용하여 Solr 버전에 맞게 Jar파일을 가져온다.
여기서 사용된 버전은 7.5.0 버전임
~~~
<!-- https://mvnrepository.com/artifact/org.apache.solr/solr-solrj -->
<dependency>
  <groupId>org.apache.solr</groupId>
  <artifactId>solr-solrj</artifactId>
  <version>7.5.0</version>
</dependency>
~~~
SolrClient로 client 객체를 HttpSolrClient의 builder 메서드를 통해 만든다.
SolrInputDocument 객체의 인스턴스를 생성하고 해당 필드에 값을 담아서 client 객체에 담고 커밋하면 solr에 색인이 걸린다.

~~~
	//예제 소스
	String solrUrl = "http://localhost:8983/solr/test"
	SolrClient solrClient = new HttpSolrClient.Builder(solrUrl).build();
 	SolrInputDocument solrDoc = new SolrInputDocument();
	solrDoc.addField("BOOK_NAME", name);
	solrDoc.addField("AUTHOR", author);
	solrDoc.addField("PUBLISH", publish);
	solrClient.add(solrDoc);
	solrClient.commit();
~~~
