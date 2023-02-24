게시판 - board
전자정부프레임워크 기준 작성
자바 버전 : 1.6
springframework-version : 3.1.1.RELEASE

1. pom.xml
 mysql 연동 API 추가
		<!-- 직접 추가한 내용(1) : MySQL 연동을 위함 -->
		<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
			<version>8.0.16</version>
		</dependency>
        <!-- 직접 추가한 내용(2) : MySQL 연동을 위함 -->
        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-dbcp2</artifactId>
            <version>2.4.0</version>
        </dependency>
2. web.xml
 한글 인코딩 설정 추가
	<!-- 한글 인코딩 설정 -->
	<filter>
	      <filter-name>encodingFilter</filter-name>
	     <filter-class>org.springframework.web.filter.CharacterEncodingFilter
	      </filter-class>
	      <init-param>
	           <param-name>encoding</param-name>
	           <param-value>UTF-8</param-value>
	      </init-param>
	</filter>
	<filter-mapping>
	      <filter-name>encodingFilter</filter-name>
	      <url-pattern>/*</url-pattern>
	</filter-mapping>
	
3. servlet-context.xml
 mysql DB 접속 정보 추가
 
4. HomeController.java
@Controller
public class HomeController {
	
	@RequestMapping(value = "/", method = RequestMethod.GET)
	public String home() {
		return "redirect:/board/boardList";
	}
}

5. board package 추가
 - Board.java
 - BoardController.java
 - BoardDAO.java
 
6. jsp 파일 추가
 board
 - boardInfo.jsp
 - boardList.jsp
 - boardWriteForm.jsp
 - reWriteForm.jsp
 
 게시판 완료 확인
 
 7. member package 추가
 - Member.java
 - MemberController.java
 - MemberDAO.java
 
 8. jsp 파일 추가
 member
  - index.jsp
  - joinForm.jsp
  - list.jsp
  - loginForm.jsp
  - loginPro.jsp
  - logoutPro.jsp
  - modifyForm.jsp
  - userMenu.jsp
  파일 내용 수정 중
  회원에 따른 게시글 작업 할수 있게 변경중
--------------------------------------------------
230224_01
로그인, 가입기능 추가 - 메인페이지 버튼 추가
<추가할사항>
사용자 게시글 수정, 삭제하기 기능
검색기능 - 제목검색, 날짜 검색, 작성자 검색
로그인 권한설정

1.삭제하기
BoardController
- 삭제하기 클릭시 해당 게시판 번호를 가져옴
```
@RequestMapping(value = "/board/boardDelete")
public String boardDelete(HttpServletRequest request, Model model) {
		
	int num = Integer.parseInt(request.getParameter("num"));
	dao.boardDelete(num);
		
	return "/board/boardDeletePro";
}
```
BoardDAO
- 가져온 게시판 번호를 보고 게시글 삭제
```
public void boardDelete(int num) {
	try {
		conn = dataSource.getConnection();
		String sql = "DELETE FROM board WHERE num=?";
		pstmt = conn.prepareStatement(sql);
			
		pstmt.setInt(1, num);
		pstmt.executeUpdate();
			
	}catch(Exception e) {
		e.printStackTrace();
	}finally {
		finallyClose();
	}
}
```
boardDeletePro.jsp
- 게시글 삭제 알람창후 메인페이지 이동
  
  
  
  
  
  
  
  
  
