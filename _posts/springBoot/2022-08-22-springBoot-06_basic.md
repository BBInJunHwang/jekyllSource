---
layout: post
current: post
cover:  assets/images/springBoot/2022-07-11-springBoot-01_basic.jpg
navigation: True
title: springBoot JPA 전략(1)
date: 2022-08-22 13:00:00 +0900
tags: [springBoot]  
# tags.yml 선언한 값
class: post-template
subclass: 'post tag-springBoot'
author: BBInJunHwang
---

{% include table-of-contents_springBoot.html %}
<div>
<br>
<h2>[스프링부트] JPA 전략 </h2><br>

<p align = "justify">
<font size=3>
<div>
   <h1>JPA OSIV 전략<br>
   jpa : open-in-view : true 시 lazy 로딩 가능 </h1>
   <p>=> 영속성을 프래젠테이션 계층까지 가져간다. </p>
   <p>=> 트랜잭션 종료 후에도 컨트롤러 세션이 close 되지 않았기 때문에 영속객체는 유지상태 가능 </p>
</div>

<div class="listWrapper">
      <ul class="imageList">
        <li>
          <div class="area">
            <div>
              <span>1. 기존방식 : 서블릿 필터부터 영속성,세션오픈, 트랜잭션 시작 (컨트롤러 시작전에 시작, 종료될때 같이 종료 connection 시간 늘어남 ) <br>
              request -> 서블릿 필터부터 영속성,JDBC, 트랜잭션 시작 -> 서비스, repository -> 컨트롤러 종료 -> 영속성,jdbc,트랜잭션 종료 <br>
             </span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <div>
              <span>
              2. 최근방식 : 세션 시작(영속성 포함) 서블릿 시작부터, 트랜잭션, jdbc 오픈은 서비스단 시작~종료까지만, 영속성은 서비스 종료 후 컨트롤러까지 살아있음(lazy 로딩 가능)<br>
              request -> 서블릿 필터부터 영속성 컨텍스트 시작 -> 컨트롤러 -> 서비스 시작 (jdbc 커넥션 + 트랜잭션 시작) -> repository 1차 캐시 조회, 데이터 없으면 DB 조회, <br>
              영속성 1차캐시 -> EAGER / LAZY 따른 다름 -> 서비스 종료 (jdbc 커넥션 + 트랜잭션 종료) -> controller 종료 시 영속성 종료   <br>
             </span>
            </div>
          </div>
        </li>
      </ul>
    </div>

