---
layout: post
title:  "[Solr] Java에서 Solr query 예제 (Solr Query Example From Java)"
categories: [Java/Solr]
author : "Junny"
tags: [SolrJ,Lucene]
---
# [Solr] 자바에서 솔라 쿼리 예제 

Java에서 Apache Solr를 이용한 쿼리 생성 및 리퀘스트와 리스폰즈 결과받기.
Maven을 이용하여 Solr 버전에 맞게 Jar파일을 가져온다.
~~~
<!-- https://mvnrepository.com/artifact/org.apache.solr/solr-solrj -->
<dependency>
  <groupId>org.apache.solr</groupId>
  <artifactId>solr-solrj</artifactId>
  <version>7.1.0</version>
</dependency>
~~~
SolrQuery 클래스로 쿼리를 생성하고, QueryResponse 클래스를 이용하여 결과를 받는다.
1. 쿼리 생성 예제 소스.
~~~
	// 솔라에 보낼 쿼리  
	// .set을 이용하여 명시적으로 필드를 지정하여 데이터를 선정할 수 있다.  
	// .addXXXField를 사용하여 해당 필드에 여러번의 데이터를 입력할 수 있다. 
	SolrQuery sQuery =  new  SolrQuery(); 
	sQuery.set("fl",  "id, BOOK, AUTHOR");  // solr에 저장된 필드명 
	sQuery.set("hl",  "on");  // 하이라이팅 사용 
	sQuery.set("hl.fl",  "BOOK");// 하이라이팅 적용 필드 
	sQuery.set("hl.fragsize",  "150");  // 하이라이팅 적용된 글자 사이즈 
	sQuery.set("facet",  true);  // 패싯 사용 
	sQuery.addFacetField("BOOK");  // 패싯 필드 추가 
	sQuery.addFacetField("AUTHOR");  // 패싯 필드 추가 
	sQuery.set("sort",  "AUTHOR ASC");  // 정렬방식 ,를 사용하여 여러번 사용가능 
	sQuery.set("q",  "AUTHOR:홍길동");  // 쿼리 
	sQuery.set("group",  true);  // 그룹화 사용 
	sQuery.set("group.field",  "AUTHOR");  // 그룹화 필드 
	sQuery.set("group.limit",  "3");  // 그룹화해서 가져올 갯수  
~~~
2. 쿼리를 호출하여 결과를 받는 예제 소스
~~~
QueryResponse response =  solrQuery(sQuery);  // 데이터를 성공적으로 가져오면 status == 0 이다  
if  (response.getStatus()  ==  0)  {  // response.getXXX로 데이터 불러오면됨.  
	GroupResponse GroupResponse = response.getGroupResponse();	//리스폰즈에서 그룹 데이터 가져옴
	List<GroupCommand> grouplist = GroupResponse.getValues();  //그룹 리스폰즈의 값들을 List로 가져옴
	Iterator<GroupCommand> iterator = grouplist.iterator();			// 이터레이터 사용
	while(iterator.hasNext()) {
		GroupCommand groupCommand = iterator.next();	// 이터레이터로 데이터 불러옴
		List<Group> groupList = groupCommand.getValues(); //그룹 커맨드에서 데이터를 List로 저장
		//for문을 이용하여 데이터 접근
	}
}
~~~
<br>

###### 출처  나의 네이버 블로그  :<a href="https://blog.naver.com/tjdwns8574/221330018373"> https://blog.naver.com/tjdwns8574/221330018373</a>