---
layout: post
current: post
cover:  assets/images/businessLogic/2022-08-22-business-01_basic.jpg
navigation: True
title: 발주 프로세스(2)
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
      <h2 class="title">[발주 프로세스] 로직 설계</h2><br>
    </header>
    <div>
      <h3 class="subTitle">프로세스 고려사항<br></h3>
      <p>1. 사용자 유효성 검증<br></p>
      <p>->  중지나 탈퇴 등 상태가 아닌 정상 사용자</p>
      <br>
      <p>2. 토스 페이먼츠 설정</p>
      <p>-> ISP 카드 연동위한 파라미터 세팅</p>
      <p>-> MD5 해쉬 이용한 거래 위변조 방지</p>
      <p>-> 토스에서 발급한 상점키 환경설정</p>
      <p>-> 정상일때 사용할 PAY_KEY 리디렉트</p>
      <p>-> Toss lib 모듈 연동</p>
      <p>-> DB 데이터 처리</p>
      <br>
      <p>3. SAP 연동</p>
      <p>-> 결제 전표 전송</p>
    </div>
    <div class="listWrapper">
      <span style="font-size: 20px;"></span>
      <ul class="imageList">
        <li>
          <div class="area">
          <span>발주 구성도</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic03/ch03_buy01.PNG" alt='absolute'>
            <div>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
          <span>결제 이전 프로세스</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic03/ch03_buy02.PNG" alt='absolute'>
            <div>
                <span>1. 사용자가 중지나, 탈퇴 등 비정상적인 상태인지 검증한다.<br>
                      2. 결제 트랜잭션 테이블에 데이터 처리 시작<br>
                      3. MD5 해쉬를 이용한 거래 위변조 체크를 한다<br>
                      4. 위변조 체크를 응답받은 리디렉트 컨트롤러에서 PAY_KEY를 내려 받는다<br>
                      5. 결제 트랜잭션 테이블에 PAY_KEY 업데이트<br>
                      </span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
          <span>결제 프로세스</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic03/ch03_buy03.PNG" alt='absolute'>
            <div>
                <span>1. PAY_KEY 및 금액 등 결제에 필요한 파라미터 세팅<br>
                      2. 토스 결제 모듈 호출 <br>
                      3. 결제 응답값 DB처리 -> 개인정보 등 AES 암호화 처리<br>
                      4. 결제 전표 생성<br>
                      5. EAI 와 연동한 경로에 전표 DUMP<br>
                </span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
          <span>발주 프로세스</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic03/ch03_buy04.PNG" alt='absolute'>
            <div>
                <span>1. 발주 유효성 검사<br>
                      -> 장바구니 유효성 검사 (이미 발주된건인지 확인)<br>
                      -> 상품 유효성 검사(상품 판매 중단여부, 재고 체크, 이벤트/세트상품 대상인지 등)<br>
                      -> 쿠폰 유효성 검사(쿠폰 만료여부, 쿠폰삭제여부, 기사용쿠폰 여부)<br>
                      -> 결제 번호 유효성 검사<br><br>
                      2. 발주 처리<br>
                      -> DB 처리 (장바구니 발주 완료 처리, 결제-장바구니-SAP-쿠폰 등 매핑)<br><br>
                      3. SAP 처리<br>
                      -> 발주된 상품정보 전송<br>
                  </span>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div> 



