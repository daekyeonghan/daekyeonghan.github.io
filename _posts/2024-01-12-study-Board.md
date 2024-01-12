---
title:  "Part 3 기본적인 웹 게시물 관리"
excerpt: "코드로 배우는 스프링 웹 프로젝트"

categories:
  - Board
tags:
  - [Board]

toc: true
toc_sticky: true
 
date: 2024-01-12
last_modified_at: 2024-01-12
---

### Board
---

'코드로 배우는 스프링 웹 프로젝트'

스프링으로 웹 프로젝트에서 사용되는 게시물 관리를 만들어 봅니다.

- **Part 3 기본적인 웹 게시물 관리** 

스프링 MVC와 MyBatis를 이용해서 
- CRUD(등록,수정,삭제,조회)
- 페이징 처리
- 검색 기능
을 구현한다.

중점을 두는 부분은

- 스프링 MVC를 이용하는 웹 프로젝트 전체 구조에 대한 이해
- 개발의 각 단계에 필요한 설정 및 테스트 환경
- 기본적인 등록, 수정, 삭제, 조회, 리스트 구현
- 리스트 화면 페이징 처리
- 검색 처리와 페이지 이동 

입니다.


![20240112_141010_1](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/cd7d5682-99f2-48b9-a030-c1e4034e26f0)  

'ex02' 이름으로 Spring Legacy Project를 생성합니다.

![20240112_141010_2](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/ea59980b-6922-4404-b7ad-1323401b1b95)  
`pom.xml` 파일에 spring-tx, spring-jdbc, spring-test dependency를 추가해줍니다.

![20240112_141010_3](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/5a6e106e-cc98-46d7-a71e-e3bffa1bc6ca)  
`pom.xml` 파일에 dependency 를 추가하는 방법 중 mvn repository를 활용하면 오타없이 간편하게 입력 가능합니다.
hikariCP를 예로 들면 검색하고 상단 hikariCP를 클릭하여 들어가주고 사용하고자 하는 버전을 클릭한 뒤

![20240112_141010_4](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/03d28133-658c-45bc-9945-b38e304204d6)  


![20240112_141010_5](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/78fec8e9-3c05-4cc3-bb48-d18cf840d2c1)  
하단에 textbox 부분을 클릭하면 클립보드로 복사가 됩니다.



![20240112_141010_7](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/a167efc4-44c6-46d5-9974-06195b0870a7)  
![20240112_141010_8](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/d485f35a-d328-4e28-808a-e8e3d5fbcdb8)  
![20240112_141010_9](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/ebf8d7a5-f18e-4f31-a752-4abca64e53fe)  
테스트와 Lombok을 위해서 jUnit 버전을 변경하고, Lombok을 추가합니다.
추가한 뒤 저장하고 Progress를 확인하면 설치가 되는것을 확인 가능합니다.

![20240112_141010_6](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/f9b671f5-e79f-48a2-bbf2-24d137fac06b)  
`pom.xml`파일의 설정이 끝났으면 프로젝트를 선택하고 우 클릭 Maven > Update Project를 실행합니다.

![20240112_141010_10](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/e7623ce9-d5bf-46a7-af50-0bd7b8e64a0e)  

SQL Developer을 이용하여 book_ex 계정을 통해서 테이블을 생성합니다.  
게시물은 각 게시물마다 고유의 번호가 필요한데 오라클의 경우에는 sequence를 이용해서 이러한 작업들을 처리합니다.

스크립트 출력 부분을 확인하여 해당 쿼리들이 제대로 실행되었는지 확인 할 수 있습니다.  


![20240112_141010_11](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/544c7c6c-0ee5-4748-b133-4231184a0d78)  
테이블이 정상적으로 생성되었다면 여러 개의 샘플 데이터들을 추가해 줍니다.  
이런 데이터들을 더미 데이터라고도 합니다.  
게시물 번호 bno 칼럼은 매번 새로운 값이 들어가야 하므로 `seq_board.nextval`을 이용하여 추가합니다.

`writer`칼럼의 데이터들을 변경해주면서 5개의 데이터들을 추가해줬으며 커밋 버튼을 눌러 데이터베이스에 데이터들이 저장될 수 있도록 해줍니다.  

