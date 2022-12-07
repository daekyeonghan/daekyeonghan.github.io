---
title:  "MVC 패턴 - 게시판 만들기"
excerpt: "글 작성, 수정, 삭제, 조회수 등"

categories:
  - MVC
tags:
  - [MVC]

toc: true
toc_sticky: true
 
date: 2022-12-07
last_modified_at: 2022-12-07
---

### MVC 패턴으로 게시판 만들기
---

BoardDAOInterface.java 생성

인터페이스란  ?
쉽게 말해 자바 프로그래밍 언어에서 클래스가 구현해야 하는 동작을 지정할때
사용하는 추상 자료형이다.


메소드의 타입과 리턴타입, 변수타입, 이름을 미리 지정해서 실제 구현단계에서
기능을 변경할 때도 해당 규격에 맞게 만들어 유기적으로 연계되는 다른 클래스나
메소드에 영향을 주지 않도록 하는 것


### 1. BoardDAOInterface.java

---

```java
package com.multi.home.board;

import java.util.List;

public interface BoardDAOInterface {
	//게시판목록
	public List<BoardVO> boardAllSelect();

	//글내용보기- 1개 선택
	public BoardVO boardSelect(int no);

	//글쓰기(DB insert)
	public int boardInsert(BoardVO vo)

	//글수정(DB update)
	public int boardUpdate(BoardVO vo)

	//글삭제
	public int boardDelete(int no, String userid);

	//조회수
	public void hitCount(int no);

	//총 레코드 수
	public int totalRecord();

}
```

게시판 만들기 인터페이스 설정이 끝이났다.

본격적으로 게시판 만들기를 시작해보자. 먼저 게시판 글 목록 보기를 만들어보자.
urlMapping.properties 파일을 열어
`/board/boardList.do=com.multi.home.board.CommandList` 코드를 추가해준다.

boardList라는 jsp파일과 CommandList 클래스 파일이 서로 연결된다.

이제 BoardDAO.java 파일을 만든다. DB연결과 관련된 코드가 있는 DBConn.java파일을 extends하고
먼저 만들어줬던 BoardDAOInterface 파일을 implements 해준다. static 변수로 BoardDAO 메소드가
실행될 때 새로운 인스턴스가 생성될 수 있도록 먼저 코드를 작성해준다.


### 2. BoardDAO.java	(계속해서 추가됨)
- boardAllSelect() 메소드 추가 - (게시판 글 목록 조회)

---

```java
package com.multi.home.board;

import java.util.ArrayList;
import java.util.List;

import com.multi.home.DBConn;

public class BoardDAO extends DBConn implements BoardDAOInterface{
	
	protected BoardDAO() {}
	
	public static BoardDAO getInstance() {
		return new BoardDAO();
	}

	//게시판 목록 1-1
	public List<BoardVO> boardAllSelect() {
		List<BoardVO> list = new ArrayList<BoardVO>();
			
		try {
			sql = "SELECT no, subject, content, userid, hit, to_char(writedate, 'MM-DD HH:MI') writedate from board order by no desc";
			dbConn();
			pstmt = conn.prepareStatement(sql);
			rs = pstmt.executeQuery();

			while(rs.next()) {

				BoardVo vo = new BoardVO();
				
				vo.setSubject(rs.getString(1));
				vo.setContent(rs.getString(2));
				vo.setUserid(rs.getString(3));
				vo.setHit(rs.getInt(4));
				vo.setWritedate(rs.getString(5));

				list.add(vo);

			}
	
		}catch(Exception e) {
			System.out.println("게시판 글 목록 조회 예외 발생.. "+ e.getMessage());
		}finally {
			dbClose();
		}
		
		return list;
	}

```



BoardDAO.java에 게시판 글 목록 조회 쿼리문과 데이터 셋팅이 끝났으면 CommandList.java 클래스를 만들어준다

모든 Command 클래스는 또 CommandService.java 인터페이스를 상속받는다.

미리 만들어 둔 CommandService를 인터페이스로 추가하여 생성한다. 


### 3. CommandList.java 
- 게시판 글 목록 조회하는 Command 클래스

---

```java
package com.multi.home.board;

import java.io.IOException;
import java.util.List;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import com.multi.home.CommandService;

public class CommandList implements CommandService {

	@Override
	public String process(HttpServletRequest req, HttpServletResponse res) throws ServletException, IOException {
		
		BOardDAO dao = BoardDAO.getInstance();

		//BoardAllSelect()메소드를 호출하여 list에 넣어준다.
		List<BoardVO> list = dao.BoardAllSelect();
		
		//나중에 추가한 총 게시물 갯수 구하기 메소드
		int cnt = dao.totalRecord();

		//뷰 페이지에서 사용할 수 있도록 DB에서 선택한 레코드를 담아놓은
		//List컬렉션을 request에 셋팅한다
		req.setAttribute("list", list);
		req.setAttribute("totalRecord", cnt);

		return "/board/boardList.jsp";
		
	}

}
```


