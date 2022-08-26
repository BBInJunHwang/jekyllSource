---
layout: post
current: post
cover:  assets/images/infra/2022-06-12-infra-01_basic.jpg
navigation: True
title: 로그인 구현 연동
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
      <h3 class="subTitle">프로세스 고려사항</h3>
      <p>1. 토큰 유효성 검사</p>
      <p>-> JWT 토큰이 유효한지 </p>
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
              <span>header 토큰 확인, 토큰 검증, 만료 여부, refresh 로직 등등</span>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div> 