JPA OSIV 전략 <br>
jpa : open-in-view : true 시 lazy 로딩 가능<br> 
=> 영속성을 프래젠테이션 계층까지 가져간다. <br>
=> 트랜잭션 종료 후에도 컨트롤러 세션이 close 되지 않았기 때문에 영속객체는 유지상태 가능 <br>
=> 만약 false 일시 영속성 유지상태는 service 단 레벨로 내려오면서 트랜잭션 종료시 같이 종료되기때문에 컨트롤러에서 lazy 로딩 불가능 <br>
(JDBC 종료시 가 아니라 서비스가 종료 시 트랜잭션을 끝내버리면 트랜젹션 범위도 줄어들고 영속성 컨텍스트도 빨리 끝나고 부하가 적어짐) <br>
<br>
1. 기존방식 : 서블릿 필터부터 영속성,세션오픈, 트랜잭션 시작 (컨트롤러 시작전에 시작, 종료될때 같이 종료 connection 시간 늘어남 ) <br>
request -> 서블릿 필터부터 영속성,JDBC, 트랜잭션 시작 -> 서비스, repository -> 컨트롤러 종료 -> 영속성,jdbc,트랜잭션 종료 <br>
<br>
2. 최근방식 : 세션 시작(영속성 포함) 서블릿 시작부터, 트랜잭션, jdbc 오픈은 서비스단 시작~종료까지만, 영속성은 서비스 종료 후 컨트롤러까지 살아있음(lazy 로딩 가능)<br>
request -> 서블릿 필터부터 영속성 컨텍스트 시작 -> 컨트롤러 -> 서비스 시작 (jdbc 커넥션 + 트랜잭션 시작) -> repository 1차 캐시 조회, 데이터 없으면 DB 조회, 영속성 1차캐시 -> <br>EAGER / LAZY 따른 다름 -> 서비스 종료 (jdbc 커넥션 + 트랜잭션 종료) -> controller 종료 시 영속성 종료 <br>
<br>
Many to one 경우 EAGER    <br>
player  /  team 관계 시 <br>
선수1 팀1	팀1 <br>
선수2 팀1    팀2 <br>
선수3 팀2 <br>
선수4 팀2 <br>
<br>
EAGER 경우 선수1 정보를 조회한다고 해도 팀1 정보도 같이 조회한다. (조인 함)<br>
=> 영속성 컨텍스트 1차 캐시 내  선수1 정보과 팀1 정보를 같이 select 한다. <br>
<br>
Many to one LAZY 전략 <br>
선수1 조회 시 1차 캐시에 팀1 정보를 안가져온다. (조인 안함)<br>
=> 만약 이때 영속성,JDBC,트랜잭션 종료 시 가져 올 수가 없다. (영속성 컨텍스트 종료로 인해 ) -> controller 단에서 팀1 조회 불가능 <br>
=> lazy 경우 팀1 proxy(가짜) 객체를 1차 캐시에 둔다 (진짜 데이터가 아님, 연결된 빈 객체임), repository에 프록시가 연결되어있음<br>
   controller 에서는 아직 영속성 컨텍스트가 살아있음 (jdbc종료,트랜잭션종료 but 영속성 종료 x)<br><br>
   이때 팀1 프록시를 호출하면 영속성 컨텍스트 내 팀1 프록시 객체가 호출 -> jdbc만 다시 연결, 트랜잭션 생성x  ->  영속성 컨텍스트에 팀1 정보 select 가 실행되며 proxy객체가 아닌 실제 정보를 가져오며 jdbc 커넥션 종료<br>
   그럼 컨트롤러시점에서 팀1 객체도 존재하게 된다. 그리고 컨트롤러 종료시 영속성 컨텍스트 종료 <br><br>
   서비스 단에서 jdbc, 트랜잭션 시작~종료 하지만, 영속성 컨텍스트는 컨트롤러 단에서 존재한다. <br>
   lazy 로딩으로 jdbc 재연결 가능 but 이때 컨트롤러단에서 영속성 컨텍스트는 살아있지만 select 정보를 변경 감지 통한 수정 불가능 (insert/update/delete 불가능함) 왜냐면 트랜잭션<br> 종료되었기 때문 <br>
<br>
<br>
요약하면 <br>
<br>
기존방식 : request 시점에서 서블릿 필터에서 영속성, jdbc, 트랜잭션 시작 -> 컨트롤러, 서비스, Repository 후 다시 컨트롤러 종료 시 -> 영속성, jdbc, 트랜잭션 종료된다 커넥션 유지기간이 길어진다<br>
<br>
요즘방식 : request 시점에서 서블릿 필터에서 영속성만 시작 -> 컨트롤러 -> 서비스 (jdbc, 트랜잭션 시작) -> Repository 후 EAGER/LAZY 따라 -> 서비스 종료 (jdbc, 트랜잭션 종료)
이때 분기<br>
1. EAGER 경우 서비스 종료 시점에서 jdbc, 트랜잭션과 함께 영속성 컨텍스트도 종료한다, Many to one 에서 한번에 join 해서 데이터를 가져와서 1차캐시에 두고 처리 <br>
2. LAZY 경우 서비스 종료 시점에서 jdbc, 트랜잭션만 종료하며, Many to one 에서 join 없이 1차캐시에 데이터를 가져온 후, proxy 빈 객체를 저장해놓고(조인 대상 데이터), 컨트롤러 시점에서 아직 영속성이 종료되지 않았기 때문에 proxy 호출 시 트랜잭션없이 jdbc만 호출해서 select 한다. (이때 트랜잭션이 없기때문에 변경 불가능)<br>
<br>
</font>
</p>
</div>



<div>
    <header>
      <h2 class="title"></h2><br>
    </header>
    <div>
      <h3 class="subTitle"></h3>
      <p> ->  </p>
    </div>
    <div class="listWrapper">
      <span style="font-size: 20px;"></span>
      <ul class="imageList">
        <li>
          <div class="area">
            <img data-action="zoom" src="" alt='absolute'>
            <div>
              <span></span>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div> 
