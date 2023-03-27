---
layout: post
title: "[Spring] Controller advice로 Exception handling하기"
date: 2023-03-27
categories: [Java/Spring]
author : "Junny"
tags : [Spring, controller, controller_advice, spring_boot]
---

## ControllerAdvice로 exception handling하기
<br>

### #1 배경
<p>
- Controller에서 발생하는 에러를 모두 try catch로 처리하다 보면 소스가 점점 지저분해진다. dto의 validation까지 적용한다면 더더욱 길어진다. 그리고ResponseEntity로 객체와 에러를 모두 처리하려다 보니 리턴 객체 유형을 와일드카드를 써야되는 문제도 있다.<br><br>
- 이 에러 처리를 공통적으로 해결할 수 있는 방안을 찾다가 Spring3.2에 도입된 @ControllerAdvice라는 스프링의 기능이 유용해서 적용하는 방법을 작성하려고 한다.
</p>

<br>

### #2 개요
<p>
- @ControllerAdvice는 전역 에러 핸들러로 어느 컨트롤러에서 발생한 에러라도, 여기에서 정의된 내용이 있으면 그 내용으로 에러를 처리한다. (Spring AOP를 이용)<br><br>
- 일반 MVC에서 사용하는 @ControllerAdvice와 Rest Api에서 사용하는 @RestControllerAdvice가 있다. <br><br>
- 아래의 코드는 @ControllerAdvice와 @RestControllerAdvice의 선언부인데, 살펴보면 @RestControllerAdvice에는 @ControllerAdvice가 포함되어 있어 사용법은 같으나, @ResponseBody가 적용되어 있어 결과가 JSON값으로 전송된다.
</p>

``` java
@Target(ElementType.TYPE)  
@Retention(RetentionPolicy.RUNTIME)  
@Documented  
@Component  
public @interface ControllerAdvice {
}

@Target(ElementType.TYPE)  
@Retention(RetentionPolicy.RUNTIME)  
@Documented  
@ControllerAdvice   // controllerAdvice 포함하고 있음
@ResponseBody  		// 결과값이 JSON형식
public @interface RestControllerAdvice {
}
```
<br>

### #3 @ExceptionHandler 
<p>
특정 에러 클래스를 등록하여 controller에서 에러가 발생했을 경우를 확인하여 실행하는 기능을 수행한다.
</p>
<br>

### #4 적용방법
<p>
- @ExceptionHandler 어노테이션을 이용하여 적용한다. value 값으로는 해당하는 오류를 작성하면 된다. 여러개일 경우 {}으로 감싸 배열형태로 나열하면 된다. <br><br>
- @ResponseStatus를 지정하여 에러가 발생하면 상태 코드를 변경할 수 있다.
</p>
<br>

``` java
@ControllerAdvice  
public class ControllerExceptionAdvice {  
  // 1. Internal exception
  @ExceptionHandler(value = {PathNotConnectedException.class, NoAroundPathException.class})  
  @ResponseStatus(value = HttpStatus.INTERNAL_SERVER_ERROR)  
  public ResponseEntity<String> pathNotFoundExceptions(Throwable e) {  
    return ResponseEntity.internalServerError().body(e.getMessage());  
  }
  
  // 2. Bad request(validation)
  @ExceptionHandler  
  @ResponseStatus(value = HttpStatus.BAD_REQUEST)  
  public ResponseEntity<Object[]> badRequestExceptions(MethodArgumentNotValidException e) {  
    return ResponseEntity.status(HttpStatus.BAD_REQUEST).body(e.getBindingResult().getFieldErrors().toArray());  
  }
  
  // 3. bad request(json parsing error)
  @ExceptionHandler  
  @ResponseStatus(value = HttpStatus.BAD_REQUEST)  
  public ResponseEntity<String> badRequestExceptions(HttpMessageNotReadableException e) {  
    return ResponseEntity.status(HttpStatus.BAD_REQUEST).body(e.getMessage());  
  }
}
```
<p>
1. internal_server_error는 2가지 Exception이 발생하면 작동한다. 500 코드를 내보내며, 메세지의 내용을 보여준다. 여러 개를 등록하여 각 exception마다 다르게 처리할 수 있다.<br><br>
2. Request에서 validation을 이용한 정합성 체크(@NotNull, @Empty, @NotBlank 등)에서 오류가 발생하면 MethodArgumentNotValidException이 발생한다. 이것을 이용해서 에러 내용을 front-end에 전달할 수 있다.<br><br>
3.  Request에서 데이터 형식이 json이 아니거나, 파싱에서 에러가 발생하면 나타나는 오류를 처리할 수 있다.
</p>
<br>
<p>
@ControllerAdvice를 이용한 Exception handling은 프로젝트당 하나의 파일로 정의하는 것이 좋다. 여러개로 나누게 되면 관리하기가 어렵고 controller에 간섭하는 aop가 많으면 성능이슈도 있을 수 있다.
</p>
<br>
<p>
⚠ 틀린 내용이 있을 수 있습니다. 틀린 내용이 있다면 댓글로 알려주세요
</p>
<br>
<br>
참고 사이트<br>

1)  [Spring Boot @ControllerAdvice & @ExceptionHandler example](https://www.bezkoder.com/spring-boot-controlleradvice-exceptionhandler/) <br>

2) [[Spring] 전역 예외 처리를 위한 @ControllerAdvice와 @RestControllerAdvice](https://chanos.tistory.com/entry/Spring-%EC%A0%84%EC%97%AD-%EC%98%88%EC%99%B8-%EC%B2%98%EB%A6%AC%EB%A5%BC-%EC%9C%84%ED%95%9C-ControllerAdvice%EC%99%80-RestControllerAdvice) <br>
   
3) [Exception Handling을 어떻게 하면 더 잘할 수 있을까?](https://velog.io/@dhwlddjgmanf/%EA%BC%AC%EB%A6%AC%EB%B3%84-%EC%98%A4%EB%A5%98%EC%9D%BC%EC%A7%80-Exception-Handling%EC%9D%84-%EC%96%B4%EB%96%BB%EA%B2%8C-%ED%95%98%EB%A9%B4-%EB%8D%94-%EC%9E%98%ED%95%A0-%EC%88%98-%EC%9E%88%EC%9D%84%EA%B9%8C) <br>