---
layout: post
current: post
cover:  assets/images/spring/2022-06-12-spring-01_basic.jpg
navigation: True
title: spring 시작하기(1) bean 생성
date: 2022-06-12 03:00:00 +0900
tags: [spring]  
# tags.yml 선언한 값
class: post-template
subclass: 'post tag-spring'
author: BBInJunHwang
---
{% include spring-table-of-contents.html %}
<br>
<h2>[스프링] Bean 개념 및 생성</h2><br>
스프링 빈이란?<br>
-> 스프링 IOC 컨테이너가 관리하는 자바객체<br>
-> New로 생성한 객체가 아님<br>
-> ApplicationContext 로 얻을 수 있음<br>

스프링 빈 xml 등록 방법

xml 설정에서 다음과 같이 설정한다.
bean id 값, bean class 경로 지정 후 
<img data-action="zoom" src='{{ "/assets/images/spring/spring01/ch01_bean_xml_01.PNG" | relative_url }}' alt='absolute'>

property 를 통해서  setter method 이용한 주입이 가능하다.
set메서드명 -> name값으로 치환되며 
ex) setFormat -> format 으로 set 생략 + 첫글자 대->소 로 인식한다.
<img data-action="zoom" src='{{ "/assets/images/spring/spring01/ch01_bean_class_01.PNG" | relative_url }}' alt='absolute'>

DAO <-> Service 간 의존관계가 존재할시 DI(Dependency Injection (의존관계 주입))이 가능하다.

Dao를 빈으로 생성 후 Service빈에 constructor-arg ref=빈명 을 통해서 넘겨줄 수 있다.
<img data-action="zoom" src='{{ "/assets/images/spring/spring01/ch01_bean_xml_02.PNG" | relative_url }}' alt='absolute'>

Service 쪽 생성자에 dao를 넘겨 받아 생성한다.
<img data-action="zoom" src='{{ "/assets/images/spring/spring01/ch01_bean_class_02.PNG" | relative_url }}' alt='absolute'>