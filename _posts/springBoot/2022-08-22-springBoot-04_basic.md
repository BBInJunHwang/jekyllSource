---
layout: post
current: post
cover:  assets/images/springBoot/2022-07-11-springBoot-01_basic.jpg
navigation: True
title: springBoot 시큐리티(2)
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
<h2>[스프링부트] Security Service </h2><br>

<p align = "justify">
<font size=3>
SecurityConfig 설정에서 loginProcessingUrl로 등록된 요청이 올때 자동으로 호출이 된다.

UserDetailsService를 상속 받아서 custom이 가능하며, 
loadUserByUsername 를 정의한다.

DB 조회를 통해서 유저가 확인되면, 
UserDetails 타입인 PrincipalDetails를 리턴한다.

<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/springBoot/springBoot04/ch04_security_service01.PNG" | relative_url }}' alt='absolute'>


로그인이 정상 완료 시 session 공간 내 secuirty contextholder key값에 session 정보를 저장한다.
반드시 구조는 Authentication 타입이며, 
Authentication 안에 User정보는 UserDetails 타입이여야 한다. 

</font>
</p>
</div> -->


<div>
    <header>
      <h2 class="title">[스프링부트] Security Service</h2><br>
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
            <img data-action="zoom" src="/assets/images/springBoot/springBoot04/ch04_security_service01.PNG" alt='absolute'>
            <div>
              <span>SecurityConfig 설정에서 loginProcessingUrl로 등록된 요청이 올때 자동으로 호출이 된다.<br>
                    <br>
                    UserDetailsService를 상속 받아서 custom이 가능하며, <br>
                    loadUserByUsername 를 정의한다.<br>
                    <br>
                    DB 조회를 통해서 유저가 확인되면, <br>
                    UserDetails 타입인 PrincipalDetails를 리턴한다.<br>
                    <br>
                    로그인이 정상 완료 시 session 공간 내 secuirty contextholder key값에 session 정보를 저장한다.<br>
                    반드시 구조는 Authentication 타입이며, <br>
                    Authentication 안에 User정보는 UserDetails 타입이여야 한다. </span>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div> 

