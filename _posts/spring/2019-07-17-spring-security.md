---
layout: post
title: spring- Spring Security 설정!
category: spring
tags: [spring, java, Security]
comments: true
---

# Spring Security 설정

## 1. 의존성 추가
~~~
		<!-- Spring Security -->
		<dependency>
		    <groupId>org.springframework.security</groupId>
		    <artifactId>spring-security-core</artifactId>
		    <version>4.1.3.RELEASE</version>
		</dependency>

		<dependency>
		    <groupId>org.springframework.security</groupId>
		    <artifactId>spring-security-config</artifactId>
		    <version>4.1.3.RELEASE</version>
		</dependency>

		<dependency>
			<groupId>org.springframework.security</groupId>
			<artifactId>spring-security-taglibs</artifactId>
		    <version>4.1.3.RELEASE</version>
		</dependency>

		<dependency>
			<groupId>org.springframework.security</groupId>
			<artifactId>spring-security-acl</artifactId>
		    <version>4.1.3.RELEASE</version>
		</dependency>
~~~
## 2. 스프링 부트

~~~
  <!-- https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-security -->
  <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-security</artifactId>
      <version>2.1.6.RELEASE</version>
  </dependency>

	-- 3버젼 --

	<filter>
		<filter-name>springSecurityFilterChain</filter-name>
		<filter-class>org.springframework.web.filter.DelegatingFilterProxy</filter-class>
	</filter>


	-- 4버젼 --

	AbstractSecurityWebApplicationInitializer를 상속받는 클래스 생성


	-- 5버젼 --
	관례 ㄱ ㄱ

~~~

## Security Filter Chain

	 1. ChannelProcessingFilter
	 2. SecurityContextPersistenceFilter		( auto-config default )
	 3. ConcurrentSessionFilter
	 4. LogoutFilter				( auto-config default )
	 5. UsernamePasswordAuthenticationFilter	( auto-config default )
	 6. DefaultLoginPageGeneratingFilter		( auto-config default )
	 7. CasAuthenticationFilter
	 8. BasicAuthenticationFilter			( auto-config default )
	 9. RequestCacheAwareFilter			( auto-config default )
	10. SecurityContextHolderAwareRequestFilter	( auto-config default )
	11. JaasApiIntegrationFilter
	12. RememberMeAuthenticationFilter
	13. AnonymousAuthenticationFilter		( auto-config default )
	14. SessionManagementFilter			( auto-config default )
	15. ExceptionTranslationFilter			( auto-config default )
	16. FilterSecurityInterceptor			( auto-config default )
