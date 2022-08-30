---
layout: post
current: post
cover:  assets/images/businessLogic/2022-08-22-business-01_basic.jpg
navigation: True
title: 발주 프로세스(1)
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
      <h2 class="title">[발주 프로세스] DB 설계</h2><br>
    </header>
    <div>
      <h3 class="subTitle">프로세스 고려사항</h3>
      <p>1. 상품구조</p>
      <p>-> 일반상품 </p>
      <p>-> 사은품 </p>
      <p>-> 세트상품 (일반상품 + 사은품) </p>
      <p>-> 이벤트 상품(일반상품의 할인가격) </p>
      <p>-> 세트상품과 이벤트 상품은 특정 사용자 지정 </p>
      <br>
      <p>2. 프로모션 구조</p>
      <p>-> 프로모션 대상 상품지정 </p>
      <p>-> 프로모션 제공 상품지정 </p>
      <p>-> 프로모션은 특정 사용자 지정 </p>
      <p>-> 프로모션은 개수 혹은 가격합산이 충족할때 적용</p>
      <p>-> 프로모션은 단건/누적으로 적용</p>
      <br>
      <p>3. 결제 구조</p>
      <p>-> 토스 페이먼츠 간편결제를 사용</p>
      <p>-> 결제 후 SAP으로 전표 생성 후 전달</p>
      <p>-> 전체 / 부분환불이 존재</p>
    </div>
    <div class="listWrapper">
      <span style="font-size: 20px;"></span>
      <ul class="imageList">
        <li>
          <div class="area">
          <span>DB 구성도</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic02/ch02_db_ERD01.PNG" alt='absolute'>
            <div>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
          <span>상품 구성도</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic02/ch02_product01.PNG" alt='absolute'>
            <div>
                <span>1. 브랜드 하위에 상품들이 존재하며, 브랜드 코드/상품코드가 PK로 존재<br>
                      2. 일반상품, 사은품은 단독으로 마스터 테이블이 존재<br>
                      3-1. 세트상품 key 값을 이용해 안에 포함된 일반상품/사은품을 매핑<br>
                      3-2. 세트상품 key 값을 이용해 타켓 대상 ID를 매핑<br>
                      4-1. 이벤트 상품key 값을 이용해 할인정보를 매핑<br>
                      4-2. 이벤트 상품 key 값을 이용해 타켓 대상 ID를 매핑</span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
          <span>프로모션 구성도</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic02/ch02_promotion01.PNG" alt='absolute'>
            <div>  
                <span>1. 프로모션 key 값으로 타켓 상품을 매핑<br>
                      2. 프로모션 key 값으로 증정 상품을 매핑<br>
                      3. 프로모션 key 값으로 타켓 대상 ID를 매핑<br>
                      4. 프로모션 key 값으로 적용 히스토리를 매핑<br>
                </span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
          <span>발주 구성도</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic02/ch02_buy01.PNG" alt='absolute'>
            <div>
                <span>1. 결제 트랜잭션, 결제성공/결제환불 이중으로 처리<br>
                      2. 발주이력은 장바구니,결제이력,쿠폰이력,SAP처리 등 key값으로 매핑<br>
                </span>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div> 