req.setAttribute(A,B);
A - 새로운 변수명
B - DB에서 select한 list

CommandList 메소드가 종료되면 process는 boardList.jsp로 이동한다.

boardList.jsp 파일을 만들어준다.



### 4. boardList.jsp 
- 게시판으로 들어왔을 때 보여지는 jsp파일로 DB데이터들을 어떻게 보여줄지에 대한 코드존재
---

```java
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>게시판 목록</title>
<link rel="stylesheet" href="/webMVC/css/style.css" type="text/css"/>
<style>
	.head-info>div{
		float:left;
		width:50%;
		height:50px;
		background:violet;
		line-height: 50px;
	}
	.head-info>div:last-child{
		text-align: right;
	}
	
	.board-list>li{
		float:left;
		width: 10%;
		height: 40px;
		line-height: 40px;
		border-bottom: 1px solid #ddd;
	}
	
	.board-list>li:nth-child(5n+2){
		width: 60%
	}
</style>
</head>
<body>
<div class="container">
	<h1>게시판 목록</h1>
	<div class="head-info">
		<div>총 레코드 수: ${totalRecord}개</div>
		<div>
		<c:if test="${logId != null && logId != ' ' }">
			<a href="/webMVC/board/boardWrite.do">글쓰기</a>
		</c:if>
		</div>
	</div>
	<ul class="board-list">
		<li>번호</li>
		<li>제목</li>
		<li>작성자</li>
		<li>조회수</li>
		<li>등록일</li>
		
		<c:forEach var="vo" items="${list}">
			<li>${vo.no}</li>
			<li class = "word-cut"><a href="/webMVC/board/boardView.do?no=${vo.no}">${vo.subject}</a></li>
			<li>${vo.userid}</li>
			<li>${vo.hit}</li>
			<li>${vo.writedate}</li>
		</c:forEach>
		
	</ul>
</div>
</body>
</html>
```

전체적으로 게시판 글 목록이 보여지는 스타일을 설정했다. body부분에서는 게시판 목록에 보여지는
총 게시물 갯수, 로그인이 되어있는 상태라면 '글쓰기' 버튼을 눌렀을 때 boardWrite.do로 이동이된다.
또한 반복문으로 vo에 저장되어 있는 번호, 제목, 작성자, 조회수, 등록일을 출력해주는 코드들을 작성했다.

그 전에 먼저 해당하는 게시글번호의 레코드를 선택 할 수 있는
boardSelect() 메소드를 추가해주자.

### 2-1. BoardDAO.java	(계속해서 추가됨)
- boardAllSelect() 메소드 추가 - (게시판 글 목록 조회)
- boardSelect() 메소드 추가 - (no에 해당하는 레코드를 선택하는)

---

```java
	@Override
	public BoardVO boardSelect(int no) {
		BoardVo vo = new BoardVO();
		try {
			dbConn();

			sql = "SELECT no, userid, subject, content, hit, writedate FROM board WHERE no=?";

			pstmt = conn.prepareStatement(sql);
			pstmt.setInt(1, no);
			rs = pstmt.executeQuery();

			if(rs.next()) {
				vo.setNo(rs.getInt(1));
				vo.setUserid(rs.getString(2));
				vo.setSubject(rs.getString(3));
				vo.setContent(rs.getString(4));
				vo.setHit(rs.getInt(5));
				vo.setWritedate(rs.getString(6));
			}
		}catch(Exception e) {
			System.out.println("레코드 선택 예외 발생..." + e.getMessage());
		}finally {
			dbClose();
		}
		return vo;
	}
```


이번에는 글 쓰기 기능을 구현해보자

이번에도 먼저 urlMapping.properties 파일을 열어

`/board/boardWrite.do=com.multi.home.board.CommandBoardWrite`
`/board/boardWriteOk.do=com.multi.home.board.CommandBoardWriteOk`

두줄의 코드를 추가한다 아래 코드는 로그인 된 상태로 글 제목과 내용이 입력되었다면
글을 등록하겠다는 의미를 갖고 있는 부분이다.


### 2-2. BoardDAO.java	(계속해서 추가됨)
- boardAllSelect() 메소드 추가 - (게시판 글 목록 조회)
- boardSelect() 메소드 추가 - (no에 해당하는 레코드를 선택하는)
- boardInsert() 메소드 추가 - (게시판 글 작성)
---


