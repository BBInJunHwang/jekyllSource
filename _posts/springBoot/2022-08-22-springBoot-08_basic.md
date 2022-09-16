---
layout: post
current: post
cover:  assets/images/springBoot/2022-07-11-springBoot-01_basic.jpg
navigation: True
title: springBoot My Project(2)
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
      <h2 class="title">My Project(2) SELECT TEST</h2><br>
    </header>
    <div>
      <h3 class="subTitle">스프링 부트 테스트</h3>
      <p> -> Junit 이란 단위 테스트 프레임워크  </p>
    </div>
    <div class="listWrapper">
      <ul class="imageList">
        <li>
          <div class="area">
            <div>
             <img data-action="zoom" src="/assets/images/springBoot/springBoot08/ch08_selectTest01.PNG" alt='absolute'>
              <span>
              @ExtendWith(SpringExtension.class) <br>
              -> Spring TestContext Framework를 Junit5에 포함<br>
              <br>
              @DataJpaTest<br>
              -> JPA 관련 테스트 설정만 로드, DataSource의 설정이 정상적인지, JPA를 사용하여 데이터를 제대로 생성, 수정, 삭제하는지 등의 테스트가 가능<br>
                 @Transactional 어노테이션을 포함, 테스트가 완료되면 자동으로 롤백
              <br>
                 JPA 영속성 컨텍스트의 쿼리 실행 방식<br>
                 영속성 컨텍스트는 flush()가 실행되기 전까지 실행될 쿼리를 가지고 있다가 한번에 쿼리를 실행하도록 설계<br>
                 flush()가 실행되기 전까지 쿼리가 실행되지 않는다는 것은 @Transactional안에서 Rollback이 되어야 하는 상황이라면<br> 
                 애초에 쿼리가 실행조차 되지 않는다.<br>
                 <br>
              JUnit에서의 @Transactional Test가 실행된다면 SELECT를 제외한 모든 쿼리는 Rollback 대상<br>
              <br>
              @Rollback(false)<br>
              -> 테스트 코드에서 자동으로 설정되는 Rollback의 실행을 강제로 설정<br>
              -> insert / update 정상 수행 <br>
              <br>
              @AutoConfigureTestDatabase(replace = Replace.NONE)<br>
              -> 기본 Junit에서 실행 시 in-memory H2 DB를 사용한다. 기본이 ANY<br>
              -> NONE을 넣게되면 프로퍼티에 설정된 DB 연결정보 사용<br>
              <br><br>
              </span>
              <img data-action="zoom" src="/assets/images/springBoot/springBoot08/ch08_selectTestlogEager.PNG" alt='absolute'>
              <span>
                EAGER 전략을 실시하면, <br>
              </span>
              <img data-action="zoom" src="/assets/images/springBoot/springBoot08/ch08_selectTestlogLAZY.PNG" alt='absolute'>
              <span>
                DB 기준에서는 User 내 teamId로 Team을 조회 할 수 있으며, <br>
              </span>
            </div>
          </li>
      </ul>
    </div>
  </div> 



