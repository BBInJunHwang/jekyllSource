---
layout: post
current: post
cover:  assets/images/springBoot/2022-07-11-springBoot-01_basic.jpg
navigation: True
title: springBoot 시작하기(1)
date: 2022-07-11 13:00:00 +0900
tags: [springBoot]  
# tags.yml 선언한 값
class: post-template
subclass: 'post tag-springBoot'
author: BBInJunHwang
---

{% include table-of-contents_springBoot.html %}
<!-- <div>
<br>
<h2>[스프링부트] yml 설정파일 </h2><br>


<p align = "justify">
<font size=3>
스프링 프레임워크에서 사용했던 xml 파일과 같이 
.yml 혹은 .properties 확장자를 설정파일로 사용한다. 
프로젝트 진입전에 .yml 파일을 읽고 시작한다.

.properties 파일은 자동완성은 지원하지만 비슷한 부분은 계속 선언 해줘야한다.

비해 .yml 파일은 가독성이 좋으며, 중복 코드 제거 가능하다. 사용방법은 아래와 같이
key :  공백 두번 필요하다.

서버 설정으로 포트, 인코딩 등 가능하며
prefix suffix 설정 및 데이터 소스 설정
JPA, Spring security 등 여러가지 설정이 가능하다.

특히 jpa 설정에서는 ddl-auto create/update 가있으며, create 는 조심해야한다.
서버 시작 시 기존 drop 후 create 


<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/springBoot/springBoot01/ch01_yml_01.PNG" | relative_url }}' alt='absolute'>

</font>
</p>
</div> -->


<div>
    <header>
      <h2 class="title">[스프링부트] yml 설정파일</h2><br>
    </header>
    <div>
      <!-- <h3 class="subTitle"></h3>
      <p> ->  </p> -->
    </div>
    <div class="listWrapper">
      <!-- <span style="font-size: 20px;"></span> -->
      <ul class="imageList">
        <li>
          <div class="area">
            <img data-action="zoom" src="/assets/images/springBoot/springBoot01/ch01_yml_01.PNG" alt='absolute'>
            <div>
              <span>스프링 프레임워크에서 사용했던 xml 파일과 같이 <br>
                    .yml 혹은 .properties 확장자를 설정파일로 사용한다. <br>
                    프로젝트 진입전에 .yml 파일을 읽고 시작한다.<br>
                    <br>
                    .properties 파일은 자동완성은 지원하지만 비슷한 부분은 계속 선언 해줘야한다.<br>
                    <br>
                    비해 .yml 파일은 가독성이 좋으며, 중복 코드 제거 가능하다. 사용방법은 아래와 같이<br>
                    key :  공백 두번 필요하다.<br>
                    <br>
                    서버 설정으로 포트, 인코딩 등 가능하며<br>
                    prefix suffix 설정 및 데이터 소스 설정<br>
                    JPA, Spring security 등 여러가지 설정이 가능하다.<br>
                    <br>
                    특히 jpa 설정에서는 ddl-auto create/update 가있으며, create 는 조심해야한다.<br>
                    서버 시작 시 기존 drop 후 create </span>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div> 