BoardDAO.java 클래스에 boardInsert() 메소드를 추가하였다.


	@Override
	public int boardInsert(BoardVO vo) {
		int result = 0;
		try {
			sql = "insert into board(no, userid, subject, content, ip) values(board_sq.nextval,?,?,?,?)";
			pstmt = conn.prepareStatement(sql);
			
			pstmt.setString(1, vo.getUserid());
			pstmt.setString(2, vo.getSubject());
			pstmt.setString(3, vo.getContent());
			pstmt.setString(4, vo.getIp());

			result = pstmt.executeUpdate();

		}catch(Exception e) {
			System.out.println("게시판 글쓰기 예외발생..." + e.getMessage());			
		}finally {
			dbClose();
		}
		return result;
	}

------------------------------------------------------------------------------------------------------------------
--- CommandBoardWrite.java 파일 생성 CommandService 인터페이스 추가
------------------------------------------------------------------------------------------------------------------
package com.multi.home.board;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import com.multi.home.CommandService;

public class CommandBoardWrite implements CommandService {

	@Override
	public String process(HttpServletRequest req, HttpServletResponse res) throws ServletException, IOException {
		return "/board/boardWrite.jsp";
	}

}

------------------------------------------------------------------------------------------------------------------
--- boardWrite.jsp 파일 생성
로그인이 안된상태로 글 작성을 눌렀을 경우 로그인 페이지로 이동한다.
글 제목, 내용이 입력되었는지 확인하는 스크립트 코드와 제목과 내용이 모두 입력된상태로
글 등록 버튼을 눌렀을 때 다음 경로인 boardWriteOk.jsp로 이동할 수 있도록 한다.
------------------------------------------------------------------------------------------------------------------



<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<!-- 로그인 안된경우. 로그인페이지로 보내기 -->
<c:if test="${logId==null || logId=='' }">
	<script>
	location.href="/webMVC/member/login.do";
	</script>
</c:if>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>게시판 글쓰기</title>
<link rel="stylesheet" href="/webMVC/css/style.css" type="text/css"/>
<style>
	#subject{
		width:100%;
	}
	#content{
		width:100%;
		height:200px;
	}
</style>
<script>
	function boardFormCheck(){
		//폼의 버튼 클릭하면 호출되는 함수
		var dom = document.getElementById("subject");
		if(dom.value==""){
			alert("글 제목을 입력하세요");
			dom.focus();
			return;	//함수 실행 중단. true, false 할 필요없음. (폼태그에 onsubmit없기때문에)
		}
		
		var content = document.getElementById("content");
		if(content.value==""){
			alert("글 내용을 입력하세요");
			content.focus();	//커서를 유지하고 리턴
			return;
		}
		
		//제목과 글내용이 입력된 경우
		var frm = document.getElementById("boardFrm");
		frm.action = "/webMVC/board/boardWriteOk.do";
		frm.submit();	//폼을 서브밋 발생시킴 -> action으로 접속한다.
	}
</script>
</head>
<body>
<div class="container">
	<h1>게시판 글쓰기 폼</h1>
	<form method="post" id ="boardFrm">
		<ul>
			<li>제목</li>
			<li><input type="text" name="subject" id="subject"/></li>
			<li>글내용</li>
			<li>
				<textarea name="content" id="content"></textarea>
			</li>
			<li>
				<input type="button" value="글등록" onclick="boardFormCheck()"/>
			</li>
		</ul>
	</form>
</div>
</body>
</html>


------------------------------------------------------------------------------------------------------------------
--- CommandBoardWriteOk.java 파일 생성
로그인이 되어있는 상태로 글 제목과 내용이 입력되었다.
글이 DB에 추가되고, 게시판 목록에 추가한 글이 표시되어야한다.
WriteOK는 이동되어지는 페이지로 사용자에게 보여질 화면이 없기 때문에
jsp파일은 따로 생성하지 않는다.
------------------------------------------------------------------------------------------------------------------

package com.multi.home.board;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

import com.multi.home.CommandService;

public class CommandBoardWriteOk implements CommandService {

