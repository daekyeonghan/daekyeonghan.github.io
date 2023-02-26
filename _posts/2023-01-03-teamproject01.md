---
title:  "반려견 미용실 예약 서비스 '이웃집 하로'"
excerpt: "프로젝트 기간 2023-01-06 ~ 2023-02-16"

categories:
  - TeamProject
tags:
  - [Team, Project]

toc: true
toc_sticky: true
 
date: 2023-02-26
last_modified_at: 2023-02-26
---

제가 직접 구현한 부분을 설명하기 위해서 만들었습니다.  
시연영상이나 시스템 구성도 등 세부내용은 프로젝트 레포지토리 리드미를 참고 부탁드립니다.  
▶[📺 이웃집하로](https://github.com/daekyeonghan/petsalon)◀  
감사합니다.
{: .text-center }

1. Shop_notice, Review_answer, Resv DB 구축 및 CRUD 설계
![image](https://user-images.githubusercontent.com/117332830/221411688-6bd578a3-da89-494c-a2b2-5cdf427b0826.png) 
Resv 예약정보 테이블 dto

![image](https://user-images.githubusercontent.com/117332830/221411726-118b918f-1ce4-4972-8240-d83e90a28530.png)
![image](https://user-images.githubusercontent.com/117332830/221411836-bed15840-65db-4a0a-a73d-cd5f1d2eb5bd.png)
Resv 예약정보 DDL & DML 구문

![image](https://user-images.githubusercontent.com/117332830/221411925-d1c6df6c-13ab-4268-997e-827f0311a2fe.png)
![image](https://user-images.githubusercontent.com/117332830/221411959-f0782b7a-bd24-4cc4-9535-69ff640c00b4.png)

Select, Select All, Insert, Update, Delete CRUD 설계

2. Daum 주소 API를 활용한 우편번호 찾기 및 주소 검색
3. Ajax를 활용한 회원가입 개별 유효성검사 후 회원가입 기능 구현
4. 예약 확정/취소 안내를 위한 이메일 전송 서비스 구현
5. 고객 이용 후기 작성, 수정, 삭제 및 후기 페이지 구현
6. 네이버 클라우드 플랫폼 ChatBot 서비스 구현
7. Ajax, 이메일 본인인증을 활용한 고객 비밀번호 재설정 구현
8. SHA-512 방식을 활용한 비밀번호 암호화
9. Img Util을 통한 이미지 업로드, 수정, 삭제 구현
