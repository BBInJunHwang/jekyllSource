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

{% include table-of-contents_springBoot.html %}
<!-- <div>
<br>
<h2>[스프링부트] model </h2><br>


<p align = "justify">
<font size=3>
@Data - getter / setter을 자동으로 완성
@getter, @setter 로 개별로 설정도 가능하다.

@NoArgsConstructor - 빈생성자 자동 완성<br>
@AllArgsConstructor - 전체 생성자 자동 완성<br>
@Builder - 빌더 패턴 적용<br>
@Entity - 해당 클래스 (UserTB)가 서비스 실행 시 DB 테이블 생성된다.<br>
@DynamicInsert - insert 시 null 필드 제외한다.<br>


등 @ 어노테이션을 이용한 여러가지 설정을 편하게 할 수 있다.

@GeneratedValue(strategy = GenerationType.IDENTITY) 
프로젝트에 연결된 DB의 넘버링 전략을 따라간다 (시퀀스 사용)

@ID - pk 적용한다.
@Column(nullable = true/false , length = 숫자) - null 여부 및 사이즈 설정 가능하다.

@Enumerated(EnumType.STRING) - Enum 사용시 DB는 Enum 타입이 없기 때문에 해당 타입이 String 이라고 알려준다.

@CreationTimestamp - 현재 시간 입력한다.

<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/springBoot/springBoot02/ch02_model_01.PNG" | relative_url }}' alt='absolute'>


@Lob - 대용량 데이터 설정
@ColumDefault("'문자'") - ""안에 숫자면 그대로, 문자면 ''감싸서 default 값 적용가능

@ManyToOne(fetch = FethchType.EAGER) - 반드시 찾는다.
@JoinColumn(name="필드명") - 선언된 필드(모델 테이블 클래스)와 
name으로 선언된 필드를 FK로 설정한다. (자동생성)
예시로 사용자 1명은 여러개 게시글을 작성 가능하다.


 @OneToMany(mappedBy = "필드명") - 예시로 게시글 1개에는 여러개 답글을 달 수 있다. mappedBy는 FK 생성이 아닌 단순 조인을 위한 필드 일뿐이다. 



<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/springBoot/springBoot02/ch02_model_02.PNG" | relative_url }}' alt='absolute'>

</font>
</p>
</div> -->




<div>
    <header>
      <h2 class="title">[스프링부트] model</h2><br>
    </header>
    <!-- <div>
      <h3 class="subTitle"></h3>
      <p> ->  </p>
    </div> -->
    <div class="listWrapper">
      <!-- <span style="font-size: 20px;"></span> -->
      <ul class="imageList">
        <li>
          <div class="area">
            <img data-action="zoom" src="/assets/images/springBoot/springBoot02/ch02_model_01.PNG" alt='absolute'>
            <div>
              <span>@Data - getter / setter을 자동으로 완성<br>
                    @getter, @setter 로 개별로 설정도 가능하다.<br>
                    <br>
                    @NoArgsConstructor - 빈생성자 자동 완성<br>
                    @AllArgsConstructor - 전체 생성자 자동 완성<br>
                    @Builder - 빌더 패턴 적용<br>
                    @Entity - 해당 클래스 (UserTB)가 서비스 실행 시 DB 테이블 생성된다.<br>
                    @DynamicInsert - insert 시 null 필드 제외한다.<br>
                    <br>
                    등 @ 어노테이션을 이용한 여러가지 설정을 편하게 할 수 있다.<br>
                    <br>
                    @GeneratedValue(strategy = GenerationType.IDENTITY) <br>
                    프로젝트에 연결된 DB의 넘버링 전략을 따라간다 (시퀀스 사용)<br>
                    <br>
                    @ID - pk 적용한다.<br>
                    @Column(nullable = true/false , length = 숫자) - null 여부 및 사이즈 설정 가능하다.<br>
                    <br>
                    @Enumerated(EnumType.STRING) - Enum 사용시 DB는 Enum 타입이 없기 때문에 해당 타입이 String 이라고 알려준다.<br>
                    <br>
                    @CreationTimestamp - 현재 시간 입력한다.</span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <img data-action="zoom" src="/assets/images/springBoot/springBoot02/ch02_model_02.PNG" alt='absolute'>
            <div>
              <span>@Lob - 대용량 데이터 설정<br>
                    @ColumDefault("'문자'") - ""안에 숫자면 그대로, 문자면 ''감싸서 default 값 적용가능<br>
                    <br>
                    @ManyToOne(fetch = FethchType.EAGER) - 반드시 찾는다.<br>
                    @JoinColumn(name="필드명") - 선언된 필드(모델 테이블 클래스)와 <br>
                    name으로 선언된 필드를 FK로 설정한다. (자동생성)<br>
                    예시로 사용자 1명은 여러개 게시글을 작성 가능하다.<br>
                    <br>
                    <br>
                    @OneToMany(mappedBy = "필드명") - 예시로 게시글 1개에는 여러개 답글을 달 수 있다. mappedBy는 FK 생성이 아닌 단순 조인을 위한 필드 일뿐이다. </span>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div> 