	@Override
	public String process(HttpServletRequest req, HttpServletResponse res) throws ServletException, IOException {
		req.setCharacterEncoding("UTF-8");	//한글 인코딩
		BoardVO vo = new BoardVO();

		//폼의 제목과 글 내용을 vo에 셋팅
		vo.setSubject(req.getParameter("subject");
		vo.setContent(req.getParameter("content");
		
		//접속자 ip 셋팅
		vo.setIp(req.getRemodeAddr());

		//세션의 로그인 정보 (글 작성자)
		HttpSession session = req.getSession();
		vo.setUserid((String)session.getAttribute("logId"));

		//글 등록
		BoardDAO dao = BoardDAO.getInstance();
		int result = dao.boardInsert(vo);

		//뷰 페이지에서 result 결과를 셋팅
		req.setAttribute("result", result);

		return "/board/boardResult.jsp";
	}

}


------------------------------------------------------------------------------------------------------------------
--- boardResult.jsp 파일 생성
result 값이 0일 때는 글 등록 실패 -> 다시 글 등록페이지로 이동
result 값이 1일 때는 글 등록 성공 -> 글 목록으로 이동

------------------------------------------------------------------------------------------------------------------
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<c:if test="${result==0}">
	<!-- 글 등록실패 -->
	<script>
		alert("글 등록 실패하였습니다.");
		history.go(-1);
	</script>
</c:if>
<c:if test="${result==1}">
	<!-- 등록성공 location, sendRedirect-->
	<script>
		location.href = "/webMVC/board/boardList.do";
	</script>
</c:if>

------------------------------------------------------------------------------------------------------------------
BoardDAO.java	(계속해서 추가됨)
1 -- boardAllSelect() 메소드 추가 - (게시판 글 목록 조회)
2 -- boardSelect() 메소드 추가 - (no에 해당하는 레코드를 선택하는)
3 -- boardInsert() 메소드 추가 - (게시판 글 작성)
4 -- hitCount() 메소드 추가 - (조회수 증가)
5 -- totalRecord() 메소드 추가 - (총 게시물의 갯수)

게시글을 열람 했을 때 조회수가 증가되며, 게시글을 새로 작성하거나 삭제했을 때 총 게시글의 갯수를 구해서
게시글 목록, 게시글 조회 때 출력된다.
------------------------------------------------------------------------------------------------------------------
	//조회수 증가	
	@Override
	public void hitCount(int no) {
		try {
			dbConn();
			sql = "update board set hit=hit+1 where no=?";
			pstmt = conn.prepareStatement(sql);
			pstmt.setInt(1, no);
			pstmt.executeUpdate();
		}catch(Exception e) {
			System.out.println("조회수 증가 예외발생..." + e.getMessage());
		}finally {
			dbClose();
		}
		
	}

	//총 레코드 수
	@Override
	public int totalRecord() {
		int totalRecord = 0;
		
		try {
			sql = "select count(no) cnt from board";
			
			dbConn();
			
			pstmt = conn.prepareStatement(sql);
			
			rs = pstmt.executeQuery();
			
			if(rs.next()) {
				
				totalRecord = rs.getInt(1);
			}
		}catch(Exception e) {
			System.out.println("총 레코드 조회 에러 발생..." + e.getMessage());
		}finally {
			dbClose();
		}
		return totalRecord;
	}

}



------------------------------------------------------------------------------------------------------------------
--- CommandBoardView.java 파일 생성
게시글 목록에서 글 제목을 눌렀을 때 글 내용이 보여져야 한다.
글 제목을 눌렀을 때 조회수가 증가되고, 해당하는 번호의 게시글 DB 정보가 넘어온다.
그 다음 boardView.jsp 파일로 이동된다.

urlMapping.properties 파일을 열어

`/board/boardView.do=com.multi.home.board.CommandBoardView`

를 추가해준다.


------------------------------------------------------------------------------------------------------------------

/board/boardView.do=com.multi.home.board.CommandBoardView

package com.multi.home.board;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import com.multi.home.CommandService;

public class CommandBoardView implements CommandService {

	@Override
	public String process(HttpServletRequest req, HttpServletResponse res) throws ServletException, IOException {
		int no = Integer.parseInt(req.getParameter("no"));
		
		BoardDAO dao = BoardDAO.getInstance();
		
		//조회수 증가
		dao.hitCount(no);
		
		//레코드 선택
		BoardVO vo = dao.boardSelect(no);
		
		req.setAttribute("vo", vo);
		
		return "/board/boardView.jsp";
	}

}

------------------------------------------------------------------------------------------------------------------
--- boardView.jsp 파일 생성
글 제목을 눌렀을 때 보여지는 화면의 코드이다. 
로그인된 ID와 글 작성자가 일치하여야만 수정, 삭제 버튼이 노출된다.

------------------------------------------------------------------------------------------------------------------

<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>글 내용보기</title>
<link rel="stylesheet" href="/webMVC/css/style.css" type="text/css"/>
</head>
<body>
<div class="container">
	<h1>글 내용보기</h1>
	<ul>
		<li>번호</li>
		<li>${vo.no}</li>
		<li>작성자</li>
		<li>${vo.userid}</li>
		<li>조회수</li>
		<li>${vo.hit }</li>
		<li>등록일</li>
		<li>${vo.writedate }</li>
		<li>제목</li>
		<li>${vo.subject }</li>
		<li>글내용</li>
		<li>${vo.content }</li>
	</ul>
	<div>
		<c:if test="${logId==vo.userid }">
			수정
			삭제
		</c:if>
	</div>
</div>

</body>
</html>