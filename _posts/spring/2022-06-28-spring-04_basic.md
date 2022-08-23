---
layout: post
current: post
cover:  assets/images/spring/2022-06-12-spring-01_basic.jpg
navigation: True
title: spring 시작하기(4) ArrayList 빈생성 및 component 스캔과 Service-dao간 DI
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
<h2>[스프링] ArrayList 빈생성 및 component 스캔과 Service-dao간 DI</h2><br>

<p align = "justify">
<font size=3>
ArrayList 형으로 빈 생성 가능하며 아래와 같이 userList bean 생성 로직이다.<br>
-> class=java.util.ArrayList 로 List형의 빈이며, 절대로 UserVO 타입의 빈이 아니다.<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring04/ch04_bean_xml_01.PNG" | relative_url }}' alt='absolute'>

다음과 같이  applicationContext에서 빈을 가져올때 빈 id 와 type 모두 가져올 수 있지만<br>
List.class 타입을 가진 bean이 2개 존재 -> userList, userList2 해당 경우는 에러가 발생할 수 있다.<br>
-> 타입으로 찾게되면 동일 타입 빈 중 어떤걸 가져와야 할지 모르기 떄문, 그렇기 때문에 명시 해주자.<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring04/ch04_bean_class_01.PNG" | relative_url }}' alt='absolute'>


아래와 같이 Component-scan 과 base package 를 설정해주면 @Component, @Service, @Repository 등<br>
빈으로 선언한 클래스를 스캔 후 빈으로 등록한다.
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring04/ch04_bean_xml_02.PNG" | relative_url }}' alt='absolute'>

base package에 선언된 dao,service 클래스들은 모두 빈으로 등록되었으며, <br>
service -> @Autowired를 통한 dao 클래스 의존성 주입<br>
dao -> @Autowired 통한 List빈이 주입<br>
main 클래스에서 getBean을 통해 service 빈을 가져온 후 최종 return
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring04/ch04_bean_dao_class_01.PNG" | relative_url }}' alt='absolute'>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring04/ch04_bean_service_class_01.PNG" | relative_url }}' alt='absolute'>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring04/ch04_bean_main_class_01.PNG" | relative_url }}' alt='absolute'>

</font>
</p>
</div>