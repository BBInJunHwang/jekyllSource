---
layout: post
current: post
cover:  assets/images/spring/2022-06-12-spring-01_basic.jpg
navigation: True
title: spring 시작하기(7) AOP PointCut
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
<h2>[스프링] AOP PointCut</h2><br>

PointCuts<br>
-> 원하는 method만 weving 될 수 있도록 (JoinPoint가 될 수 있도록) 지정한다. <br>
-> Proxy는 모든 target으로 지정한 클래스 내 모든 메소드에 대해서 호출이 된다. (대상 선별없이) <br>
-> 아래 예시처럼 service2 클래스에 대해서 타켓을 지정해놓은 상태이다. <br>
<br>
JoinPoint<br>
-><br>
<br>
Weaving<br>
-> 뜨개질?<br>

<br>
classic 방법<br>
advice를 적용하기 위해서 매번 advisor를 생성해줘야한다.<br>
-> 불편<br>
<br>


<p align = "justify">
<font size=3>
pointcut 빈을 생성하며, method명을 지정한다. class=" advisor 빈을 생성 후 advice 할 빈과<br>
pointcut 할 빈을 연결한다.<br>
proxy 빈에 logBeforeAdvice -> classBeforeAdvisor로 변경한다.<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring07/ch07_bean_xml_01.PNG" | relative_url }}' alt='absolute'><br>

SelectService는 before advice 제외된다.<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring07/ch07_main_class_aop_nobefore_01.PNG" | relative_url }}' alt='absolute'><br>

poincut 빈에 등록된 method 인 SelectService2 는 before advice 적용된다.<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring07/ch07_main_class_aop_yesbefore_01.PNG" | relative_url }}' alt='absolute'><br>

만약 다른 advice도 pointcut을 지정하고 싶으면 advisor을 하나 더 생성 후 적용한다.<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring07/ch07_bean_xml_02.PNG" | relative_url }}' alt='absolute'><br>

SelectService는 before, after advice 제외된다.<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring07/ch07_main_class_aop_nobeforeafter_01.PNG" | relative_url }}' alt='absolute'><br>



간소화 방법<br>
advice-pointcut 합치는 방법<br>

다음과 같이 NameMatchMethodPointcutAdvisor class를 이용해서 namematch + advisor 기능을 이용한다.<br>
before advice 경우 SelectService2에만 적용가능하게 설정했으며, <br>
after advice 경우 SelectService2, SelectService3 에 적용을 했다. (mappedName -> mappedNames 변경 후 list-value 구조로 변경)<br>
<br>
실행하게 되면, SelectService는 before, after advice 제외<br>
SelectService2는 before, after advice 모두 적용<br>
SelectService3는 after advice만 적용<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring07/ch07_bean_xml_03.PNG" | relative_url }}' alt='absolute'><br>


RegexpMethodPointcutAdvisor class를 이용해서 정규식을 적용 할 수도 있다.<br>
mappedNames -> patterns 변경 후 .(anycharacter) *(0개이상) -> .*Service2* Method 이름 중에서 해당 패턴이 있는 대상에 대해서만<br>
around advice를 적용한다.<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring07/ch07_bean_xml_04.PNG" | relative_url }}' alt='absolute'><br>

정규 패턴 적용 전에는 SelectService3 에서 around advice 호출 되었지만<br>
정규 패턴 적용 후에는 around advice 제외한다.<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring07/ch07_main_class_aop_regexp_01.PNG" | relative_url }}' alt='absolute'><br>

</font>
</p>
</div> -->






