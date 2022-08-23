---
layout: post
current: post
cover:  assets/images/spring/2022-06-12-spring-01_basic.jpg
navigation: True
title: spring 시작하기(2) @annotation
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
<h2>[스프링] @Autowired / @Resource</h2><br>

<p>Annotation 이란?</p>
<p align = "justify">
<font size=3>
-> Annotation은 자바 소스 코드에 추가하여 사용할 수 있는 메타데이터의 일종<br>
-> 스프링에서 빈 인스턴스가 생성된 이후 @Autowired를 설정한 메서드가 자동으로 호출, 인스턴스가 자동으로 주입
</font></p>

<p>
<font size=3>
xml 설정과 같이 기존 service 에 주입되던 dao 빈을 주석처리 해도 정상적으로 주입이 가능하다.<br>
@Autowired로 의존 관계를 주입받을 경우, context:component scan  태그를 사용해야한다.
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring02/ch02_bean_xml_01.PNG" | relative_url }}' alt='absolute'><br>

생성자 주입, setter 주입 등 생략이 되어도 @Autowired 통해 필드에 주입 후 사용이 가능하다.<br>
-> 차후 생성자,setter,필드 주입간의 차이점 추가할 예정이며, 생성자 주입을 사용을 권장한다.<br>
ex) 아래는 @Autowired를 이용한 필드 주입 예시
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring02/ch02_bean_class_01.PNG" | relative_url }}' alt='absolute'>
</font>
</p>

@Autowired / @Resource
<p>
<font size=3>
@Autowired는 타입(class 타입)으로 의존성 주입하며, 변수, 생성자, Setter메서드, 일반 메서드 사용 가능하다.<br>
타입 > name 순으로 찾기 떄문에 같은 타입 2개이상 빈이 존재하면 에러가 발생한다.<br>
ex) 같은 클래스로 2개이상 빈이 등록 시 동일 타입 빈 중 어떤 빈을 사용해야 할지 모른다.<br>
bean id="test1" class="com.ijhwang.userDao"<br>
bean id="test2" class="com.ijhwang.userDao"<br>
<br>
해당 부분 해결을 위한 @Qualifier("test1") 이용해서 사용할 빈 설정이 가능하며, required=false 값을 통해<br>
빈이 검색되지 않았을 시 에러도 방지한다.<br>
<br>
@Resource는 이름으로 주입하며, 변수, Setter메서드등에 적용 가능하다.<br>
@Resource(name="빈명") 으로 사용 가능<br>
name 설정이 없다면 name > 타입 순으로 찾아준다.
</font>
</p>
</div>