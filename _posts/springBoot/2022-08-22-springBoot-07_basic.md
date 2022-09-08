---
layout: post
current: post
cover:  assets/images/springBoot/2022-07-11-springBoot-01_basic.jpg
navigation: True
title: springBoot My Project(1)
date: 2022-08-22 13:00:00 +0900
tags: [springBoot]  
# tags.yml 선언한 값
class: post-template
subclass: 'post tag-springBoot'
author: BBInJunHwang
---

{% include table-of-contents_springBoot.html %}
<div>
    <header>
      <h2 class="title">My Project(1) Entity 설계</h2><br>
    </header>
    <div>
      <h3 class="subTitle">Entity 설계</h3>
      <p> -> Entity란 DB와 매칭될 클래스  </p>
      <p> -> DB에는 객체를 저장 할 수 없기 떄문에 id 등 key값을 이용하지만 ORM 관점에서는<br>
             객체를 넣으며 JPA를 통해서 OOP(객체) 와 DB의 불일치성을 해결가능하다 (자동으로 FK 생성)  </p>
    </div>
    <div class="listWrapper">
      <span style="font-size: 20px;">OOP점 관점으로 먼저 클래스를 만들어서 DB설계를 진행한다.</span>
      <ul class="imageList">
        <li>
          <div class="area">
            <div>
              <span>
                DB 기준에서는 User 내 teamId로 Team을 조회 할 수 있으며, <br>
                Team 역시 teamId로 User를 조회 할수 있다. 서로가 서로 조회 되는 양방향 관계 <br><br>
                하지만 객체관점에서는 DB 테이블 처럼 무조건 양방향일 필요가 없으며, <br>
                User N : Team 1 관계이다. <br>
                외래키는 N 쪽인 User에 둔다. (teamId)<br>
                <br>
                연관관계의 주인은 외래 키가 있는 곳!<br>
                주인은 mappedBy 속성을 사용하지 않는다.<br>
                항상 '다(N)'쪽이 외래 키를 가진다.<br>
                @ManyToOne은 항상 연관관계의 주인이 됨. mappedBy 속성이 없다.   <br>
                <br>
                @ManyToOne(fetch = FetchType.LAZY) <br> 
                -> ManyToOne 관계로 UserInfo가 다 쪽이며, TeamInfo 에서는 참조하지 않는다 (단방향) <br>
                <br>
                EAGER 전략과 LAZY 전략 2개가 있으며,<br>
                EAGER 전략은 연관관계 있는 Entity를 조인해서 무조건 들고온다<br>
                LAZY  전략은 연관관계 있는 Entity를 가져오지 않고 getter 등으로 접근시에 가져완다<br>
                <br>
                @JoinColumn(name="컬럼명") 으로 Fk를 지정한다. <br>
                @JoinColumn(name="teamId")<br>
                private TeamInfo teamInfo;<br>
              </span>
            </div>
            <img data-action="zoom" src="/assets/images/springBoot/springBoot07/ch07_JPA_UserInfo01.PNG" alt='absolute'>
            <div>
              <span>
              @NoArgsConstructor <br>
              -> 기본 생성자 생성 <br><br>
              @AllArgsConstructor<br>
              -> 전체 필드 생성자 생성<br><br>
              @Builder <br>
              -> 빌더 패턴을 사용한다 (데이터 순서에 상관없이 객체 생성가능, setter 메서드 없음 변경불가, 이해쉬움)<br><br>
              @Entity <br>
              -> 해당 클래스를 Entity라고 선언, JPA에서 관리, 테이블 매핑<br><br>
              @Getter<br>
              -> 롬복에서 지원하는 get메서드 생성<br>
              -> Entity는 setter 생성하면 안된다 (객체의 값 변경으로 인한 일관성 보장x)<br><br>
              @DynamicInsert<br>
              -> 기본적으로 hibernate에서는 insert/update 시 모든 컬럼을 사용하며<br>
                 insert 시 null이 아닌 필드만 포함시킨다<br><br>
              @DynamicUpdate<br>
              -> 기본적으로 hibernate에서는 insert/update 시 모든 컬럼을 사용하며<br>
                 update 시 null이 아닌 필드만 포함시킨다<br><br>
              @Where(clause = "delYn = 'N'")<br>
              -> 쿼리 실행시 일괄적으로 where delYn ='N' 조건문 추가 <br>
                 논리적 삭제로 인한 삭제 플래그 적용<br><br>
              @SQLDelete(sql ="UPDATE USERINFO SET DELYN = 'Y' WHERE USERID = ?")<br>
              -> JpaRepository delete() 실행시 delete 문구가 아닌 update 삭제플래그 처리를 위함<br>
              </span>
            </div>
          </div>
        </li>
         <li>
          <div class="area">
            <img data-action="zoom" src="/assets/images/springBoot/springBoot07/ch07_JPA_TeamInfo01.PNG" alt='absolute'>
            <div>
              <span>TeamInfo Entity로서 TeamId로 UserInfo Entity와 관계가 형성이 된다.</span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <img data-action="zoom" src="/assets/images/springBoot/springBoot07/ch07_JPA_CommonEntity.PNG" alt='absolute'>
            <div>
              <span>
              @MappedSuperclass<br>
              -> 생성ID, 생성시간, 수정ID, 수정시간등 여러 Entity에서 공통적으로 사용하는 부분을 따로 뺸 클래스로서<br>
              객체의 입장에서 공통 매핑 정보가 필요할 때 사용한다<br>
              DB 테이블과는 상관없으며, 각 테이블마다 따로 사용한다.<br><br>
              @EntityListeners(AuditingEntityListener.class)<br>
              -> Entity 를 DB에 적용하기 전/후에 커스텀 콜백을 요청<br>
              영속성 컨텍스트 저장 후  Auditing 기능으로 인해서 트랜잭션 커밋 시점에 플러시가 호출할 때 <br>
              하이버네이트가 자동으로 시간 값을 채워준다. <br><br>
              </span>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div> 



