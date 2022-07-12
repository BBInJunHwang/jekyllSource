---
layout: post
current: post
cover:  assets/images/spring/2022-06-12-spring-01_basic.jpg
navigation: True
title: spring 시작하기(3) @datasource
date: 2022-06-12 03:00:00 +0900
tags: [spring]  
# tags.yml 선언한 값
class: post-template
subclass: 'post tag-spring'
author: BBInJunHwang
---

{% include spring-table-of-contents.html %}
<br>
<h2>[스프링] @JDBC 설정</h2><br>

dataSource 설정 -> dsForCommon 명으로 DB 연결정보 설정한다.
value 값은 Properties 값을 읽어온다.
<img data-action="zoom" src='{{ "/assets/images/spring/spring03/ch03_bean_xml_01.PNG" | relative_url }}' alt='absolute'>

SqlSessionFactoryBean 사용해서 mybatis<->spring 연동한다.
ref=dsForCommon명으로 연결정보를 넘겨주며, 
configLocation 설정을 통해 VO alias 등 설정 가능하다.
mapperLocations 설정을 통해서 매퍼관련 자원 위치를 설정하면 xml 읽고 로드한다.
mapperLocation 경우 list 가 아닌 단일 value로 설정한다.

SqlSessionTemplate은 mybatis 연동모듈 핵심이며, sqlSession 생성하고 트랜잭션을 관리한다.
SqlSession을 구한하며, 대체하는 역할을 하며 쓰레드에 안전하게
여러개의 DAO나 매퍼에서 공유된다.
<img data-action="zoom" src='{{ "/assets/images/spring/spring03/ch03_bean_xml_02.PNG" | relative_url }}' alt='absolute'>


트랜잭션을 처리하는 설정으로 sqlSessionFactory 객체를 넘겨준다.

아래는 선언적 트랜잭션 처리 방법으로 AOP를 사용한다.
트랜잭션을 실행하는 대상 Method 설정하며, insert,update,delete 로 시작하는 method에 트랜잭션을 설정한다.

기본 rollback 은 checked Exception에 적용이 안되며
runtimeException에만 적용, 모든 예외를 두고 싶다면 Exception으로 적용 필요 
<img data-action="zoom" src='{{ "/assets/images/spring/spring03/ch03_bean_xml_03.PNG" | relative_url }}' alt='absolute'>

AOP pointcut 으로 적용할 범위를 지정가능하다.
<img data-action="zoom" src='{{ "/assets/images/spring/spring03/ch03_bean_xml_04.PNG" | relative_url }}' alt='absolute'>


@Transaction 어노테이션을 사용한 트랜잭션 관리