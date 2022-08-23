---
layout: post
current: post
cover:  assets/images/spring/2022-06-12-spring-01_basic.jpg
navigation: True
title: spring 시작하기(6) AOP
date: 2022-06-12 03:00:00 +0900
tags: [spring]  
# tags.yml 선언한 값
class: post-template
subclass: 'post tag-spring'
author: BBInJunHwang
---

{% include table-of-contents_springFramework.html %}
<br>
<h2>[스프링] AOP</h2><br>

AOP란?<br> 
<p align = "justify">
<font size=3>
Aspect Oriented Programming 관점지향 프로그래밍으로 사용자 기준이 아닌 (사용자가 요구한 업무 로직) 개발자 필요로 인한 운영을 위한 업무 (주가 아닌 부가업무)

ex) 로그처리, 권한 처리(보안) 트랜잭션 등 주 업무와 상관없는 업무를 처리한다.

주 업무 앞과 뒤에 전반적인 처리를 한다.
만약 주 업무 소스코드가 없는 경우 직접 로그나 실행시간 등 코드를 넣을 수 없지만 AOP를 이용하면 업무코드를 수정하지 않아도 꽂아 넣을 수 있다.

사용자는 Proxy를 호출 하면 보조 업무 실행 후 주업무를 호출한다.


1. 자바 Proxy를 이용한 공통로직 구현
Proxy.newProxyInstance(가져올 클래스 로더, 클래스 인터페이스들, 보조업무)
-> InvocationHandler 이용해서 보조 업무를 정의하며, invoke에서 실제 업무를 호출하며, 결과값을 전달한다.

proxy.SelectService 호출 시 호출시간을 출력하는 보조 업무가 service 클래스 소스 수정없이 호출된다.
<img data-action="zoom" src='{{ "/assets/images/spring/spring06/ch06_main_class_aop_01.PNG" | relative_url }}' alt='absolute'>


2. 스프링 AOP
Before, After returnning, After throwing, Around 4가지가 존재한다.

먼저 자바 Proxy를 이용한 결과와 동일한 Around로 구현을 해본다.

Component-scan 으로 xml에 빈 설정을 하지않은 service는 xml 상에서 aop 등록시 빈으로 넘겨 줄 수 없기 때문에<br>
service2를 copy 후  xml상 빈으로 등록한다.<br>
target 으로 해당 빈을 ref 넘겨주며, AOP를 적용할 interceptorNames list 구조로 logAroundAdvice 빈을 넘겨준다.
<img data-action="zoom" src='{{ "/assets/images/spring/spring06/ch06_bean_xml_01.PNG" | relative_url }}' alt='absolute'>

LogAroundAdvice 클래스에는 invoke를 구현한다. 자바 Proxy와 동일하게 Object 로 실행 후 결과값을 넘겨준다.
<img data-action="zoom" src='{{ "/assets/images/spring/spring06/ch06_advice_class_aop_01.PNG" | relative_url }}' alt='absolute'>

Main 실행 시 동일한 결과가 호출된다.
<img data-action="zoom" src='{{ "/assets/images/spring/spring06/ch06_main_class_aop_02.PNG" | relative_url }}' alt='absolute'>

before, after, afterThrowing 추가
<img data-action="zoom" src='{{ "/assets/images/spring/spring06/ch06_bean_xml_02.PNG" | relative_url }}' alt='absolute'>

before<br>
-> 해당 메소드가 실행되기전 호출 클래스나, 파라마터 등 조회 가능
<img data-action="zoom" src='{{ "/assets/images/spring/spring06/ch06_before_class_aop_01.PNG" | relative_url }}' alt='absolute'>

after<br>
-> 해당 메소드 실행 후 호출 클래스나, 파라미터, 결과값등 조회가능
<img data-action="zoom" src='{{ "/assets/images/spring/spring06/ch06_after_class_aop_01.PNG" | relative_url }}' alt='absolute'>

afterThrowing<br>
-> 따로 구현메소드는 없으며, exception에 따른 직접 구현을 하면된다 <br>
-> 파라미터가 null 인경우 runtimeException을 발생시켰으며, 해당 부분으로 빠진다.
<img data-action="zoom" src='{{ "/assets/images/spring/spring06/ch06_afterThrowing_class_aop_01.PNG" | relative_url }}' alt='absolute'>
<img data-action="zoom" src='{{ "/assets/images/spring/spring06/ch06_bean_service_class_01.PNG" | relative_url }}' alt='absolute'>

순서는 before -> 메소드 실행 -> after -> around 순

</font>
</p>