`select * from tnl_board` 쿼리를 이용하여 데이터들이 제대로 입력되었는지 확인합니다.  



![20240112_154246_13](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/b088faef-d33f-4fc3-b2cb-6c41205ac634)  

root-context.xml에 mybatis-spring 네임스페이스를 추가하고 DataSource의 설정과 MyBatis의 설정을 추가합니다.

![20240112_154246_15](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/78c99a74-b2a1-4576-8d35-3ecc6a8c9605)

![20240112_154246_14](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/27654738-a447-4084-a5fe-0fad9b3aa50c)  

Part 1 부분에서 작성했던 `DataSourceTests` 클래스와 `JDBCTests` 클래스를 test 패키지에 추가해줍니다.  


![20240112_154246_16](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/bed67df9-43c0-4fdd-805c-4a76628a7b41)

`JDBCTests` 클래스 테스트를 실행하여 정상적으로 동작하는지 확인합니다.

![20240112_154246_17](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/c896576d-289f-4253-8988-af6e8fcd6333)  
`DataSourceTests` 클래스 테스트를 실행하여 정상적으로 동작하는지 확인합니다.

![20240112_154246_18](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/842f52c8-fc7c-4a20-8bcf-f00ec6196057)  
현재 tbl_board 테이블의 구성을 기준으로 VO 클래스를 정의합니다.  

![20240112_154246_19](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/5ed5286c-0a2d-483f-ba7a-385933869de1)  
`BoardMapper` 인터페이스를 추가하고 `tbl_board` 테이블의 저장되어 있는 게시물 형식의 데이터들을 리스트 형식으로 불러오는 쿼리문을 작성해줍니다.

![20240112_154246_20](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/6e4b25e4-9152-47f1-ba33-a23a726217a7)  
작성된 `BoardMapper` 인터페이스를 테스트 할 수 있도록 테스트 환경인 `src/test/java`에 패키지를 작성하고 `BoardMapperTests` 클래스를 추가합니다.

![20240112_154246_21](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/3a4c5a54-7a16-4921-afed-7bee901602fa)
![20240112_154246_22](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/32c66be5-d636-48db-a3e4-391be463ff75)
![20240112_154246_23](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/5c2c8781-0e0b-4207-91f3-89d194784a09)
![20240112_154246_24](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/6ade5505-0c3e-46fa-a351-b1b5bdf9b9ed)
![20240112_154246_25](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/cd722087-51b3-40b9-9aaf-1db203333659)
![20240112_154246_26](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/9e86658b-f47d-43ba-b62d-9b5e9c2041e6)
![20240112_154246_27](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/4a210d70-f40a-42c2-838a-8ba2838e1a3e)
![20240112_154246_28](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/f85f1b89-a424-4410-9980-c11f0647066e)
![20240112_154246_29](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/f064f55e-93b0-4883-bba6-6cd314de5465)
![20240112_154246_30](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/cf4da852-77ab-4dde-934c-5501589cc19f)
![20240112_154246_31](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/8c7b52d6-d7e8-47b0-891f-b06f2c0ee67c)
![20240112_154246_32](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/c913d228-f751-4a59-b2e3-2ed34b082129)
![20240112_154246_33](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/8b14ef16-6d69-4de1-93e2-b698b9c19bf0)
![20240112_154246_34](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/588e12f0-54c4-4270-8341-8caec2152ceb)
![20240112_154246_35](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/68afb5db-7279-4ca4-ad17-ae44a6d54de1)
![20240112_154246_36](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/18788248-7e49-4b72-8f3a-dcbf0d0e8cad)
![20240112_154246_37](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/e5b4061c-6a1b-4ffa-9cfa-4ef26513934b)
![20240112_154246_38](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/403611c6-330b-4077-84ec-b0fe8d7fff2b)
![20240112_154246_39](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/3cbc0ce8-b29e-46b3-add3-b6979b11f330)
![20240112_154246_40](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/81ba6461-47ba-4a40-8604-9e23e4dec27e)
![20240112_154246_41](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/89caef96-3b26-4e00-b079-b6e10459c3e1)
