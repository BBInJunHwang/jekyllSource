---
layout: post
current: post
cover:  assets/images/businessLogic/2022-08-22-business-01_basic.jpg
navigation: True
title: AWS Migration
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
      <h2 class="title">[스프링] On premise -> AWS migration</h2><br>
    </header>
    <div>
      <h3 class="subTitle">IDC 내 온 프레미스 환경 내 구축된 서비스 AWS 마이그레이션 실시<br><br></h3>
      <span>변경사항<br>
            1. 자바 버전 6 -> 8, 스프링 3.x -> 4.X or 5.X 전환 필요<br><br>
            2. 오라클 11 -> 19 전환 필요<br><br>
            3. NEXUS 연동 불가로 인한 new Maven parent 필요<br><br>
            4. DB link -> EAI 전환 필요<br><br>
            5. 파일 업로드 로직 변경 필요<br><br>
               AS-IS : 웹 서버 + window 서버용 CDN dll 파일 통한 파일 업로드<br>
               TO-BE : FTP 업로드 + S3 업로드 <br><br>
            6. SVN -> Git Lab 변경<br><br>
            7. CI/CD 구축<br><br>
            + 고려사항<br>
            1. 자바 및 스프링 변경에 따른 검토 필요 <br><br>
            2. 오라클 19에서 지원하지않는 문법 변경<br><br>
            3. 기존 Nexus 대체할 로컬 repo 연동 및 parent 구성<br><br>
            4. EAI 연동할 수신 테이블 설계 및 데이터 범위 지정<br><br>
            5. 파일업로드 시 기존 CDN dll 파일 제거 및 window 서버용 로직 제거<br><br>
            6. 영상 업로드, PDF 업로드 분리 및 PDF -> 이미지 변환실시<br><br>
            7. Git Lab 소스 push 및 브랜치 관리<br><br>
            8. 자동배포를 위한 파이프라인 구성<br><br>
            </span>
    </div>
    <div class="listWrapper">
      <!-- <span style="font-size: 20px;"></span> -->
      <ul class="imageList">
        <li>
          <div class="area">
            <span>1. 자바 및 스프링 버전 변경</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_spring_versionup01.PNG" alt='absolute'>
            <div>
              <span>자바 1.8 적용<br>
                  스프링 4.3 적용<br>
              </span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <span>2. 오라클 변경</span>
            <div>
              <span>WM_CONCAT -> LISTAGG 등 지원 하지 않는 쿼리 변경<br> 
                    linux 환경에서 OS의 LANG 설정이 달라서 문자열을 묵시적으로 날짜로 변환을 못해서 발생하는 에러 조치<br></span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <span>3. 로컬 repository 구성 및 parent 신규 생성</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_maven_parent01.PNG" alt='absolute'>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_maven_parent02.PNG" alt='absolute'>
            <div>
              <span>parent 신규 생성 및 연결 모듈 추가<br></span>
            </div>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_maven_local_repo01.PNG" alt='absolute'>
            <div>
              <span>로컬 repository에 정의할 lib 추가<br></span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <span>4. EAI 연동</span>
            <div>
              <span>기존 DB link 사용이 불가능하기 떄문에, Legacy 데이터를 내려 받을 receive 테이블 생성<br>
                    데이터 정보를 매핑 후 EAI 통해서 수신 실시</span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <span>5. 첨부파일 업로드 변경<br></span>
            <span>영상인경우</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_s3_upload_class01.PNG" alt='absolute'>
            <div>
              <span>S3 업로드를 위한 putObject 메서드 구현<br></span>
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
              <span>S3 업로드를 위한 pubOjbect 이미지 메서드 구현<br></span>
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
                    IO 작업 후 S3 업로드 로직 추가</span>
            </div>
          <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_pdf_convert_result01.PNG" alt='absolute'>
            <div>
              <span>PDF 파일 장 수만큼 이미지 파일로 변경완료</span>
            </div>
          <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_signedUrl_class01.PNG" alt='absolute'>
            <div>
              <span>사용자에게 보여주기 위한 pre-signedUrl 생성</span>
            </div>
        </li>
        <li>
          <div class="area">
            <span>6. GitLab 관리</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_gitlab01.PNG" alt='absolute'>
            <div>
              <span>svn -> Gitlab Push 및 PRD, STG, DEV 환경별 branch 관리 실시<br></span>
            </div>
          </div>
        </li>
        <li>
          <div class="area">
            <span>7. CI/CD 구축</span>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_aws_cicd_git01.PNG" alt='absolute'>
            <div>
              <span>Git push 시 자동으로 파이프라인이 가동될 수 있도록 연결<br></span>
            </div>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_aws_cicd_env_variable01.PNG" alt='absolute'>
            <div>
              <span>PRD, STG, DEV 환경별 스프링 프로필을 사용할 수 있도록 환경변수 적용<br></span>
            </div>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_aws_cicd_build01.PNG" alt='absolute'>
            <div>
              <span>Git push 시 자동으로 파이프라인이 가동될 수 있도록 연결<br></span>
            </div>
            <img data-action="zoom" src="/assets/images/businessLogic/businessLogic01/ch01_aws_cicd_pipeline01.PNG" alt='absolute'>
            <div>
              <span>Git push 시 자동으로 파이프라인이 가동될 수 있도록 연결<br></span>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div> 