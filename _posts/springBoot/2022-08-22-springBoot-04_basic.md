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
<br>
<h2>[스프링부트] Security Service </h2><br>

SecurityConfig 설정에서 loginProcessingUrl로 등록된 요청이 올때 자동으로 호출이 된다.

UserDetailsService를 상속 받아서 custom이 가능하며, 
loadUserByUsername 를 정의한다.

DB 조회를 통해서 유저가 확인되면, 
UserDetails 타입인 PrincipalDetails를 리턴한다.

<img data-action="zoom" src='{{ "/assets/images/springBoot/springBoot04/ch04_security_service01.PNG" | relative_url }}' alt='absolute'>


로그인이 정상 완료 시 session 공간 내 secuirty contextholder key값에 session 정보를 저장한다.
반드시 구조는 Authentication 타입이며, 
Authentication 안에 User정보는 UserDetails 타입이여야 한다. 





