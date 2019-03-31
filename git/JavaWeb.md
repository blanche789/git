- 配置环境
	- Tomact:
		- 作用：
		- tomcat是一个轻量级应用服务器，是支持运行Servlet/JSP应用程序的容器，运行在jvm上，绑定IP地址并监听TCP端口。作用有：
			- 管理serverlet应用的生命周期
			- 把客户端请求的url映射到对应的serverlet
			- 与Servlet程序合作处理HTTP请求 

- servlet（service applet）
	- 服务器小程序

- doGet()
	- 重写doGet,当有人访问网页的时候,就执行doGet内的代码块
	- 网页为:localhost:8080/javaweb(项目名称)/TestServlet(地址)
- html
	- 代码实现：
	
			<!DOCTYPE html>
			<html>
			<head>
			<meta charset="UTF-8">
			<title>注册</title>
			</head>
			<body>
			 <form action="ok.jsp" method="post">  //action为连接的地址，method为调用servlet中的doPost（）
			 	userName:<input type="text" name ="userName"/>
			 	<br>
			 	 <input type="submit" value="注册"/>
			 	</form>
			</body>
			</html>
- Servlet获取表单数据(servlet class)
	- 调用HttpServletRequest对象的getParameter（）方法获取请求参数、表单数据
	- 调用HttpServletRequest对象的setCharacterEncoding（）方法设置中文字符串
	- 代码实现：
			
			package com.javaweb;
			import java.io.IOException;
			import javax.servlet.ServletException;
			import javax.servlet.annotation.WebServlet;
			import javax.servlet.http.HttpServlet;
			import javax.servlet.http.HttpServletRequest;
			import javax.servlet.http.HttpServletResponse;
			
			/**
			 * Servlet implementation class TestServlet
			 */
			@WebServlet("/Test")
			public class TestServlet extends HttpServlet {
				private static final long serialVersionUID = 1L;
			       
			    /**
			     * @see HttpServlet#HttpServlet()
			     */
			    public TestServlet() {
			        super();
			        // TODO Auto-generated constructor stub
			    }
			
				/**
				 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
				 */
				protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
						System.out.println("doGet");
						request.setCharacterEncoding("utf-8");  //doPost只识别utf-8，所以需要设置字符集
						String userName = request.getParameter("userName");
						System.out.println("userName=" + userName);
				}
			
				/**
				 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse response)
				 */
				protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
					System.out.println("doPost");
					doGet(request, response);  //doPost的方法就是调用doGet
				}
			
			}

	
- JSP获取表单数据
	- 创建JSP
	- 设置中文字符集（preference-web-jsp-utfp）
	- 通过${param.参数名} 获取参数、表单数据
	- 代码实现:
	
			 <%@ page language="java" contentType="text/html; charset=UTF-8"
			    pageEncoding="UTF-8"%>
			<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
			<html>
			<head>
			<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
			<title>Insert title here</title>
			</head>
			<body>
				<h1>ok.jsp</h1>
				${param.userName }
			</body>
			</html>