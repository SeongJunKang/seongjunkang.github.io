---
layout: post
title:  "[Spring] Mock Junit Test Example"
date:   2020-08-24
categories: [Java/Spring]
author : "Junny"
tags : [Mock,Mockito,Junit,단위테스트]
---
# [Spring] Mock Junit Test Example

Spring에서 Junit만 사용하여 통합테스트만 하고있었다.
근데 점점 규모가 커지면서 테스트의 시간이 늘어나기 시작해서 단위테스트 방법을 찾아보다가 Mockito의 기능을 확인하고 예제로 남긴다.

테스트 환경
java : 1.8 jdk
spring-version : 4.1.4.RELEASE
build : maven

pom.xml에 추가된 의존 라이브러리
```
<dependency>
	<groupId>junit</groupId>
	<artifactId>junit</artifactId>
	<version>4.11</version>
	<scope>test</scope>
</dependency>
<dependency>
	<groupId>org.mockito</groupId>
	<artifactId>mockito-all</artifactId>
	<version>1.9.5</version>
	<scope>test</scope>
</dependency>
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-test</artifactId>
	<version>${org.springframework-version}</version> //4.1.4.RELEASE
	<scope>test</scope>
</dependency>
```


TEST class 소스
``` 
@RunWith(MockitoJUnitRunner.class)
public class serviceTest  {
  @Mock
  private TestService service;
  
  private Test test;
  
  @Before
  public void setup() {
  	this.test = new Test();
  	this.test.setValue("테스트");
  	this.test.setId(1);
  }
  
  @Test
  public void 테스트ID로_값호출() {
  	given(service.findById(any())).willReturn(test);
  	
  	Test param = new Test();
  	param.setId(1);
  	final Test returnValue = service.findById(param);
  	Assert.assertNotEquals(null,returnValue.getValue());
  }
}
```

매우 기본적인 예시를 작성했다. 추후에 복잡하게 변경되면 다시 작성해야겠다.
TDD에서 좀 더 발전된 예시가 BDD(Behavior Driven Development)이다. 행동으로 진행하며 테스트를 진행하는 방법이다.
BDD는 시나리오 기반 테스트를 진행하며, TDD는 함수 기반 테스트를 진행한다.
하나의 시나리오는 Given, When, Then구조를 가지는 것으로 기본패턴을 권장한다.
```
@Test
public void bddTest() throws Exception{
        // given : 선행조건 기술
        // when : 기능 수행
        // then : 결과 확인
}
```


출처 : [https://cornswrold.tistory.com/366](https://cornswrold.tistory.com/366)
출처 : [https://beomseok95.tistory.com/293](https://beomseok95.tistory.com/293)