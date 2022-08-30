---
layout: post
current: post
cover:  assets/images/businessLogic/2022-08-22-business-01_basic.jpg
navigation: True
title: 로그인 프로세스 (2)
date: 2022-06-12 03:00:00 +0900
tags: [businessLogic]  
# tags.yml 선언한 값
class: post-template
subclass: 'post tag-businessLogic'
author: BBInJunHwang
---

{% include table-of-contents_businessLogic.html %}
<div>
    <header>
      <h2 class="title">[로그인] 인증 프로세스</h2><br>
    </header>
    <div>
      <h3 class="subTitle">프로세스 고려사항<br></h3>
      <p>1. 사내직원 여부</p>
      <p>-> 사내직원 : LDAP 인증</p>
      <p>-> 일반사용자 : DB 인증</p>
    </div>
    <div class="listWrapper">
      <span style="font-size: 20px;"></span>
      <ul class="imageList">
        <li>
          <div class="area">
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic06/ch06_authenticationProvider01.PNG" alt='absolute'>
            <div>
              <span>authenticationProvider 에서 사내직원 / 일반 사용자 분기 실시</span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic06/ch06_ldap01.PNG" alt='absolute'>
            <div>
              <span>LDAP 프로세스는 DB인증을 위한 패스워드 SHA512 해시화와 달리 Window LDAP 서버로 인증하기 위해서는<br>
                    평문 패스워드가 필요하기 때문에 클라이언트와 비대칭키를 이용한 RSA 암호화 값을 복호화 해준다.</span>
            </div>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic06/ch06_ldap02.PNG" alt='absolute'>
            <div>
              <span>LDAP 인증을 위한 ID / PASSWORD 입력 후 연결 진행 및 LDAP 쿼리를 수행 후 사용자 여부를 파악한다.</span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic06/ch06_createToken01.PNG" alt='absolute'>
            <div>
              <span>로그인이 정상 수행되었을때 토큰을 발급한다.<br>
                    토큰은 발급 후 사용자 테이블에 저장되며, 차후 토큰 탈취 등 상황에서 가장 마지막에 발급된 토큰만<br>
                    유효하게 사용가능하도록 upsert 된다.<br>
              </span>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div> 



