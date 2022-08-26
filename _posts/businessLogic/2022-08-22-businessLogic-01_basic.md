---
layout: post
current: post
cover:  assets/images/infra/2022-06-12-infra-01_basic.jpg
navigation: True
title: AWS MIG 구현
date: 2022-06-12 03:00:00 +0900
tags: [businessLogic]  
# tags.yml 선언한 값
class: post-template
subclass: 'post tag-businessLogic'
author: BBInJunHwang
---

{% include table-of-contents_businessLogic.html %}
<!-- <div>
<br>
<h2>[스프링] on premise -> CDN migration</h2><br>

<p align = "justify">
<font size=3>
기존 온 프레미스 환경내 구축되어있던 서비스 AWS 마이그레이션 실시<br>

<h1>변경사항</h1> <br>
파일 업로드<br>
AS-IS <br>
기존 웹 서버 + window 서버용 CDN dll 파일 통한 파일 업로드<br> 
TO-BE<br> 
FTP 업로드 + S3 업로드 <br>

+ 고려사항<br>
1. 기존 CDN dll 파일 제거 및 window 서버용 로직 제거 <br>
2. 영상 업로드, PDF 업로드 분리 및 PDF -> 이미지 변환<br>


영상인경우 <br>
웹 서버 업로드 대체 s3 putObject 메서드 구현<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/businessLogic/businessLogic01/ch01_s3_upload_class01.PNG" | relative_url }}' alt='absolute'>


CDN 직접 영상 파일 업로드를 위한 FTP 업로드 로직 구현 
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/businessLogic/businessLogic01/ch01_ftp_upload_class01.PNG" | relative_url }}' alt='absolute'>


PDF 경우 <br>
웹 서버 업로드 대체 s3 pubOjbect 이미지 메서드 구현<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/businessLogic/businessLogic01/ch01_s3_upload_class02.PNG" | relative_url }}' alt='absolute'>

PDF -> IMG 변경 위한 메서드 구현<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/businessLogic/businessLogic01/ch01_pdf_convert_class01.PNG" | relative_url }}' alt='absolute'>

pdfbox.lib 에서 제공하는 PDFImageWriter.class 내 writeImage 이미지는 <br>
단순히 IO를 통해 읽은 이미지를 서버내 특정경로에 저장만 시키기 때문에 <br>
읽은 후  s3 업로드를 위해서는 재정의가 필요하다<br>
IO 작업 후 s3 업로드 로직 추가<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/businessLogic/businessLogic01/ch01_pdf_convert_class02.PNG" | relative_url }}' alt='absolute'>

정상적으로 PDF 파일 장수만큼 이미지 파일로 변경완료<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/businessLogic/businessLogic01/ch01_pdf_convert_result01.PNG" | relative_url }}' alt='absolute'>

최종적으로 사용자에게 보여주기 위한 pre-signedUrl 생성<br>
<img style="margin-left:0; margin-bottom: 25px;border: 2px outset gray; border-radius:10px;" data-action="zoom" src='{{ "/assets/images/businessLogic/businessLogic01/ch01_signedUrl_class01.PNG" | relative_url }}' alt='absolute'>

</font>
</p>
</div> -->





