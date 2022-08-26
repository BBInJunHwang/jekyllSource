---
layout: post
current: post
cover:  assets/images/spring/2022-06-12-spring-01_basic.jpg
navigation: True
title: spring 시작하기(5) DI 3가지 방법
date: 2022-06-12 03:00:00 +0900
tags: [spring]  
# tags.yml 선언한 값
class: post-template
subclass: 'post tag-spring'
author: BBInJunHwang
---

{% include table-of-contents_springFramework.html %}
<!-- <div>
<h2>[스프링] DI 3가지 방법</h2><br>

DI 3가지 방법을 설명한다.<br>


<p align = "justify">
<font size=3>
아래와 같이 Component-scan 과 base package 를 설정해주면 @Component, @Service, @Repository 등<br>
빈으로 선언한 클래스를 스캔 후 빈으로 등록한다.<br><br>
context:annotation-config 과 다른점은 annotation-config은 xml 등 이미 선언된 빈에 대해서
@Autowired 등 자동 주입을 진행해주기 떄문에 반드시 미리 빈을 선언 해놓아야 한다.<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;"  data-action="zoom" src='{{ "/assets/images/spring/spring05/ch05_bean_xml_01.PNG" | relative_url }}' alt='absolute'>

1. 필드주입 <br>
-> dao 클래스에서 @Autowired private List userList 필드부분에 선언<br>
-> service 클래스에 @Autowired private CommonDao commonDao 필드부분에 선언<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;"  data-action="zoom" src='{{ "/assets/images/spring/spring05/ch05_bean_dao_class_field_01.PNG" | relative_url }}' alt='absolute'>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;"  data-action="zoom" src='{{ "/assets/images/spring/spring05/ch05_bean_service_class_field_01.PNG" | relative_url }}' alt='absolute'>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;"  data-action="zoom" src='{{ "/assets/images/spring/spring05/ch05_bean_main_class_01.PNG" | relative_url }}' alt='absolute'>


2. setter 주입 <br>
-> dao 클래스에서 @Autowired setUserList 부분에 선언 <br>
-> service 클래스에서 @Autowired setCommonDao 부분에 선언 <br>
※ dao 클래스에서 @Autowired 대신 @Resource 사용해도 동일하며 <br>
@Autowired는 타입 > name 순서,
@Resource는 name > 타입 순서로 탐색하며 @Resource 사용시 빈 name을 명시해주는게 좋다.
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;"  data-action="zoom" src='{{ "/assets/images/spring/spring05/ch05_bean_dao_class_setter_01.PNG" | relative_url }}' alt='absolute'>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;"  data-action="zoom" src='{{ "/assets/images/spring/spring05/ch05_bean_service_class_setter_01.PNG" | relative_url }}' alt='absolute'>

3. 생성자 주입<br>
-> dao 클래스에서 생성자로 userList를 받은 후 설정한다. <br>
-> service 클래스에서 생성자로 commonDao를 받은 후 설정한다. <br>
※ 생성자 주입에서는 @Autowired, @Resource 등 어노테이션 생략이 가능하다. (단 반드시 단일생성자일때만 )
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;"  data-action="zoom" src='{{ "/assets/images/spring/spring05/ch05_bean_dao_class_constructor_01.PNG" | relative_url }}' alt='absolute'>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;"  data-action="zoom" src='{{ "/assets/images/spring/spring05/ch05_bean_service_class_constructor_01.PNG" | relative_url }}' alt='absolute'>


필드주입 vs setter 주입 vs 생성자 주입

필드 주입<br>
장점 - 코드양이 적다.<br>
단점 - final 키워드 사용 불가, 의존관계 파악 불가, 순환참조 탐지불가 (서버 정상기동, 호출시 stackOverFlowError 발생)<br>
     - 순환참조 방지 패치 -> 기존에 호출 시 A빈이 B빈을 참조하고, B빈이 A빈을 참조할 시 호출되는 시점에서 무한참조로 에러가 발생했지만,<br>
       후에 스프링 부트2.6에서는 서버 기동시 cycle형성으로 기동 실패로 나온다.<br>

