---
layout: post
current: post
cover:  assets/images/springBoot/2022-07-11-springBoot-01_basic.jpg
navigation: True
title: springBoot 시작하기(2)
date: 2022-07-11 13:00:00 +0900
tags: [springBoot]  
# tags.yml 선언한 값
class: post-template
subclass: 'post tag-springBoot'
author: BBInJunHwang
---

{% include springBoot-table-of-contents.html %}
<br>
<h2>[스프링부트] model </h2><br>



@Data - getter / setter을 자동으로 완성
@getter, @setter 로 개별로 설정도 가능하다.

@NoArgsConstructor - 빈생성자 자동 완성
@AllArgsConstructor - 전체 생성자 자동 완성
@Builder - 빌더 패턴 적용
@Entity - 해당 클래스 (UserTB)가 서비스 실행 시 DB 테이블 생성된다.
@DynamicInsert - insert 시 null 필드 제외한다.

등 @ 어노테이션을 이용한 여러가지 설정을 편하게 할 수 있다.

@GeneratedValue(strategy = GenerationType.IDENTITY) 
프로젝트에 연결된 DB의 넘버링 전략을 따라간다 (시퀀스 사용)

@ID - pk 적용한다.
@Column(nullable = true/false , length = 숫자) - null 여부 및 사이즈 설정 가능하다.

@Enumerated(EnumType.STRING) - Enum 사용시 DB는 Enum 타입이 없기 때문에 해당 타입이 String 이라고 알려준다.

@CreationTimestamp - 현재 시간 입력한다.

<img data-action="zoom" src='{{ "/assets/images/springBoot/springBoot01/ch02_model_01.PNG" | relative_url }}' alt='absolute'>
<img data-action="zoom" src='{{ "/assets/images/springBoot/springBoot01/ch02_model_02.PNG" | relative_url }}' alt='absolute'>


