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
<br>
<h2>[스프링] on premise -> CDN migration</h2><br>

기존 온 프레미스 환경내 구축되어있던 서비스 AWS 마이그레이션 실시 

변경사항 

1. 파일 업로드<br>
AS-IS <br>
기존 웹 서버 + window 서버용 CDN dll 파일 통한 파일 업로드<br> 
TO-BE<br> 
FTP 업로드 + S3 업로드 <br>

+ 고려사항<br>
1. 기존 CDN dll 파일 제거 및 window 서버용 로직 제거 <br>
2. 영상 업로드, PDF 업로드 분리 및 PDF -> 이미지 변환<br>


영상인경우 <br>
웹 서버 업로드 대체 s3 putObject 메서드 구현<br>
<img data-action="zoom" src='{{ "/assets/images/businessLogic/businessLogic01/ch01_s3_upload_class01.PNG" | relative_url }}' alt='absolute'>


CDN 직접 영상 파일 업로드를 위한 FTP 업로드 로직 구현 
<img data-action="zoom" src='{{ "/assets/images/businessLogic/businessLogic01/ch01_ftp_upload_class01.PNG" | relative_url }}' alt='absolute'>


PDF 경우 <br>
웹 서버 업로드 대체 s3 pubOjbect 이미지 메서드 구현<br>
<img data-action="zoom" src='{{ "/assets/images/businessLogic/businessLogic01/ch01_s3_upload_class02.PNG" | relative_url }}' alt='absolute'>

PDF -> IMG 변경 위한 메서드 구현<br>
<img data-action="zoom" src='{{ "/assets/images/businessLogic/businessLogic01/ch01_pdf_convert_class01.PNG" | relative_url }}' alt='absolute'>

pdfbox.lib 에서 제공하는 PDFImageWriter.class 내 writeImage 이미지는 <br>
단순히 IO를 통해 읽은 이미지를 서버내 특정경로에 저장만 시키기 때문에 <br>
읽은 후  s3 업로드를 위해서는 재정의가 필요하다<br>
IO 작업 후 s3 업로드 로직 추가<br>
<img data-action="zoom" src='{{ "/assets/images/businessLogic/businessLogic01/ch01_pdf_convert_class02.PNG" | relative_url }}' alt='absolute'>

정상적으로 PDF 파일 장수만큼 이미지 파일로 변경완료<br>
<img data-action="zoom" src='{{ "/assets/images/businessLogic/businessLogic01/ch01_pdf_convert_result01.PNG" | relative_url }}' alt='absolute'>

최종적으로 사용자에게 보여주기 위한 pre-signedUrl 생성<br>
<img data-action="zoom" src='{{ "/assets/images/businessLogic/businessLogic01/ch01_signedUrl_class01.PNG" | relative_url }}' alt='absolute'>




