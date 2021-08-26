---
layout: post
title:  "Spring  vs Spring Boot"
subtitle:   "Spring  vs Spring Boot"
categories: java&spring
tags: Spring   
comments: true
header-img: img/Java&Spring/spring-boot-logo.jpg
---


# Spring  vs Spring Boot

---

안녕하세요. 첫 글로 만나뵙는 내용은 "Spring vs Spring Boot" 입니다. Spring Boot로 처음 Backend 개발을 하면서 Spring이라는 거대한 생태계를 이해하지 못한 채 빠르게 프로젝트를 진행하였습니다. 대부분 서칭을 해보면 단순히 **Spring Boot가 개발하는데 편리하다.**, **의존성을 자동으로 주입해준다.** 는 등의 내용을 찾아볼 수 있습니다. 그래서 오늘은 *Spring vs Spring Boot*에 대해 알아보도록 하겠습니다.

## 1.  Spring

Spring이란, java 애플리케이션 개발을 위한 전반적인 인프라를 제공해주는 framework입니다. 

###  Spring Framework

#### (1) Spring Container

Spring framework의 핵식으로 IoC규칙에 의해 애플리케이션 내의 object들의 생명주기를 관리합니다.

- Ioc(Inversion of Control)

  > IoC란 다른말로 하면 DI(Dependency Injection)으로 IoC Container는 오브젝트의 생성과 관계설정, 사용, 제거 등의 작업을 대신 해준다하여 붙여진 이름입니다.
  >
  > IoC Container에 의해 관리되는 오브젝트들은 Bean 이라고 부르며, IoC Container는 Bean을 저장한다고 하여, BeanFactory 라고도 합니다. 
  >
  > BeanFactory는 하나의 인터페이스이며, Application Context는 BeanFactory의 구현체를 상속받고 있는 인터페이스입니다. 

- Bean

  >Bean이란 Spring의 IoC Container(=DI Container)를 통해 관리(생성,제어)되는 객체를 말합니다.
  >
  >Spring에서 Bean을 설정하는 방법은 여러가지가 있습니다.
  >
  > **XML을 통한 등록**
  >
  >```xml
  ><bean id="hello" class="me.yj.test.bean.Hello">
  > <property name="printer" ref="myPrinter">
  ></bean>
  >```
  >
  > **자동인식을 통한 Bean 등록**
  >
  >  컴포넌트 스캐너는 지정된 클래스패스 밑에 있는 모든 패키지의 클래스를 대상으로 특정 애노테이션이 존재하는지를 파악하고 빈으로 등록합니다. 컴포넌트 스캐너에 의해 필터링 되는 애노테이션을 `스테레오타입 애노테이션`이라고 부르고 주로 사용하는 스테레오 타입 애노테이션은 다음과 같습니다.
  >
  >
  >
  >  \- @Component : 빈으로 지정하는 가장 기본적인 애노테이션
  >
  >  \- @Repository : 데이터 액세스 계층의 DAO 또는 리포지토리 클래스에 사용.
  >
  >  \- @Service : 서비스 계층의 클래스에 사용.
  >
  >  \- @Controller : MVC 컨트롤러에 사용. 스프링 웹 서블릿에 의해 웹 요청을 처리하는 컨트롤러 빈으로 선정됩니다.
  >
  >```java
  >@Component
  >public class AnnotationHello { }
  >```
  >
  > **자바코드에 의한 등록 : @Configuration, @Bean**
  >
  >  \- @Configuration 또한 @Component를 사용하기 때문에 빈 스캐너에 의해 자동 검색 됩니다.
  >
  >  \- @Configuration를 사용한 클래스 자체도 Bean으로 등록됩니다.
  >
  >  \- @Bean으로 등록된 메서드의 return 객체를 Bean으로 등록합니다.
  >
  >  \- @Bean("name")으로 이름을 지정할 수 있으며 이름을 지정하지 않을 시 메서드 명이 id가 됩니다.
  >
  >  \- new 연산을 사용하지만, 매번 다른 객체가 생성되지 않고 싱글톤으로 DI가 됩니다.
  >
  >```java
  >@Configuration
  >public class AnnotatedHelloConfig{
  >   @Bean
  >   public Hello hello(Printer printer){
  >       return new Hello(printer);
  >   }
  >   @Bean
  >   public Printer printer(){
  >       return new Printer();
  >   }
  >}
  >```


