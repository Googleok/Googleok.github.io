---
layout: post
title: spring- XML을 이용한 Spring 설정!
category: spring
tags: [spring, java, xml]
comments: true
---

1.8 XML을 이용한 설정 &#127765;        
==================================

> ### XML의 장점 &#127769;
```
XML은 단순한 텍스트 파일이다.
컴파일과 같은 별도의 빌드작업이 없다.
오브젝트의 관계가 바뀌는 경우에도 빠르게 변경사항을 반영할 수 있다.
스키마나 DTD를 이용해서 정해진 포맷을 따라 작성됐는지 손쉽게 확인할 수도 있다.
```
<hr/>

## 1.8.1 XML 설정 &#127766;
```
@Configuration == <beans>
@Bean == <bean>

@Bean 메소드를 통해 얻을수 있는 빈의 DI정보
-> 빈의 이름
-> 빈의 클래스
-> 빈의 의존 오브젝트
ex ) 130 p 참고!
```
<hr/>

> ### userDao() 전환 &#127769;
```
XML에서는 <property> 태그를 사용해 의존 오브젝트와의 관계를 정의한다.
 <property>
--> 속성: 1. name  == 프로퍼티의 이름.
          2. ref == 수정자 메소드를 통해 주입해줄 오브젝트의 빈 이름.

userDao.setConnectionMaker(connectionMaker());
=>  <bean id="userDao" class="springbook.dao.UserDao">
      <property name="connectionMaker" ref="connectionMaker" />
    </bean>
```
<hr/>

> ### XML의 의존관계 주입 정보 &#127769;
```
완성된 XML 설정정보
<beans>
    <bean id="connectionMaker" class="springbook.user.dao.DConnectionMaker" />
    <bean id="userDao" class="springbook.dao.UserDao">
          <property name="connectionMaker" ref="connectionMaker" />
    </bean>
</beans>
Tip! XML은 수정이 불편하므로 이름을 잘 정하고 수정하지 않는 편이 좋다.
```
<hr/>

## 1.8.2 XML을 이용하는 애플리케이션 컨텍스트 &#127767;
```
134P 1-40 참고
애플리케이션 컨텍스트 생성 부분
AnnotationConfigApplicationContext
GenericXmlApplicationContext
ClassPathXmlApplicationContext
```
<hr/>

## 1.8.3 DataSource 인터페이스로 변환 &#127768;

> ### DataSource 인터페이스 적용 &#127769;
```
앞에서 설명했던 ConnectionMaker 와 같은 것은 사용하지 않는다.
Spring에 DataSource는 여러가지 기능이 추가 되어 갖춰줘 있기 때문이다.
ex) 137P 1-42 참고!
```
<hr/>

> ### 자바 코드 설정 방식 &#127769;
```
138P 1-43, 1-44 참고!
```
<hr/>

> ### XML 설정 방식 &#127769;
```
<bean id="dataSource"
          class="org.springframework.jdbc.dataSource.SimpleDriverDataSource" />
여기에 <property> 태그와 ref 애트리뷰트로 의존할 빈 이름을 넣어 주면 된다.
```
<hr/>

## 1.8.4 프로퍼티 값의 주입 &#127770;
> ### 값 주입 &#127769;
```
텍스트나 단순 오브젝트 등을 수정자 메소드에 넣어주는 것을 스프링에서는 '값을 주입
한다' 고 말한다. 이것도 성격은 다르지만 일종의 DI라고 볼 수 있다.
여기서 <property>를 사용해 주입할 정보를 지정할 수 있다는 점에서 <property ref="">와 동일하다.
하지만 다른 빈 오브젝트의 레퍼런스(ref)가 아니라 단순 값(value)을 주입해주는 것이기
때문에 ref 애트리뷰트 대신 value 애트리뷰트를 사용한다.
```
```
<Before> 코드를 통한 DB 연결정보 주입
dataSource.setDriverClass(com.mysql.jdbc.Driver.class);
dataSource.setUrl("jdbc:mysql://localhost/springbook");
dataSource.setUsername("spring");
dataSource.setPassword("book");

<After> XML을 이용한 DB 연결정보 설정
<property name="driverClass" value="com.mysql.jdbc.Driver" />
<property name="url" value="jdbc:mysql://localhost/springbook" />
<property name="username" value="spring" />
<property name="password" value="book" />

==> ref 대신에 value를 사용했을 뿐
value의 값들은 다른 빈의 이름이 아니라 실제로 수정자 메소드의
파라미터로 전달되는 스트링 그 자체다.
```
<hr/>

> ### value 값의 자동 변환 &#127769;
```
여기서 재밌는 건 String 이라고 했는데 driverClass 는 Class 타입 오브젝트를 전달한다.
이 경우엔 스프링이 프로퍼티의 값을, 수정자 메소드의 파라미터 타입을 참고로 해서
적절한 형태로 변환해주기 때문이다.

최종 완성 DataSource는 141P 1-48을 참고하자
```
<br/>
<br/>
<br/>
<img src="http://notefolio.net/data/img/f9/ea/f9eaa90519b8742cdeffded9e486002e360e90bc10ca5c58d26cf8d460703680_v1.jpg" width="100%">
