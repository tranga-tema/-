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

	String url = "jdbc:mysql://localhost/?characterEncoding=UTF-8&serverTimezone=UTC"; 
	String user = "root"; 
	String passwd = "0698";
	Connection con = null;
	String sql = "select * from oneline";
	PreparedStatement pstmt =null;
	PreparedStatement pstmt2 =null;
	
	Class.forName("com.mysql.cj.jdbc.Driver");
	
	con = DriverManager.getConnection(url, user, passwd);
	
	pstmt2 = con.prepareStatement("use world");
	pstmt2.executeUpdate();
	pstmt2.close();
	
	pstmt = con.prepareStatement(sql);
	ResultSet rs=pstmt.executeQuery();
	while(rs.next()) {
		int no = rs.getInt(1);
		String memo = rs.getString(2);
		String wdate = rs.getString(3);
		
		out.print("일련번호"+no+ ":"+memo+":( " + wdate + " )<br>");
	
	}
	rs.close();
	pstmt.close();
	con.close(); 
	out.println("DB조회 성공");  
%>
<form method="post" action="http://localhost:8080/oneline/memo01.html">
	<button type="submit">html호출</button> 
</form>

</body>
</html>