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

2. 회원가입 페이지 구현

![PC 회원가입](https://user-images.githubusercontent.com/117332830/221447783-cc4f7197-b7bd-4068-8226-30e0d7e9fd11.gif)
[회원가입 시연]

2-1. Daum 주소 API를 활용한 우편번호 찾기 및 주소 검색  

![image](https://user-images.githubusercontent.com/117332830/221447986-a850c7ab-4798-4460-aac2-b6d1b3a03476.png)  
![image](https://user-images.githubusercontent.com/117332830/221447995-4b18e808-d5e5-49f8-ace4-b445f2cce0c7.png)  

2-2. Ajax를 활용한 회원가입 개별 유효성검사 후 회원가입 기능 구현  

![image](https://user-images.githubusercontent.com/117332830/221448766-e404064c-8ada-4bdc-8690-a0015e316052.png)  

![image](https://user-images.githubusercontent.com/117332830/221448797-7e22f2d7-528e-44fd-9056-44ec75370d3b.png)  
[Ajax를 활용 DB상에 존재하는 이메일인지 확인]  
이메일 형식에 맞지 않거나 중복된 이메일 즉 사용 불가능한 이메일의 경우 본인인증 버튼이 비활성화되어있고, 이메일 형식에 맞고 중복되지 않는 이메일주소라면 본인인증 버튼이 활성화됩니다.

![image](https://user-images.githubusercontent.com/117332830/221448433-99b8c121-f278-4277-9f59-0ffac8d062b6.png)  
![image](https://user-images.githubusercontent.com/117332830/221448444-b08a36e5-5dee-4bc8-9497-596315144889.png)  
![image](https://user-images.githubusercontent.com/117332830/221449372-942e2eb1-53a2-46bc-a9bf-f3b63dd8ec69.png)  
[스크립트 및 컨트롤러 코드]  
Ajax에서는 DB에 존재하는지 여부를 확인해줬고 카운팅하여 존재하면1 존재하지 않으면 0을 반환, html에 스크립트 코드에서는 컨트롤러에서 받은 값과 이메일 형식검사 정규표현식으로 판단해 사용가능한 이메일일 경우 본인인증 버튼이 활성화 됩니다.

2-3. SHA-512 방식을 활용한 비밀번호 암호화
![image](https://user-images.githubusercontent.com/117332830/221449865-95d83f7b-70b3-4d99-8b8a-c6bbd578ce23.png)
[사용자 비밀번호를 암호화하여 DB에 저장]

![image](https://user-images.githubusercontent.com/117332830/221451853-d77eb2bc-1dd5-4eb3-ac6d-d44a38127e67.png)  
[frame 패키지에 CryotiUtil]

![image](https://user-images.githubusercontent.com/117332830/221451867-00b02c92-1684-4e39-8f9d-7c0f8ac20f8a.png)  
[DB로 보내줄때 CryptoUtil에 sha512를 호출하여 적용시키는 코드]

Frame 패키지에 CryptoUtil 클래스 sha512메소드를 만들어서 RegisterController에 registerimpl안에 호출해서 사용했다. 

```java
String userpwd = user.getUserpwd(); //사용자가 입력한 비밀번호를 받아서
String enc_userpwd = CryptoUtil.sha512(userpwd); //SHA-512 방식 암호화 적용

user.setUserpwd(enc_userpwd); //암호화가 적용된 비밀번호를 set해서

service.register(user); //등록해준다
```

2-4. 비밀번호 재설정

![image](https://user-images.githubusercontent.com/117332830/221452351-f51dc166-9eb3-4f13-b689-669e3a0cbed9.png)
[비밀번호 찾기 & 재설정 폼]

![비밀번호재설정](https://user-images.githubusercontent.com/117332830/221453284-0dc0c1f0-0378-4f25-a2b9-836c6ebaf853.gif)  
[비밀번호 찾기 & 재설정 시연]

SHA (Secure Hash Algorithm, 안전한 해시 알고리즘)은 해시 함수들의 모음
SHA-512 방식은 단방향 암호화 방식으로 사용자가 비밀번호를 잃어버렸을 경우 복호화가 불가능하여 알려줄 수 없다. 따라서 본인인증을 거친 후 재설정 할 수 있도록 구현했습니다.

모달을 이용하였고 이름, 연락처, 이메일 3가지 정보가 DB에 존재하는지 또한 모든 정보가 일치하는지 확인이 되면 본인인증 버튼이 활성화 됩니다. 이메일로 인증번호를 받아서 인증이 완료되면 비밀번호 재설정 input박스가 활성화 되고 재확인을 거쳐 확인이 되면 마찬가지로 비밀번호 재설정 버튼이 활성화 됩니다.


3. 예약 확정/취소 안내를 위한 이메일 전송 서비스 구현

이메일 전송 서비스는 javax mail 을 활용하였고 회원가입 본인인증, 예약확정/취소 안내 부분에 적용되었습니다. 사용자가 예약을 접수하면 관리자 페이지에서 예약확정/취소를 할 수 있습니다. 예약확정 버튼을 누르면 예약확정 이메일이 발송되고 예약을 취소하면 취소사유 안내와 해당 예약 정보가 함께 발송되도록 구현하였습니다.

![image](https://user-images.githubusercontent.com/117332830/221453947-ba2b19b0-1d3f-4d49-b8b3-1f2b4c478a13.png)
[예약확정/취소 부분 코드]

![KakaoTalk_20230217_141745681](https://user-images.githubusercontent.com/117332830/221454132-99b63526-b541-43aa-963d-ebcdca0999ae.png)  
[예약취소 이메일]  

![KakaoTalk_20230217_141745660](https://user-images.githubusercontent.com/117332830/221454164-44037b26-79dc-4ce7-9943-2d9aa321a8a7.png)  
[예약확정 이메일]

4. 고객 이용 후기 작성, 수정, 삭제 및 후기 페이지 구현

![PC 이용후기-작성](https://user-images.githubusercontent.com/117332830/221454813-fffb5065-e794-474b-a198-0ebe3165d001.gif)  
[이용후기 작성]

![PC 이용후기-수정,삭제](https://user-images.githubusercontent.com/117332830/221454870-799fe9a5-ab03-4673-9865-0243bc0e5cec.gif)  
[이용후기 수정, 삭제]

이용후기 전체 페이지를 구현하였습니다. 이용후기는 크게 작성, 수정, 삭제로 구분할 수 있습니다.  

4.1 작성
먼저 후기를 작성하려면 그 사용자의 예약정보가 있어야합니다. 예약 페이지에서 사용자가 예약을 신청하면 그 예약 정보를 바탕으로 스케줄 정보에 저장이 됩니다.
따라서 사용자가 후기를 작성하려면 예약정보와 스케줄정보가 있어야하고 해당 예약정보로 작성된 후기가 있는지 확인을 해야됩니다. 

![image](https://user-images.githubusercontent.com/117332830/221455406-9d6abc00-401f-4698-8fae-9cfe1fca2e19.png)  
[후기 작성 버튼 활성화 스크립트 코드]  

아래 카운팅 정보들을 비교한 후 후기를 작성할 수 있는 경우라면 후기 작성 버튼이 활성화 되며 그렇지 않은 경우에는 비활성화 되어있습니다.  

![image](https://user-images.githubusercontent.com/117332830/221455696-c1a22bc5-0f90-4da9-b0ce-af9e470ba339.png)
[예약정보 카운트 쿼리]  
예약확정 여부가 1이고 현재 시간이 스케줄 정보에 등록된 이용시간이 클 경우 카운팅합니다.  

![image](https://user-images.githubusercontent.com/117332830/221455718-39b3e887-dc8d-4968-8e2a-43e842aca7e4.png)  
[후기정보 카운트 쿼리]  
사용자 이메일주소로 후기정보 테이블에 작성된 후기의 갯수를 카운팅합니다.  


![image](https://user-images.githubusercontent.com/117332830/221457663-beed2115-90b0-4e2b-82b4-5c0e938a03f2.png)  
[후기 작성 모달]  

후기 작성 버튼을 누르면 후기를 작성할 수 있는 최근 이용내역 셀렉트박스가 모달로 뜨게됩니다. 최근 이용내역을 선택 후 작성버튼을 누르면 작성폼이 나옵니다. 

![image](https://user-images.githubusercontent.com/117332830/221456498-2a462375-d16a-4843-a583-537f9b58ae29.png)  
[후기 작성 셀렉트 박스 코드]  
타임리프를 이용하여 최근 이용내역을 가져왔습니다.

글자 수 입력제한을 해서 DB에 VARCHAR로 선언한 변수의 크기를 초과할 경우 에러 발생을 대비해주었습니다. 후기 사진도 업로드 가능한데 미리보기 기능도 구현하였습니다. 사진을 넣지 않고 업로드 할 경우에는 '이웃집 하로'의 로고 사진으로 등록됩니다. 후기 작성 폼도 마찬가지로 유효성검사를 거쳐 글의 최소 최대 기준을 통과하면 등록이 가능합니다.

![image](https://user-images.githubusercontent.com/117332830/221458001-a377abd2-5db3-437c-9be1-90ed2b38b71f.png)  
![image](https://user-images.githubusercontent.com/117332830/221458169-07f7bebc-7514-476f-82e3-6ad02fd08cb5.png)  

4.1.1 이미지 업로드, 삭제 기능 구현
![image](https://user-images.githubusercontent.com/117332830/221460206-75977425-de77-49c0-a266-306e92f7d284.png)  
[후기 작성 폼 사진 input 코드]  
![image](https://user-images.githubusercontent.com/117332830/221459828-2d0c694e-c8b0-4a8c-ba96-ca2b2663cec3.png)
[이미지 업로드, 삭제 Util]

Frame 패키지에 Util.java 파일을 만들어 필요할 때 호출해서 사용해주었습니다.
UUID를 통해서 사진이 등록될 때 특정 숫자를 랜덤으로 부여해서 이미지 이름의 중복을 막아 주었습니다.
admindir, userdir 별 경로를 설정해주어 업로드 했을 경우 이상없이 사용자 페이지, 관리자 페이지에 노출되게 하였습니다. 삭제도 마찬가지입니다.

![image](https://user-images.githubusercontent.com/117332830/221460448-61f007cd-a30a-4d4c-ab95-18937f77ff3d.png)  
[ReviewController 후기 작성 코드]  

사용자가 사진을 업로드 했을 때와 사진 없이 글만 등록할 때 경우로 나누었습니다. 사진을 업로드 했을 때는 그 사진을 각각 admindir, userdir 저장해주고, 사진 없이 글만 등록했을 경우에는 로고사진의 이름을 set해주어 로고사진이 보여지게 했습니다.

![696 11-23-22-7423](https://user-images.githubusercontent.com/117332830/221462634-15688b4a-4202-4900-a793-b1a97e1e44c2.png)  
[작성된 후기 상세 페이지]  
![image](https://user-images.githubusercontent.com/117332830/221464176-4ef54b82-77a8-4625-992d-a0b08e671202.png)  
[후기 상세 페이지 코드]

타임리프를 이용하여 컨트롤러에서 모델로 넘겨받은 데이터들을 뿌려주었습니다. 가게 답변 같은 경우는 작성된 후기를 관리자가 답변을 등록할 수 있는데 등록을 한 경우에만 노출됩니다.  

![624 11-23-14-2775](https://user-images.githubusercontent.com/117332830/221464409-6fad76a6-b2b6-4ba0-b367-ce7d0ddb0764.png)  
[관리자 답변]  



**4.2 수정**  
두번째로 후기 수정입니다.  

로그인 되어 있는 이메일 정보와 후기를 작성한 이메일 정보를 비교하여 같을 경우 수정 버튼이 활성화 되며 작성한 후기를 수정할 수 있습니다.   

![777 11-23-31-0329](https://user-images.githubusercontent.com/117332830/221463227-9b621bab-1ce4-453d-b68d-35fb6c615ac1.png)  
[후기 수정 폼]  

수정을 눌러서 들어오면 후기를 삭제할 수 있고, 제목, 내용, 사진 모두 수정 가능합니다. 사진을 수정하지 않고 수정할 시 원본 그대로 업로드 되고, 수정한 경우에는 수정된 사진으로 업로드 됩니다.  

![849 11-23-38-4053](https://user-images.githubusercontent.com/117332830/221463818-a1bb889d-6cc1-4519-ab96-a9fd5d11fbfe.png)  

![903 11-23-44-4878](https://user-images.githubusercontent.com/117332830/221463857-5bf2e718-5754-490b-834d-2bd7923c708d.png)  

**4.3 삭제**
![image](https://user-images.githubusercontent.com/117332830/221465204-97b2e944-604c-453a-8a86-a6bc7b293f20.png)  
[후기 삭제 코드]  
사진을 등록하지 않았던 후기는 파일이름이 로고 사진으로 되어있기 때문에 사용자가 사진을 등록한 후기글만 deleteFile 메소드가 실행되게 하였습니다.  


**4.5 후기 메인 페이지 기능**  

**4.5.1 디자이너별 검색기능**  

![150 11-22-21-8323](https://user-images.githubusercontent.com/117332830/221465601-a558c345-5b00-4cb4-9de5-195bc3c5026d.png)  

사진들 우측 상단에 셀렉트박스를 누르면 디자이너별로 작성되어 있는 후기를 검색할 수 있어 디자이너 별로 어떤 스타일을 잘하는지 확인 할 수 있습니다.

디자이너는 10명인데 모든 디자이너가 후기가 작성되어 있지 않다면 후기가 작성되어 있는 디자이너들만 셀렉트박스에 표시되게 하였습니다.

![image](https://user-images.githubusercontent.com/117332830/221465871-9e16c247-f9d1-47ec-a7f4-f5e87d57b6bd.png)
[셀렉트박스 - 후기가 작성되어 있는 디자이너들만 표시]

![186 11-22-26-1534](https://user-images.githubusercontent.com/117332830/221465954-517954b0-48bc-490a-8546-7a432e5fe5ec.png)
[라비쌤으로 검색한 결과]

**4.5.2 스타일 랭킹, 최신 리뷰들 확인**  

![image](https://user-images.githubusercontent.com/117332830/221461194-98774f4b-9eb8-4b0f-a7c5-c17cc625179a.png)

후기 페이지에 들어오면 현재 가장 인기있는 스타일들을 확인할 수 있고, 최근 등록된 리뷰들을 볼 수 있게 하였습니다. 

```java
<div class="col-md mb-5" style="height: 600px; margin-right: 50px;">
	<div class="col" style="margin-right: 50px;">
	<h5 class="fs-4 mt-1 mb-3" style="line-height: 150%;"><b>지금 뜨고있는 이웃집하로의</br> 가장 인기있는 스타일이에요</b></h5>
	</div>
	<div id="carouselExampleDark" class="carousel slide" data-bs-ride="carousel">
	  <div class="carousel-inner" >
	    <div class="carousel-item" th:each="itemrankImage, itemrankImageStat : ${itemrank}" th:classappend="${itemrankImageStat.index} == 0 ? 'active'">
	      <img th:src="'/assets/img/'+ ${itemrankImage.item_photo}" class="img-fluid w-100 rounded" alt="..." style="min-height: 500px; max-height: 500px;">
		<div class="fs-4 text-center bg-white shadow rounded" th:text="${itemrankImage.item_name}" style="width:100%; height: 45px; padding-top: 5px; "></div>
	    </div>
	  </div>
	</div>
</div>
```  
![image](https://user-images.githubusercontent.com/117332830/221462250-6756ecba-fbcf-4d56-a204-ac4e1caf6ada.png)  
[가장 인기있는 스타일 코드]  

예약정보와 아이템정보를 Join하여 아이템 아이디를 그룹화 시켜서 카운팅 해준 뒤 내림차순 정렬하여 높은 순서부터 3개까지의 스타일을 가져와줬습니다.

```java
<div class="col-md mb-5" style="height: 600px;">
  <div class="col">
    <h5 class="fs-4 mt-3" style="line-height: 150%; margin-bottom: 40px;"><b>따끈따끈 방금 등록된 리뷰</b></h5>
  </div>
  <div id="carouselExampleDark" class="carousel slide" data-bs-ride="carousel">
    <div class="carousel-inner" >
    <div class="carousel-item" th:onclick="|location.href='@{/reviewview(no=${recentreviewImage.review_no},resv_no=${recentreviewImage.resv_no})}'|" th:each="recentreviewImage, recentreviewImageStat : ${recentreview}" th:classappend="${recentreviewImageStat.index} == 0 ? 'active'">
	<img th:src="'/assets/img/'+ ${recentreviewImage.review_photo}"  class="img-fluid w-100 rounded" id="review-img" style="min-height: 500px; max-height: 500px;">
	<div class="fs-4 text-center bg-white shadow rounded" th:text="${recentreviewImage.review_title}" id="recreview-title"></div>
      </div>
    </div>
  </div>
</div>
```  
![image](https://user-images.githubusercontent.com/117332830/221461861-adeec75a-0592-4938-a4ae-918fb7dea49c.png)  
[방금 등록된 리뷰 코드]  

부트스트랩 캐러셀을 활용하였고, 가장 최근 리뷰 작성날짜부터 3개까지의 후기 정보를 가져와줬습니다.

7. 네이버 클라우드 플랫폼 ChatBot 서비스 구현
8. Ajax, 이메일 본인인증을 활용한 고객 비밀번호 재설정 구현
9. 마이페이지 후기작성, 확인
