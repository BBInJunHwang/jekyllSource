---
layout: post
current: post
cover:  assets/images/businessLogic/2022-08-22-business-01_basic.jpg
navigation: True
title: 발주 프로세스(3)
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
      <h2 class="title">[발주 프로세스] 환불 설계</h2><br>
    </header>
    <div>
      <h3 class="subTitle">프로세스 고려사항</h3>
      <p>1. 상품상태 확인</p>
      <p>-> 주문확정 / 배송중 분기</p>
      <p>-> 주문확정 : 물류 취소 후 결제 취소 </p>
      <p>-> 배송중 : 결제만 취소</p>
      <p>2. 환불타입</p>
      <p>-> 전체 환불 : 모든 상품 환불</p>
      <p>-> 부분환불 : 일부 상품 환불 </p>
    </div>
    <div class="listWrapper">
      <span style="font-size: 20px;"></span>
      <ul class="imageList">
        <li>
          <div class="area">
          <span>환불 구성도</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic04/ch04_refund01.PNG" alt='absolute'>
            <div>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
          <span>상품상태 확인</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic04/ch04_refund02.PNG" alt='absolute'>
            <div>
                <span>1. 상품상태가 주문확정인지 배송중인지 확인한다.<br>
                      2. 주문확정 시 물류취소를 선행한다.<br>
                </span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
          <span>환불타입 확인</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic04/ch04_refund03.PNG" alt='absolute'>
            <div>
                <span>1. 전체환불 / 부분환불 확인한다.<br>
                      2. 부분환불 
                      -> 결제 기록과 대조 후 부분환불 상품목록과 가격을 비교한다.<br>
                      -> 이미 취소된 상품인지, 환불금액이 일치하는지, 환불 누적금액과 결제금액 비교<br>
                      3. 전체환불
                      </span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
          <span>환불 결과</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic04/ch04_refund04.PNG" alt='absolute'>
            <div>
                <span>1. 토스 모듈을 이용한 환불 실시<br>
                      2. DB처리
                </span>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div> 



