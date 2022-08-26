---
layout: post
current: post
cover:  assets/images/springBoot/2022-07-11-springBoot-01_basic.jpg
navigation: True
title: springBoot 시큐리티(1)
date: 2022-08-22 13:00:00 +0900
tags: [springBoot]  
# tags.yml 선언한 값
class: post-template
subclass: 'post tag-springBoot'
author: BBInJunHwang
---

{% include table-of-contents_springBoot.html %}
<!-- <div>
<br>
<h2>[스프링부트] Security </h2><br>

<p align = "justify">
<font size=3>
SpringBoot 에서 시큐리티 설정을 위해서 WebSecurityConfigurerAdapter 상속받아서 정의한다.

기본적으로 configure(HttpSecurity) 재정의하며, http 요청에 대해서 처리가 가능하다.

.antiMatchers
-> 요청 경로마다 authenticated , hasRole 등 인증, 권한 여부로 제어가 가능하다.

.loginPage
-> 로그인 페이지 경로를 지정한다.

.loginProcessingUrl 
-> 로그인 요청 시 낚아채서 대신 로그인을 진행해준다.

<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/springBoot/springBoot03/ch03_security_config01.PNG" | relative_url }}' alt='absolute'>



컨트롤러 단에서도 요청에 대해서 간단하게 권한을 걸어 줄 수도 있다.<br>
@Secured<br>
@PreAuthroize (표현식 사용 가능 and / or)

<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/springBoot/springBoot03/ch03_security_config02.PNG" | relative_url }}' alt='absolute'>

</font>
</p>
</div> -->



<div>
    <header>
      <h2 class="title">[스프링부트] Security</h2><br>
    </header>
    <!-- <div>
      <h3 class="subTitle"></h3>
      <p> ->  </p>
    </div> -->
    <div class="listWrapper">
      <!-- <span style="font-size: 20px;"></span> -->
      <ul class="imageList">
        <li>
          <div class="area">
            <img data-action="zoom" src="/assets/images/springBoot/springBoot03/ch03_security_config01.PNG" alt='absolute'>
            <div>
              <span>SpringBoot 에서 시큐리티 설정을 위해서 WebSecurityConfigurerAdapter 상속받아서 정의한다.<br>
                    기본적으로 configure(HttpSecurity) 재정의하며, http 요청에 대해서 처리가 가능하다.<br><br>
                    .antiMatchers<br>
                    -> 요청 경로마다 authenticated , hasRole 등 인증, 권한 여부로 제어가 가능하다.<br><br>
                    .loginPage<br>
                    -> 로그인 페이지 경로를 지정한다.<br><br>
                    .loginProcessingUrl <br>
                    -> 로그인 요청 시 낚아채서 대신 로그인을 진행해준다.</span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <img data-action="zoom" src="/assets/images/springBoot/springBoot03/ch03_security_config02.PNG" alt='absolute'>
            <div>
              <span>컨트롤러 단에서도 요청에 대해서 간단하게 권한을 걸어 줄 수도 있다.<br>
                    @Secured<br>
                    @PreAuthroize (표현식 사용 가능 and / or)</span>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div> 

