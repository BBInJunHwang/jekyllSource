---
layout: post
current: post
cover:  assets/images/businessLogic/2022-08-22-business-01_basic.jpg
navigation: True
title: 로그인 프로세스 (1)
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
      <h2 class="title">[로그인] 커스텀 필터 적용</h2><br>
    </header>
    <div>
      <h3 class="subTitle">프로세스 고려사항</h3>
      <p>request 검증</p>
      <p>-> 모든 request는 json 형태로 요청</p>
      <p>-> Client에서 ajax 요청 시 CORS 해결</p>
    </div>
    <div class="listWrapper">
      <span style="font-size: 20px;"></span>
      <ul class="imageList">
        <li>
          <div class="area">
          <span>로그인 구성도</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic05/ch05_login01.PNG" alt='absolute'>
            <div>
              <span>
              </span>
            </div>
            <span>커스텀 필터</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic05/ch05_requestFilter01.PNG" alt='absolute'>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic05/ch05_requestFilter02.PNG" alt='absolute'>
            <div>
              <span>1. requestFilter <br>
                    -> 각종 필터에서 request를 먼저 stream으로 읽었을때 필터 통과 후 컨트롤러에서 request 처리 시 null 발생<br>
                    -> 톰캣에서 한번 읽은 stream은 사용 불 가능 <br>
                    -> Wrapper 객체를 만들어서 읽은 후 다른곳에서 사용시 해당 객체를 반환
              </span>
            </div> 
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic05/ch05_jsonFilter01.PNG" alt='absolute'>
            <div>
              <span>2. JSON 유효성 필터 <br>
                    -> request가 정상적인 json 구조 요청인지 확인한다.<br>
                    -> Gson lib 이용해서 정상적으로 json 구조 생성이 되면 통과<br>
              </span>
            </div>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic05/ch05_corsFilter01.PNG" alt='absolute'>
            <div>
              <span>3. CORS 필터 <br>
                    -> 클라이언트 서버가 따로 존재하며, ajax 등 스크립트를 통해서 호출 시 CORS 발생 <br>
                    -> CORS 방지를 위한 필터 처리
              </span>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div> 