setter 주입<br>
장점 - ??<br>
단점 - final 키워드 사용 불가<br>

생성자 주입<br>
장점 -  final 키워드 사용 가능 -> 다른 클래스에서 호출시 불변적용 가능<br>
    -  ※NPE 방지
     - 보통 필드에 @Autowired를 붙이는 경우가 많지만, 생성자 주입을 사용하도록 노력하자<br>
단점 - 코드가 조금 길어진다.<br>

생성자 주입을 통한 NPE 방지란?

먼저 아래와 같이 setter 주입을 예시로 했으며, 필드주입도 동일한 현상이 일어난다.<br>
dao 클래스 @Repository 주석 처리를 통한 빈등록 x <br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;"  data-action="zoom" src='{{ "/assets/images/spring/spring05/ch05_bean_dao_class_notBean_01.PNG" | relative_url }}' alt='absolute'>
service 클래스 setCommonDao를 통한 dao 주입<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;"  data-action="zoom" src='{{ "/assets/images/spring/spring05/ch05_bean_service_class_setter_02.PNG" | relative_url }}' alt='absolute'>
기동 시 dao 클래스는 null 인상태로 주입되며, service 클래스에서 호출되기 전까지 null인지 알 수 없음<br>
실제 서버 기동 후 해당 클래스가 호출될 때 알 수 있다.(런타임 에러시 발견)
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;"  data-action="zoom" src='{{ "/assets/images/spring/spring05/ch05_bean_service_class_setter_NPE_01.PNG" | relative_url }}' alt='absolute'>

생성자 주입 시 아래와 같이 생성과 동시에 주입 되며, 컴파일 시 에러 발생을 통한 미리 알 수 있다.<br>
실제로 서비스를 운영하는 시점에서 서버가 정상기동되면 놓칠 수 있는 부분이기 때문에, 컴파일 자체에서 에러가 나면 바로 인지 및 패치가 가능하다.
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;"  data-action="zoom" src='{{ "/assets/images/spring/spring05/ch05_bean_service_class_constructor_02.PNG" | relative_url }}' alt='absolute'>
</font>
</p>
</div> -->




