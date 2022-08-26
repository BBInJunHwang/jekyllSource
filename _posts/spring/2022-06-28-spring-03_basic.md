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

{% include table-of-contents_springFramework.html %}
<!-- <div>
<br>
<h2>[스프링] @datasource 설정</h2><br>

<p align = "justify">
<font size=3>
dataSource 설정 -> dsForCommon 명으로 DB 연결정보 설정한다.<br>
value 값은 Properties 값을 읽어온다.<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring03/ch03_bean_xml_01.PNG" | relative_url }}' alt='absolute'>
</font>
</p>

<p align = "justify">
<font size=3>
SqlSessionFactoryBean 사용해서 mybatis <-> spring 연동한다. <br>
ref=dsForCommon명으로 연결정보를 넘겨주며, <br>
configLocation 설정을 통해 VO alias 등 설정 가능하다.<br>
mapperLocations 설정을 통해서 매퍼관련 자원 위치를 설정하면 xml 읽고 로드한다.<br>
mapperLocation 경우 list 가 아닌 단일 value로 설정한다.<br>
<br>
SqlSessionTemplate은 mybatis 연동모듈 핵심이며, sqlSession 생성하고 트랜잭션을 관리한다.<br>
또한 SqlSession을 구현하며, 대체하는 역할을 하며 쓰레드에 안전하게 여러개의 DAO나 매퍼에서 공유된다.<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring03/ch03_bean_xml_02.PNG" | relative_url }}' alt='absolute'><br>


아래는 트랜잭션을 처리하는 설정으로 sqlSessionFactory 객체를 넘겨준다.<br>
선언적 트랜잭션 처리 방법으로 AOP를 사용한다.<br>
트랜잭션을 실행하는 대상 Method 설정하며, insert,update,delete 로 시작하는 method에 트랜잭션을 설정한다.<br>
<br>
기본 rollback 은 checked Exception에 적용이 안되며, runtimeException에만 적용<br>
-> 모든 예외를 두고 싶다면 Exception으로 적용 필요 <br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring03/ch03_bean_xml_03.PNG" | relative_url }}' alt='absolute'><br>
AOP pointcut 으로 적용할 범위를 지정가능하다.
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring03/ch03_bean_xml_04.PNG" | relative_url }}' alt='absolute'>
</font>
</p>

<p align = "justify">
<font size=3>
@Transaction 어노테이션을 사용한 트랜잭션 관리 -> 차후 추가예정
</font>
</p>
</div> -->


<div>
    <header>
      <h2 class="title">[스프링] @datasource 설정</h2><br>
    </header>
    <!-- <div>
      <h3 class="subTitle">스프링 빈이란?</h3>
      <p> ->  스프링 IOC 컨테이너가 관리하는 자바객체</p>
      <p> ->  New로 생성한 객체가 아님</p>
      <p> ->  ApplicationContext 로 얻을 수 있음</p>
    </div> -->
    <div class="listWrapper">
      <!-- <span style="font-size: 20px;">스프링 빈 xml 등록 방법</span> -->
      <ul class="imageList">
        <li>
          <div class="area">
            <img data-action="zoom" src="/assets/images/spring/spring03/ch03_bean_xml_01.PNG" alt='absolute'>
            <div>
              <span>dataSource 설정 -> dsForCommon 명으로 DB 연결정보 설정한다.<br>
                    value 값은 Properties 값을 읽어온다.<br></span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <div>
            <img data-action="zoom" src="/assets/images/spring/spring03/ch03_bean_xml_02.PNG" alt='absolute'>   
              <span>SqlSessionFactoryBean 사용해서 mybatis <-> spring 연동한다. <br>
                    ref=dsForCommon명으로 연결정보를 넘겨주며, <br>
                    configLocation 설정을 통해 VO alias 등 설정 가능하다.<br>
                    mapperLocations 설정을 통해서 매퍼관련 자원 위치를 설정하면 xml 읽고 로드한다.<br>
                    mapperLocation 경우 list 가 아닌 단일 value로 설정한다.<br>
                    <br>
                    SqlSessionTemplate은 mybatis 연동모듈 핵심이며, sqlSession 생성하고 트랜잭션을 관리한다.<br>
                    또한 SqlSession을 구현하며, 대체하는 역할을 하며 쓰레드에 안전하게 여러개의 DAO나 매퍼에서 공유된다.<br></span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <img data-action="zoom" src="/assets/images/spring/spring03/ch03_bean_xml_03.PNG" alt='absolute'>
            <div>
              <span>아래는 트랜잭션을 처리하는 설정으로 sqlSessionFactory 객체를 넘겨준다.<br>
                    선언적 트랜잭션 처리 방법으로 AOP를 사용한다.<br>
                    트랜잭션을 실행하는 대상 Method 설정하며, insert,update,delete 로 시작하는 method에 트랜잭션을 설정한다.<br>
                    <br>
                    기본 rollback 은 checked Exception에 적용이 안되며, runtimeException에만 적용<br>
                    -> 모든 예외를 두고 싶다면 Exception으로 적용 필요 <br></span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <img data-action="zoom" src="/assets/images/spring/spring03/ch03_bean_xml_04.PNG" alt='absolute'>
            <div>
              <span>AOP pointcut 으로 적용할 범위를 지정가능하다.</span>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>