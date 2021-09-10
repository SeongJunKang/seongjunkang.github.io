---
layout: post
title: "[JPA] JPA에서 객체 일부분만 가져오기"
date: 2021-09-10
categories: [Java/JPA]
author : "Junny"
tags : [Java,jpa]
---
# [JPA] JPA에서 객체 일부분만 가져오기

JPA를 사용해 repository에서 객체를 불러올 때, Entity 전체의 데이터를 가져온다.

API를 통해 데이터를 전달하는데 필요없는 부분까지 혹은 보이지 않았으면 하는 부분까지 전달할 필요는 없다.

아래와 같은 Entity가 있다.
~~~
@Entity
@Data
@Table(name="book")
@NoArgsConstructor(access = AccessLevel.PROTECTED)
public class Book {
    @Id
    @GeneratedValue
    private Long id;
    
    @Column(name="BOOK_NAME")
    private String bookName;
    
    private String publisher;
    
    private String author;

    @Column(name="PUBLISHING_DATE")
    @Temporal(TemporalType.DATE)    
    private LocalDate publishingDate;
}
~~~

책 검색에서 사용되는 컬럼은 bookName과 author만 보내고 싶다고 한다면

다음과 같은 맵핑 클래스르 작성하면 된다.

변수명은 Entity의 변수명과 일치해야한다.

~~~
@Getter
@Setter
@AllArgsConstructor
public class BookNameAndAuthor {
    private String bookName;
    private String author;
}
~~~

Getter와 Setter는 Jackson에서 사용하기 때문에 추가했다.

AllArgsConstructor 어노테이션은 JPA에서 객체를 반환할 때 사용한다.

Repository 인터페이스에서 위에서 정의한 객체를 리턴으로 반환하면 원하는 내용의 값만 불러올 수 있다.

~~~
@Repository("bookRepository")
public interface BookRepository extends CrudRepository<Book, Long> {
    List<BookNameAndAuthor> findAll();
}
~~~