<div>
    <header>
      <h2 class="title">[스프링] DI 3가지 방법</h2><br>
    </header>
    <div>
      <h3 class="subTitle">DI 3가지 방법을 설명한다.</h3>
      <p> ->  필드주입</p>
      <p> ->  setter 주입</p>
      <p> ->  생성자 주입</p>
    </div>
    <div class="listWrapper">
      <img data-action="zoom" src="/assets/images/spring/spring05/ch05_bean_xml_01.PNG" alt='absolute'>
      <span style="font-size: 20px;">아래와 같이 Component-scan 과 base package 를 설정해주면 @Component, @Service, @Repository 등<br>
                                   빈으로 선언한 클래스를 스캔 후 빈으로 등록한다.<br><br>
                                   context:annotation-config 과 다른점은 annotation-config은 xml 등 이미 선언된 빈에 대해서
                                   @Autowired 등 자동 주입을 진행해주기 떄문에 반드시 미리 빈을 선언 해놓아야 한다.</span>
      <ul class="imageList">
        <li>
          <div class="area">
            <span>1. 필드주입 <br></span> 
            <img data-action="zoom" src="/assets/images/spring/spring05/ch05_bean_dao_class_field_01.PNG" alt='absolute'>
            <img data-action="zoom" src="/assets/images/spring/spring05/ch05_bean_service_class_field_01.PNG" alt='absolute'>
            <img data-action="zoom" src="/assets/images/spring/spring05/ch05_bean_main_class_01.PNG" alt='absolute'>
            <div>
              <span>-> dao 클래스에서 @Autowired private List userList 필드부분에 선언<br>
                    -> service 클래스에 @Autowired private CommonDao commonDao 필드부분에 선언</span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <span>2. setter 주입 <br></span> 
            <img data-action="zoom" src="/assets/images/spring/spring05/ch05_bean_dao_class_setter_01.PNG" alt='absolute'>
            <img data-action="zoom" src="/assets/images/spring/spring05/ch05_bean_service_class_setter_01.PNG" alt='absolute'>
            <div>
              <span>-> dao 클래스에서 @Autowired setUserList 부분에 선언 <br>
                    -> service 클래스에서 @Autowired setCommonDao 부분에 선언 <br>
                    ※ dao 클래스에서 @Autowired 대신 @Resource 사용해도 동일하며 <br>
                    @Autowired는 타입 > name 순서,
                    @Resource는 name > 타입 순서로 탐색하며 @Resource 사용시 빈 name을 명시해주는게 좋다.</span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <span>3. 생성자 주입 <br></span> 
            <img data-action="zoom" src="/assets/images/spring/spring05/ch05_bean_dao_class_constructor_01.PNG" alt='absolute'>
            <img data-action="zoom" src="/assets/images/spring/spring05/ch05_bean_service_class_constructor_01.PNG" alt='absolute'>
            <div>
              <span>-> dao 클래스에서 생성자로 userList를 받은 후 설정한다. <br>
                    -> service 클래스에서 생성자로 commonDao를 받은 후 설정한다. <br>
                    ※ 생성자 주입에서는 @Autowired, @Resource 등 어노테이션 생략이 가능하다. (단 반드시 단일생성자일때만 )</span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <div>
              <span>필드주입 vs setter 주입 vs 생성자 주입<br>
               1. 필드 주입<br>
               장점 - 코드양이 적다.<br>
               단점 - final 키워드 사용 불가, 의존관계 파악 불가, 순환참조 탐지불가 (서버 정상기동, 호출시 stackOverFlowError 발생)<br>
                    - 순환참조 방지 패치 -> 기존에 호출 시 A빈이 B빈을 참조하고, B빈이 A빈을 참조할 시 호출되는 시점에서 무한참조로 에러가 발생했지만,<br>
                    후에 스프링 부트2.6에서는 서버 기동시 cycle형성으로 기동 실패로 나온다.<br>
               <br>
               2. setter 주입<br>
               장점 - ??<br>
               단점 - final 키워드 사용 불가<br>
               <br>
               3. 생성자 주입<br>
               장점 -  final 키워드 사용 가능 -> 다른 클래스에서 호출시 불변적용 가능<br>
               -  ※NPE 방지
                    - 보통 필드에 @Autowired를 붙이는 경우가 많지만, 생성자 주입을 사용하도록 노력하자<br>
               단점 - 코드가 조금 길어진다.<br>
               <br>
               생성자 주입을 통한 NPE 방지란?
               <br>
               먼저 아래와 같이 setter 주입을 예시로 했으며, 필드주입도 동일한 현상이 일어난다.<br>
               dao 클래스 @Repository 주석 처리를 통한 빈등록 x </span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <img data-action="zoom" src="/assets/images/spring/spring05/ch05_bean_dao_class_notBean_01.PNG" alt='absolute'>
            <div>
              <span>service 클래스 setCommonDao를 통한 dao 주입</span>
            </div>
            <img data-action="zoom" src="/assets/images/spring/spring05/ch05_bean_service_class_setter_02.PNG" alt='absolute'>
            <div>
              <span>기동 시 dao 클래스는 null 인상태로 주입되며, service 클래스에서 호출되기 전까지 null인지 알 수 없음<br>
                    실제 서버 기동 후 해당 클래스가 호출될 때 알 수 있다.(런타임 에러시 발견)</span>
            </div>
            <img data-action="zoom" src="/assets/images/spring/spring05/ch05_bean_service_class_setter_NPE_01.PNG" alt='absolute'>
            <img data-action="zoom" src="/assets/images/spring/spring05/ch05_bean_service_class_constructor_02.PNG" alt='absolute'>  
            <div>
              <span>생성자 주입 시 아래와 같이 생성과 동시에 주입 되며, 컴파일 시 에러 발생을 통한 미리 알 수 있다.<br>
                    실제로 서비스를 운영하는 시점에서 서버가 정상기동되면 놓칠 수 있는 부분이기 때문에, 컴파일 자체에서 에러가 나면 바로 인지 및 패치가 가능하다.</span>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
  

