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
<br>
<h2>[스프링부트] Security </h2><br>

SpringBoot 에서 시큐리티 설정을 위해서 WebSecurityConfigurerAdapter 상속받아서 정의한다.

기본적으로 configure(HttpSecurity) 재정의하며, http 요청에 대해서 처리가 가능하다.

.antiMatchers
-> 요청 경로마다 authenticated , hasRole 등 인증, 권한 여부로 제어가 가능하다.

.loginPage
-> 로그인 페이지 경로를 지정한다.

.loginProcessingUrl 
-> 로그인 요청 시 낚아채서 대신 로그인을 진행해준다.

<img data-action="zoom" src='{{ "/assets/images/springBoot/springBoot03/ch03_security_config01.PNG" | relative_url }}' alt='absolute'>



컨트롤러 단에서도 요청에 대해서 간단하게 권한을 걸어 줄 수도 있다.<br>
@Secured<br>
@PreAuthroize (표현식 사용 가능 and / or)

<img data-action="zoom" src='{{ "/assets/images/springBoot/springBoot03/ch03_security_config02.PNG" | relative_url }}' alt='absolute'>