#### (2) Module

Spring Framework에는 다음과 같은 모듈이 존재하며 각각의 모듈은 애플리케이션 개발시간과 속도를 향상시켜줍니다. 

<img style="max-height:50%; max-width:50%;" src="https://s3.ap-south-1.amazonaws.com/myinterviewtrainer-domestic/public_assets/assets/000/000/839/original/spring_framework.png?1628693487">

## 2. Spring Boot

그렇다면 Spring Boot는 왜 나왔을까? 이유는 아래 예시를 보면 알 수 있습니다.

```xml
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix">
        <value>/WEB-INF/views/</value>
    </property>
    <property name="suffix">
        <value>.jsp</value>
    </property>
</bean>

<mvc:resources mapping="/webjars/**" location="/webjars/"/>

<servlet>
    <servlet-name>dispatcher</servlet-name>
    <servlet-class>
        org.springframework.web.servlet.DispatcherServlet
    </servlet-class>
    <init-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>/WEB-INF/my-servlet.xml</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
</servlet>

<servlet-mapping>
    <servlet-name>dispatcher</servlet-name>
    <url-pattern>/</url-pattern>
</servlet-mapping>
```

위의 내용은 Spring MVC를 사용하기 위한 최소한의 세팅 방법입니다. 자세한 내용은 생략하고 그냥 한눈에 봐도 복잡하다는 것을 알 수 있습니다. 앞선 내용만 봐도 개발자가 개발하기 앞서 세팅 해주어야 할 부분이 많다는것을 예상할 수 있고 때문에 Spring Boot가 나오게 되었습니다.  

### Spring Boot

스프링부트는 자동설정(AutoConfiguration)을 이용하였고 어플리케이션 개발에 필요한 모든 내부 디펜던시를 관리합니다. 

```xml
<dependency>
   <groupId>org.springframework</groupId>
   <artifactId>spring-webmvc</artifactId>
   <version>4.2.2.RELEASE</version>
</dependency>
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.5.3</version>
</dependency>
<dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate-validator</artifactId>
    <version>5.0.2.Final</version>
</dependency>
<dependency>
    <groupId>log4j</groupId>
    <artifactId>log4j</artifactId>
    <version>1.2.17</version>
</dependency>
```

기존의 Spring Framework를 사용했을 때에 비하면 복잡성을 크게 줄였지만, 어플리케이션에는 Spring MVC, Jackson Databind, Hibernate 코어 및 Log4j와 같은 유사한 요구사항들이 있습니다. 이들의 복잡성을 또한번 줄이기 위해 SpringBoot Starter라고 불리는것이 도입되었습니다.

### SpringBoot Starter

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

SpringBoot Starter에는 다음과 같은 옵션들이 있습니다.

>- spring-boot-starter-web-services : SOAP 웹 서비스
>- spring-boot-starter-web : Web, RESTful 응용프로그램
>- spring-boot-starter-test : Unit testing, Integration Testing
>- spring-boot-starter-jdbc : 기본적인 JDBC
>- spring-boot-starter-hateoas : HATEOAS 기능을 서비스에 추가
>- spring-boot-starter-security : 스프링 시큐리티를 이용한 인증과 권한
>- spring-boot-starter-data-jpa : Spring Data JPA with Hibernate
>- spring-boot-starter-cache : 스프링 프레임워크에 캐싱 지원 가능
>- spring-boot-starter-data-rest : Spring Data REST를 사용하여 간단한 REST 서비스 노출

---

## 요약

오늘은 *Spring vs Spring Boot* 에 대해 알아보았습니다. 처음에 Spring Boot만 보았을때 추상화가 너무 잘되어 있어 사용하기 편할것 같다 라고 생각이 들었는데, Spring을 모르고 Spring Boot를 사용하면서 개발할 때 이유를 모르고 사용한 경우가 많았습니다. 오늘 내용을 통해 이 둘의 차이를 알게 되었고, 다음 포스팅은 Spring Boot를 이용해 프로젝트를 진행하면서 발생한 이슈와 해결, 새로 배운 내용을 진행하겠습니다. 