<div>
    <header>
      <h2 class="title">[스프링] on premise -> CDN migration</h2><br>
    </header>
    <div>
      <h3 class="subTitle">온 프레미스 환경내 구축되어있던 서비스 AWS 마이그레이션 실시<br></h3>
      <span>변경사항<br>
            1. java6 ->8, 스프링 3 -> 4.X or 5.X 전환 필요<br>
            2. 오라클 11 -> 19 전환 필요<br>
            3. NEXUS 연동 불가로 인한 new Maven parent 필요<br>
            4. DB link 불가능으로 인한 EAI 전환 필요<br>
            5. 파일 업로드<br>
               AS-IS : 웹 서버 + window 서버용 CDN dll 파일 통한 파일 업로드<br>
               TO-BE : FTP 업로드 + S3 업로드 <br>
            6. SVN -> Git Lab 변경<br>
            7. CI/CD 구축<br>
            <br>
            + 고려사항<br>
            1. java 및 spring 변경에 따른 검토필요
            2. 오라클19에서 지원하지않는 comcat -> listagg 등 문법 변경<br>
            3. 기존 Nexus 대체할 외부 lib 연동 및 parent 구성<br>
            4. EAI 연동할 수신 테이블 설계 및 데이터 범위 지정<br>
            5. 파일업로드 시 기존 CDN dll 파일 제거 및 window 서버용 로직 제거<br>
            6. 영상 업로드, PDF 업로드 분리 및 PDF -> 이미지 변환실시<br>
            7. Git Lab 소스 push 및 브랜치 관리<br>
            8. 자동배포를 위한 파이프라인 구성<br>
            </span>
    </div>
    <div class="listWrapper">
      <!-- <span style="font-size: 20px;"></span> -->
      <ul class="imageList">
        <li>
          <div class="area">
            <span>spring 버전 변경</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_s3_upload_class01.PNG" alt='absolute'>
            <div>
              <span>스프링 버전 변경<br></span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <span>쿼리 변경</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_s3_upload_class01.PNG" alt='absolute'>
            <div>
              <span>LISTAGG 쿼리 및 literal does not match format string ora-01861 OS의 LANG 설정이 달라서 문자열을 묵시적으로 날짜로 변환을 못해서 발생하는 에러<br></span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <span>parent 신규 생성</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_s3_upload_class01.PNG" alt='absolute'>
            <div>
              <span>parent 신규 생성 및 모듈 추가<br> 외부 lib 사용할 로컬 repo 정의</span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <span>EAI 연동</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_s3_upload_class01.PNG" alt='absolute'>
            <div>
              <span>기존 DB link 사용이 불가능하기 떄문에, EAI receive 테이블 생성<br></span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <span>첨부파일 업로드 변경</span>
            <span>영상인경우</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_s3_upload_class01.PNG" alt='absolute'>
            <div>
              <span>웹 서버 업로드 대체 s3 putObject 메서드 구현<br></span>
            </div>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_ftp_upload_class01.PNG" alt='absolute'>
            <div>
              <span>CDN 직접 영상 파일 업로드를 위한 FTP 업로드 로직 구현 </span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <span>PDF 경우</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_s3_upload_class02.PNG" alt='absolute'>
            <div>
              <span>웹 서버 업로드 대체 s3 pubOjbect 이미지 메서드 구현<br></span>
            </div>
          </div>
          <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_pdf_convert_class01.PNG" alt='absolute'>
            <div>
              <span>PDF -> IMG 변경 위한 메서드 구현</span>
            </div>
          <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_pdf_convert_class02.PNG" alt='absolute'>
            <div>
              <span>pdfbox.lib 에서 제공하는 PDFImageWriter.class 내 writeImage 이미지는 <br>
                    단순히 IO를 통해 읽은 이미지를 서버내 특정경로에 저장만 시키기 때문에 <br>
                    읽은 후  s3 업로드를 위해서는 재정의가 필요하다<br>
                    IO 작업 후 s3 업로드 로직 추가</span>
            </div>
          <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_pdf_convert_result01.PNG" alt='absolute'>
            <div>
              <span>정상적으로 PDF 파일 장수만큼 이미지 파일로 변경완료</span>
            </div>
          <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_signedUrl_class01.PNG" alt='absolute'>
            <div>
              <span>최종적으로 사용자에게 보여주기 위한 pre-signedUrl 생성</span>
            </div>
        </li>
        <li>
          <div class="area">
            <span>Git Lab 관리</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_s3_upload_class01.PNG" alt='absolute'>
            <div>
              <span>svn -> git lab 업로드 및 형상관리 실시<br></span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <span>CICD 구축</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_s3_upload_class01.PNG" alt='absolute'>
            <div>
              <span>기존 DB link 사용이 불가능하기 떄문에, EAI receive 테이블 생성<br></span>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div> 