<div>
    <header>
      <h2 class="title">[스프링] AOP PointCut</h2><br>
    </header>
    <div>
      <h3 class="subTitle">PointCuts</h3>
      <p> ->  원하는 method만 weving 될 수 있도록 (JoinPoint가 될 수 있도록) 지정한다.</p>
      <p> ->  Proxy는 모든 target으로 지정한 클래스 내 모든 메소드에 대해서 호출이 된다. (대상 선별없이)</p>
      <p> ->  아래 예시처럼 service2 클래스에 대해서 타켓을 지정해놓은 상태이다.</p>
      <h3 class="subTitle">JoinPoint</h3>
      <p> ->  </p>
      <h3 class="subTitle">Weaving</h3>
      <p> ->  </p>
      <span>classic 방법<br>
            advice를 적용하기 위해서 매번 advisor를 생성해줘야한다.<br>
            -> 불편</span>
    </div>
    <div class="listWrapper">
      <!-- <span style="font-size: 20px;">스프링 빈 xml 등록 방법</span> -->
      <ul class="imageList">
        <li>
          <div class="area">
            <img data-action="zoom" src="/assets/images/spring/spring07/ch07_bean_xml_01.PNG" alt='absolute'>
            <div>
              <span>pointcut 빈을 생성하며, method명을 지정한다. class=" advisor 빈을 생성 후 advice 할 빈과<br>
                    pointcut 할 빈을 연결한다.<br>
                    proxy 빈에 logBeforeAdvice -> classBeforeAdvisor로 변경한다</span>
            </div>
            <img data-action="zoom" src="/assets/images/spring/spring07/ch07_main_class_aop_nobefore_01.PNG" alt='absolute'>
            <div>
              <span>SelectService는 before advice 제외된다.</span>
            </div>
            <img data-action="zoom" src="/assets/images/spring/spring07/ch07_main_class_aop_yesbefore_01.PNG" alt='absolute'>
            <div>
              <span>poincut 빈에 등록된 method 인 SelectService2 는 before advice 적용된다.</span>
            </div>
            <img data-action="zoom" src="/assets/images/spring/spring07/ch07_bean_xml_02.PNG" alt='absolute'>
            <div>
              <span>만약 다른 advice도 pointcut을 지정하고 싶으면 advisor을 하나 더 생성 후 적용한다.</span>
            </div>
            <img data-action="zoom" src="/assets/images/spring/spring07/ch07_main_class_aop_nobeforeafter_01.PNG" alt='absolute'>
            <div>
              <span>SelectService는 before, after advice 제외된다.</span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <span>간소화 방법<br>
                  advice-pointcut 합치는 방법</span>
            <img data-action="zoom" src="/assets/images/spring/spring07/ch07_bean_xml_03.PNG" alt='absolute'>
            <div>
              <span>다음과 같이 NameMatchMethodPointcutAdvisor class를 이용해서 namematch + advisor 기능을 이용한다.<br>
                    before advice 경우 SelectService2에만 적용가능하게 설정했으며, <br>
                    after advice 경우 SelectService2, SelectService3 에 적용을 했다. (mappedName -> mappedNames 변경 후 list-value 구조로 변경)<br>
                    <br>
                    실행하게 되면, SelectService는 before, after advice 제외<br>
                    SelectService2는 before, after advice 모두 적용<br>
                    SelectService3는 after advice만 적용</span>
            </div>
            <img data-action="zoom" src="/assets/images/spring/spring07/ch07_bean_xml_04.PNG" alt='absolute'>
            <div>
              <span>RegexpMethodPointcutAdvisor class를 이용해서 정규식을 적용 할 수도 있다.<br>
                    mappedNames -> patterns 변경 후 .(anycharacter) *(0개이상) -> .*Service2* Method 이름 중에서 해당 패턴이 있는 대상에 대해서만<br>
                    around advice를 적용한다.</span>
            </div>
            <img data-action="zoom" src="/assets/images/spring/spring07/ch07_main_class_aop_regexp_01.PNG" alt='absolute'>
            <div>
              <span>정규 패턴 적용 전에는 SelectService3 에서 around advice 호출 되었지만<br>
                    정규 패턴 적용 후에는 around advice 제외한다.<br></span>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>


