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
{% include table-of-contents_springFramework.html %}
<div>
<br>
<h2>[스프링] Bean 개념 및 생성</h2><br>
<p>스프링 빈이란?</p>
<p align = "justify">
<font size=3>
->  스프링 IOC 컨테이너가 관리하는 자바객체<br>
->  New로 생성한 객체가 아님<br>
->  ApplicationContext 로 얻을 수 있음
</font></p>

스프링 빈 xml 등록 방법
<p><font size =3>
xml 파일에서 빈으로 등록 할 id , 빈 클래스 경로 선언<br>
bean 태그 내 property 를 통해서 setter method 이용한 주입이 가능하다.
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring01/ch01_bean_xml_01.PNG" | relative_url }}' alt='absolute'>
setter 메서드 동작 방식 : set메서드명 -> name값으로 치환 되며<br>
ex) setFormat -> format 으로 set 생략 + 첫글자 대->소 로 인식한다.<br>

<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring01/ch01_bean_class_01.PNG" | relative_url }}' alt='absolute'><br>
DAO <-> Service 간 의존관계가 존재할시 DI(Dependency Injection (의존관계 주입))이 가능하다.<br>
Dao 클래스를 빈으로 생성 후 Service 빈에 constructor-arg ref= 빈id를 통해서 넘겨 줄 수 있다.<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring01/ch01_bean_xml_02.PNG" | relative_url }}' alt='absolute'><br>
Service 클래스 생성자에 dao를 넘겨 받아 생성한다.<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring01/ch01_bean_class_02.PNG" | relative_url }}' alt='absolute'>

</font></p>
</div>



