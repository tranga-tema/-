<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ page import = "java.sql.*" %>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
<%
	request.setCharacterEncoding("UTF-8");
	String memo = request.getParameter("memo");
	
	String url = "jdbc:mysql://localhost/world?characterEncoding=UTF-8&serverTimezone=UTC"; 
	String user = "root"; 
	String passwd = "0698";
	Connection con = null;
	String sql = "insert into oneline(memo) values( ? )";
	PreparedStatement pstmt =null;

	Class.forName("com.mysql.cj.jdbc.Driver");
	con = DriverManager.getConnection(url, user, passwd);

	pstmt = con.prepareStatement(sql);
	pstmt.setString(1,memo);
	pstmt.executeUpdate();
	pstmt.close();
	con.close(); 
	out.println("데이터 추가 성공");  
%>
<form method="post"action="http://localhost:8080/oneline/memo_list.jsp" >
	<input type="submit" value="list보기">
</form>
</body>
</html>