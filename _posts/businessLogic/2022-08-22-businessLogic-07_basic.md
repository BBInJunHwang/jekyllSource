---
layout: post
current: post
cover:  assets/images/businessLogic/2022-08-22-business-01_basic.jpg
navigation: True
title: 로그인 프로세스 (3)
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
      <h2 class="title">[로그인] 토큰 요청</h2><br>
    </header>
    <div>
      <h3 class="subTitle">프로세스 고려사항<br></h3>
      <p>1. 토큰 유효성 검사</p>
      <p>-> JWT 토큰이 유효한지? </p>
      <p>-> JWT 토큰이 만료되었는지? </p>
    </div>
    <div class="listWrapper">
      <span style="font-size: 20px;"></span>
      <ul class="imageList">
        <li>
          <div class="area">
            <span>jwt 요청 순서도</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic07/ch07_authenticationProcess01.PNG" alt='absolute'>
          </div>
        </li>
        <li>
          <div class="area">
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic07/ch07_tokenFilter01.PNG" alt='absolute'>
            <div>
              <span>1. requset Header 토큰 확인<br>
                    2. 토큰 내 ID 값을 이용해 유효한 사용자 체크<br>
                    3. 토큰 만료 여부 확인<br>
                    -> 만약 만료되었지만, refresh 토큰이 살아있는 경우, 토큰 재발급 실시<br>
                    4. 모든 경우 확인 후 토큰이 정상인 경우 SecurityContext에 저장<br>
                    -> 세션기반이 아니기 때문에 Controller 등에서 사용자 정보를 사용하기 위함.  </span>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div> 



