---
layout: post
title:  "[Solr] DataImportHandler/mysql 설정"
date:   2020-09-14
categories: [Java/Solr]
author : "Junny"
tags : [solr, dataimporthandler, solr-mysql]
---
# [Solr] DataImportHandler/mysql 설정


Solr에서 Mysql을 이용한 데이터 색인을 위해서, mysql-connector를 import 해야된다.

우선 ${SOLR_HOME}/dist에 maven에서 해당하는 mysql-connector를 설치한다.
(SOLR_HOME은 Solr가 설치된 폴더)

${SOLR_HOEME}/server/solr/에 core를 생성한다.

solr admin을 이용하면 쉽게 생성할 수 있다.(http://localhost:8983/solr/)로 이동하면 coreAdmin을 생성할 수 있다.

![Solr admin core 생성페이지](/assets/image/java/Solr/2020-09-14-solr-dataimporthandler.png)


core를 생성했다면 다음 위치로 이동한다.
${SOLR_HOEME}/server/solr/[core]/conf 
해당 폴더에 있는 solrconfig.xml 파일을 수정해야된다.

중간에 위치하는 부분에서 dataimporthandler와 mysqlconnector를 추가해준다.

```
  <lib dir="${solr.install.dir:../../../..}/contrib/extraction/lib" regex=".*\.jar" />
  <lib dir="${solr.install.dir:../../../..}/dist/" regex="solr-cell-\d.*\.jar" />

  <lib dir="${solr.install.dir:../../../..}/contrib/clustering/lib/" regex=".*\.jar" />
  <lib dir="${solr.install.dir:../../../..}/dist/" regex="solr-clustering-\d.*\.jar" />

  <lib dir="${solr.install.dir:../../../..}/contrib/langid/lib/" regex=".*\.jar" />
  <lib dir="${solr.install.dir:../../../..}/dist/" regex="solr-langid-\d.*\.jar" />

  <lib dir="${solr.install.dir:../../../..}/contrib/velocity/lib" regex=".*\.jar" />
  <lib dir="${solr.install.dir:../../../..}/dist/" regex="solr-velocity-\d.*\.jar" />

  <!-- 이부분을 추가해준다 -->
  <lib dir="${solr.install.dir:../../../..}/dist/" regex="solr-dataimporthandler-\d.*\.jar" />
  <lib dir="${solr.install.dir:../../../..}/dist/" regex="mysql-connector-java-\d.*\.jar"  />
```


그리고 그 밑에 dataimport의 requesthandler를 추가해준다.
config는 해당 폴더에 위치한 mysql 접속 정보 및 쿼리를 작성하면된다.

```
  <requestHandler name="/dataimport" class="org.apache.solr.handler.dataimport.DataImportHandler" > 
       <lst name="defaults">
         <!-- 색인을 진행할 mysql 설정파일명 -->
         <str name="config">mysql-data-config.xml</str> 
       </lst>
  </requestHandler>
```

mysql-data-config.xml

```
<dataConfig>
    <dataSource type="JdbcDataSource" driver="com.mysql.jdbc.Driver" url="jdbc:mysql://localhost:3306/database" user="userid" password="password"/>
    <document>
       <entity name="data_entity" transformer="HTMLStripTransformer"
    		query="SELECT id,book_name,author,regdate from bookwriter">
			<field column="id" name="id"/>
			<field column="book_name" name="book_name"/>
			<field column="author" name="author"/>
			<field column="regdate" name="regdate"/>
        </entity>
    </document>
</dataConfig>
```
datasource는 DB 접속정보를 입력하고

entity는 해당내용으로 색인을 진행한다. 복수개로 등록하여 다른 쿼리를 이용하여 많은 데이터를 색인할 수 있다.
field의 name은 managed-schema에 등록해야된다.

이로써 dataimporthandler 설정이 완료되었다.

cf)
solr 7.5버전 이상에서는 한글형태소분석기 nori가 지원된다

managed-schema에 
<field name="book_name" type="text_ko" indexed="true" stored="true"/>
이렇게 입력하면 한글 형태소 분석기를 사용한 색인이 된다.

field의 속성은 각각의 다음을 의미한다.
name: Field의 이름
type: Field의 자료 형태
indexed: 색인을 할 Field인지 여부
stored: 전체 내용을 저장할지 여부
multiValued: 한 문서에 이 Field가 여러개 존재할 수 있는지 여부


