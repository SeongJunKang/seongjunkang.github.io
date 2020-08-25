---
layout: post
title:  "[Spring] MockMVC Test Properties 설정"
date:   2020-08-25
categories: [Java/Spring]
author : "Junny"
tags : [Mock,Mockito,Junit,단위테스트]
---
# [Spring] MockMVC Test Properties 설정

MockMVC 테스트를 하던 중에 Controller 테스트를 진행하고있었다.
properties에 설정된 값을 @Value를 이용하여 설정했었는데, MockMVC 테스트에서 @InjectMock을 사용했을경우
해당 값이 설정되지 않아 null로 발생하여 에러가 발생했다.

이 문제를 해결하고 그에 대한 내용을 작성하려고한다.

1. @TestPropertySource(location) 
2. @TestPropertySource(properties) 
3. ReflectionTestUtils class

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
//1. @TestPropertySource(locations= {"test.properties"})
//2. @TestPropertySource(properties= {"url=http://www.naver.com"})
public class controllerTest  {

  @InjectMocks
  private TestController controller;
  private MockMvc mvc;
  
  @Before
  public void setup() {
    //3. ReflectionTestUtils.setField(controller, "url", "http://www.naver.com");
    mvc = MockMvcBuilders.standaloneSetup(controller).build();
  }
  
  @Test
  public void 메인페이지() throws Exception {
    mvc.perform(get("/"))							// URL 호출
    .andExpect(status().isOk())					// status 확인
    .andExpect(view().name("index"))				// view의 name
    .andExpect(model().attributeExists("search"));		// model 에 객체 들어있는지 확인
  }
  
}
```

3 가지 방법을 들어 예시를 작성했다. 혹시 몰라서 작성해둔다.