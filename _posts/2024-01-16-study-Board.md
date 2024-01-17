---
title:  "Part 3 기본적인 웹 게시물 관리 - Chapter 09"
excerpt: "코드로 배우는 스프링 웹 프로젝트"

categories:
  - Board
tags:
  - [Board]

toc: true
toc_sticky: true
 
date: 2024-01-16
last_modified_at: 2024-01-16
---

### Board
---

- **Part 3 기본적인 웹 게시물 관리**  
Chapter 09 비즈니스 계층

고객의 요구사항을 반영하는 계층  
프레젠테이션 계층과 영속 계층의 중간 다리 역할을 하게 됩니다.  

![20240115_150229_1](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/9488d2d2-8e47-401c-9846-d6a3ead8c20f)  


![20240115_150229_2](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/9b21d19b-96fc-4511-b40b-73feaedeb4b2)  

src/main/java에 org.zerock.service 패키지를 만들고 BoardService 인터페이스와, BoardServiceImpl 클래스를 선언합니다.  

BoardService에는 순서대로 게시글 등록, 조회, 수정, 삭제, 목록 조회 기능입니다.

![20240115_150229_3](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/896d9f9a-89a7-4f06-b58c-b59a683b69b6)  

root-context.xml에 네임스페이스 탭에서 context 항목을 추가하고 
![20240115_150229_4](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/e29ddbb0-1c65-4550-b268-c4bb636c7c1a)  

조금 전 선언했던 서비스를 활용할 수 있도록 내용을 추가합니다.  

![20240115_150229_5](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/dd6e0004-c97f-41e9-8609-a4f8a26cfa27)  

BoardMapper와 BoardService, BoardServiceImpl에 대한 구조 설정이 완료되었으므로 BoardServiceTests 클래스를 작성해 테스트 작업을 진행합니다.  

![20240115_150229_6](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/185b8d3c-5701-46cd-b019-aae892d0644e)  

BoardService 객체와 데이터베이스 관련 로그가 출력되면 정상적으로 주입된 것입니다.  

-**게시글 등록**

![20240115_150229_7](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/6cfec69d-951c-4e11-a99f-06e8c7a3a7d0)

BoardServiceImpl에 register 등록 코드를 작성합니다. 

![20240115_150229_8](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/c4e4193b-1b56-4d97-9e47-a654cef783cb)  

BoardServiceTests에도 register 테스트 코드를 작성하여 실행해보면

![20240115_150229_9](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/c3ead4f1-54c6-4552-b61b-98111a2937ca)  

insertSelectKey()를 이용하여 나중에 생성된 게시물의 번호를 확인하고 그 다음번호인 13번으로 게시물이 생성된것을 확인할 수 있습니다.

-**게시물 목록 조회**

![20240115_150229_10](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/5e3218ac-7e39-4769-ae24-486648d491a0)

BoardServiceImpl에 먼저 getList 코드를 작성해주고

![20240115_150229_11](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/26aaa40e-f9fa-4bf0-8165-bce9aeaecf26)  

테스트 코드를 작성하여 실행해보면

![20240115_150229_12](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/80122fbc-acd4-479e-b00c-de0013c00c14)  

다음과 같이 현재 데이터베이스에 저장되어 있는 게시물들이 목록으로 출력되는 것을 확인할 수 있습니다.

-**게시물 조회**

![20240115_150229_13](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/c49efac6-10cb-47d6-a04a-02e6ba0a60a7)  

게시글 번호를 통해 해당 게시물을 조회할 수 있습니다.  
BoardServiceImpl에 코드를 작성하고

![20240115_150229_14](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/78677784-9092-4630-ab1d-2fab5d4ba227)  


![20240115_150229_15](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/0f54a21a-d6f8-4d24-b9a4-32710be251f7)  

테스트 코드를 작성하여 실행해보면 다음과 같이 1번의 게시물을 확인할 수 있습니다.

-**게시물 수정, 삭제**

![20240115_150229_16](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/76fec04e-8079-406f-93a4-f090223a5eb9)  

BoardServiceImpl에 수정, 삭제 코드를 작성해주고


![20240115_150229_17](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/bfd7afc7-d15b-47bc-9bfe-e9b33a5c4170)  

테스트 코드를 작성하여 실행해보면


![20240115_150229_18](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/18534761-9286-487e-8ae4-cb07ebccac7e)

2번 게시물이 삭제된 것을 확인할 수 있고 1번 게시물의 제목이 수정된것을 확인할 수 있습니다. (5번 게시물 내용 빨간 네모표시는 무시합니다.)
