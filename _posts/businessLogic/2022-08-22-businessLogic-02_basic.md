---
layout: post
current: post
cover:  assets/images/infra/2022-06-12-infra-01_basic.jpg
navigation: True
title: Toss Payment 연동
date: 2022-06-12 03:00:00 +0900
tags: [businessLogic]  
# tags.yml 선언한 값
class: post-template
subclass: 'post tag-businessLogic'
author: BBInJunHwang
---

{% include table-of-contents_businessLogic.html %}
<br>
<h2>[스프링] Toss Payment 연동</h2><br>

Toss 결제 모듈 연동 

Toss용 lib 및 jsp 등 사용해 비지니스 설계

+ 고려사항<br>
1. 모바일에서 토스결제 모듈 연동 (간편 결제 / 키인 결제) <br>
2. 서버에서는 유효한 사용자 체크 후 결제 진행 및 DB 데이터 처리 + 전표 SAP 연동<br>
3. 모바일에서 사용자가 결제 내역 조회 가능<br>
4. 관리자에서 모든 사용자 결제 내역 조회 및 환불 (전체/부분) 기능 <br>
5. 서버에서는 관리자에서 환불 기능 API 제공 <br>

DB 설계




<img data-action="zoom" src='{{ "/assets/images/businessLogic/businessLogic01/ch01_s3_upload_class01.PNG" | relative_url }}' alt='absolute'>






