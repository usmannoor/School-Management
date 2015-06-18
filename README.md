# School-Management
My First Repo

<!DOCTYPE html>
<html >
  <head>
    <meta charset="UTF-8">


    <title>Login Form</title>
    
    
    
    
        <style>
      @import url(http://fonts.googleapis.com/css?family=Exo:100,200,400);
@import url(http://fonts.googleapis.com/css?family=Source+Sans+Pro:700,400,300);

body{
	margin: 0;
	padding: 0;
	background: #fff;

	color: #fff;
	font-family: Arial;
	font-size: 12px;
}

.body{
	position: absolute;
	top: -20px;
	left: -20px;
	right: -40px;
	bottom: -40px;
	width: auto;
	height: auto;
	background-image: url(http://ginva.com/wp-content/uploads/2012/07/city-skyline-wallpapers-008.jpg);
	background-size: cover;
	-webkit-filter: blur(5px);
	z-index: 0;
}

.grad{
	position: absolute;
	top: -20px;
	left: -20px;
	right: -40px;
	bottom: -40px;
	width: auto;
	height: auto;
	background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,rgba(0,0,0,0)), color-stop(100%,rgba(0,0,0,0.65))); /* Chrome,Safari4+ */
	z-index: 1;
	opacity: 0.7;
}

.header{
	position: absolute;
	top: calc(50% - 35px);
	left: calc(50% - 255px);
	z-index: 2;
}

.header div{
	float: left;
	color: #fff;
	font-family: 'Exo', sans-serif;
	font-size: 35px;
	font-weight: 200;
}

.header div span{
	color: #5379fa !important;
}

.login{
	position: absolute;
	top: calc(50% - 75px);
	left: calc(50% - 50px);
	height: 150px;
	width: 350px;
	padding: 10px;
	z-index: 2;
}

.login input[type=text]{
	width: 250px;
	height: 30px;
	background: transparent;
	border: 1px solid rgba(255,255,255,0.6);
	border-radius: 2px;
	color: #fff;
	font-family: 'Exo', sans-serif;
	font-size: 16px;
	font-weight: 400;
	padding: 4px;
}

.login input[type=password]{
	width: 250px;
	height: 30px;
	background: transparent;
	border: 1px solid rgba(255,255,255,0.6);
	border-radius: 2px;
	color: #fff;
	font-family: 'Exo', sans-serif;
	font-size: 16px;
	font-weight: 400;
	padding: 4px;
	margin-top: 10px;
}

.login input[type=submit]{
	width: 260px;
	height: 35px;
	background: #fff;
	border: 1px solid #fff;
	cursor: pointer;
	border-radius: 2px;
	color: #a18d6c;
	font-family: 'Exo', sans-serif;
	font-size: 16px;
	font-weight: 400;
	padding: 6px;
	margin-top: 10px;
}

.login input[type=submit]:hover{
	opacity: 0.8;
}

.login input[type=submit]:active{
	opacity: 0.6;
}

.login input[type=text]:focus{
	outline: none;
	border: 1px solid rgba(255,255,255,0.9);
}

.login input[type=password]:focus{
	outline: none;
	border: 1px solid rgba(255,255,255,0.9);
}

.login input[type=submit]:focus{
	outline: none;
}

::-webkit-input-placeholder{
   color: rgba(255,255,255,0.6);
}

::-moz-input-placeholder{
   color: rgba(255,255,255,0.6);
}
    </style>

    
        <script src="js/prefixfree.min.js"></script>

    
  </head>

  <body>

    <div class="body"></div>
		<div class="grad"></div>
		<div class="header">
			<div>SMS</div>
		</div>
		<br>
		<div class="login">
                    <form METHOD=GET ACTION="teachLogin.jsp">
				<input type="text" placeholder="username" name="idteacherlogin"><br>
				<input type="password" placeholder="password" name="teacherPassword"><br>
				<input type="submit" value="Login">
                    </form>
		</div>
    <script src='http://cdnjs.cloudflare.com/ajax/libs/jquery/2.1.3/jquery.min.js'></script>

    
    
    
    
  </body>
</html>


<!DOCTYPE html>
<%@ page import="java.io.*,java.util.*,java.sql.*"%>
<%@ page import="javax.servlet.*,javax.servlet.http.*" %>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<%@ taglib uri="http://java.sun.com/jsp/jstl/sql" prefix="sql" %>
<html lang="en">
<head>
  
  <title>Welcome</title>
</head>

<body>
      <sql:setDataSource 
		var="usr"
			url="jdbc:mysql://localhost:3306/sms"
			driver="com.mysql.jdbc.Driver"
			user="root" password="root" 
		/>
		<sql:query dataSource="${usr}" var="result1" >
				select * from teacherlogin where idteacherlogin=? 
				<sql:param value="${param.idteacherlogin}"/>
		</sql:query>

		<c:forEach var="row1" items="${result1.rows}">
			<c:set var="flag1" scope="application" value="1"/>
		</c:forEach>

		<sql:query dataSource="${usr}" var="result2" >
			select * from teacherlogin where idteacherlogin=? and teacherPassword=?
			<sql:param value="${param.idteacherlogin}"/>
			<sql:param value="${param.teacherPassword}"/>
		</sql:query>

		<c:forEach var="row2" items="${result2.rows}">
		<c:set var="flag2" scope="application" value="1"/>
		</c:forEach>

			
			<c:choose>
			<c:when test="${flag2 eq 1}">
			<c:forEach var="row2" items="${result2.rows}">
		    <c:set var="flag2" scope="application" value="1"/>
			
				<h1>
					Welcome !!  ... <c:out value="${row2.idteacherlogin}"/>
                                        
			
		    </c:forEach>
			    <c:set var="flag1" scope="application" value="0"/>
				<c:set var="flag2" scope="application" value="0"/>
			
			</c:when>
			
			<c:when test="${flag1 eq 0}">
			
				<h1>
					User Not Registered ...
				</h1>
			
			
				<c:set var="user_flag" scope="application" value="0"/>
				<c:set var="flag" scope="application" value="0"/>
			</c:when>
			
			<c:otherwise>
			
				<h1>
					Invalid Password , Try Again !!!
				</h1>
			
				<c:set var="user_flag" scope="application" value="0"/>
				<c:set var="flag" scope="application" value="0"/>
			</c:otherwise>
			</c:choose>
		
</body>
</html>
