---
layout: post
current: post
cover:  assets/images/springBoot/2022-07-11-springBoot-01_basic.jpg
navigation: True
title: springBoot 시큐리티(3)
date: 2022-08-22 13:00:00 +0900
tags: [springBoot]  
# tags.yml 선언한 값
class: post-template
subclass: 'post tag-springBoot'
author: BBInJunHwang
---

{% include table-of-contents_springBoot.html %}
<br>
<h2>[스프링부트] Security Jwt </h2><br>


기존 세션 로그인 방식은<br>  
ID,PW 서버로 전달 -> 인증 실시 -> 세션(메모리영역) 세션ID 생성 후 user 정보 저장 -> client 쿠키에 세션ID 전달 <br>
(웹 브라우저는 특별한 설정을 하지 않아도 쿠키라는 영역에 세션ID 저장한다.)<br>

인증 후 다음 요청 시 세션ID를 넣어서 보내면 서버에서는 세션ID 존재하는지 확인 후 인증한다.<br>
서버가 1대 문제없지만 서버 2대이상 -> 서버마다 세션 메모리영역이 따로 있음 -> 스티키 세션 or 메모리 서버 레디스 사용, 세션복사 등 해야함 <br>


JWT : json web token <br>

JWT 방식은 클라이언트에게 JWT 토큰 헤더에 넣어서 응답 <br>
요청마다 JWT 토큰으로 요청해야함<br>
서버는 JWT 토큰이 유효한지 판단 -> 필터 추가 필요 <br>

SecurityConfig 설정에서 기존 세션방식과 달리 JWT 토큰을 위해서 설정을 변경해준다. <br>

더 이상 세션을 사용하지 않기 때문에 STATELSS 정책을 준다.<br>
addFilter 통해서 JWT 토큰을 검증하는 필터를 적용한다. <br>
JWT 검증을 위해서 security Filter에 등록해줘야하며, 로그인 요청 시 인증 및 토큰생성 필터와, 그외 인증이 필요한 요청에서 토큰을 검증할 필터가 필요하다<br>

<img data-action="zoom" src='{{ "/assets/images/springBoot/springBoot05/ch05_security_config01.PNG" | relative_url }}' alt='absolute'>



로그인 요청 시 동작하는 필터이며, UsernamePasswordAuthenticationFilter 로 구현되어져 있다.

1. request를 받은 후 (json) id,pw를 이용해서 임시 인증토큰 UsernamePasswordAuthenticationToken 생성한다<br>

2. UsernamePasswordAuthenticationToken 를 이용해서 loadUserByUsername 함수를 실행해 DB내 id,pw를 비교한다.
이때 인증이 완료되면 successfulAuthentication를 호출한다.<br>
<img data-action="zoom" src='{{ "/assets/images/springBoot/springBoot05/ch05_security_filter01.PNG" | relative_url }}' alt='absolute'>

3. successfulAuthentication 에서는 인증이 완료된 Authentication 객체를 이용해서 JWT 토큰을 생성한다.
서버만 알고있는 고유값과 Hash 알고리즘을 이용해서 생성<br>
<img data-action="zoom" src='{{ "/assets/images/springBoot/springBoot05/ch05_security_jwt01.PNG" | relative_url }}' alt='absolute'>

4. 로그인 외 인증이 필요한 요청이 있을때 호출되는 필터로서 BasicAuthenticationFilter를 구현한다.
header 에 bearer 값을 추출 후 해당값내 userid를 추출해서 loadUserByname을 호출해 인증을 한다.<br>
이떄 유효한 사용자면 securityContextHoleder에 저장한다<br>
<img data-action="zoom" src='{{ "/assets/images/springBoot/springBoot05/ch05_security_filter02.PNG" | relative_url }}' alt='absolute'>




