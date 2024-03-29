---
layout: post
current: post
cover:  assets/images/spring/2022-06-12-spring-01_basic.jpg
navigation: True
title: spring 시작하기(8) Spring Profile
date: 2022-08-22 03:00:00 +0900
tags: [spring]  
# tags.yml 선언한 값
class: post-template
subclass: 'post tag-spring'
author: BBInJunHwang
---

{% include table-of-contents_springFramework.html %}
<!-- <div>
<br>
<h2>[스프링] Spring Profile</h2><br>

<p align = "justify">
<font size=3>
서버 환경 별 빈생성 분기가 필요한 경우 Spring Profile을 사용한다.<br>
톰캣 환경변수 내 설정한 값을 통해서 DB 정보, 접속 정보 등 분기가 가능하다.<br>

톰캣에 환경 변수 적용
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring08/ch08_spring_profile01.PNG" | relative_url }}' alt='absolute'>

AWS S3 접속정보<br>
프로퍼티스 파일내 선언한 ${key값} 으로 value를 가져올 수 있으며 <br>
만약 환경변수 값을 이용해서 프로퍼티스 key 값을 완성시키고 싶다면 <br>
${${환경변수값}.key값완성} 구조로 가져올 수 있다 <br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring08/ch08_spring_profile02.PNG" | relative_url }}' alt='absolute'>

DB 접속정보도 마찬가지로 분기가 가능하며, context에 각 환경별 접속정보를 구축해놓고 JNDI ID로 분기 실시<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/spring/spring08/ch08_spring_profile03.PNG" | relative_url }}' alt='absolute'>

</font>
</p>
</div> -->





<div>
    <header>
      <h2 class="title">[스프링] Spring Profile</h2><br>
    </header>
    <div>
      <h3 class="subTitle">스프링 profile 이란?</h3>
      <p> ->  서버 환경 별 빈생성 분기가 필요한 경우 Spring Profile을 사용한다.</p>
      <p> ->  톰캣 환경변수 내 설정한 값을 통해서 DB 정보, 접속 정보 등 분기가 가능하다.</p>
    </div>
    <div class="listWrapper">
      <!-- <span style="font-size: 20px;">스프링 빈 xml 등록 방법</span> -->
      <ul class="imageList">
        <li>
          <div class="area">
            <img data-action="zoom" src="/assets/images/spring/spring08/ch08_spring_profile01.PNG" alt='absolute'>
            <div>
              <span>톰캣에 환경 변수 적용</span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <img data-action="zoom" src="/assets/images/spring/spring08/ch08_spring_profile02.PNG" alt='absolute'>
            <div>
              <span>AWS S3 접속정보<br>
                    프로퍼티스 파일내 선언한 ${key값} 으로 value를 가져올 수 있으며 <br>
                    만약 환경변수 값을 이용해서 프로퍼티스 key 값을 완성시키고 싶다면 <br>
                    ${${환경변수값}.key값완성} 구조로 가져올 수 있다 </span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <img data-action="zoom" src="/assets/images/spring/spring08/ch08_spring_profile03.PNG" alt='absolute'>
            <div>
              <span>DB 접속정보도 마찬가지로 분기가 가능하며, context에 각 환경별 접속정보를 구축해놓고 JNDI ID로 분기 실시</span>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>