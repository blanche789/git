## MyBatis
### Eclipese使用
- Web-->dynamic web project-->target runtime(否则出现新建jsp时会报错,因为失去了相应的jar包,预编译会出错)
	- 若忘记选择target run time,那么
		- 右键项目-->build path-->configure(配置) build path-->选择libraries-->add libraries-->Server Runtime(Tomcat)

- Eclipse中的Web内容不会发布到Tomcat中,会自在自己的workplace创建一个tomcat的最简单结构,将web项目发布到里面
	- 路径
		- 盘:\eclipse\.metadata\.plugins\org.eclipse.wst.server.core\tmp0\wtpwebapps

### 命名规则:
1.  项目名:无要求,不起中文
2.   包:公司域名倒写,保证无重复
3.    持久层:dao,persist(持久),mapper(映射器)
4.     实体:entity,model,bean,javabean.**pojo**(Plain Ordinary Java Object的缩写;不含业务逻辑的java简单对象;完全POJO的系统也称为轻量级系统(lightweight);是相对于EJB而提出的概念。)
5.      业务逻辑:service,biz(商业)
6.       控制器:controller,servlet,action,web
7.        过滤器:filter
8.         异常:exception
9.          监听器:listener
10.           注释
	1.       类上和方法上使用文档注释/** */
11.             类:大驼峰
12.              方法,属性:小驼峰

### MVC开发模式
- M:model层,实体类、dao、service
- V：视图层，view
- C：控制层，controller
	 ![](https://i.imgur.com/pGHlyT5.png)
	- 项目开发顺序：
		- 先设计数据库
		- 实体类
		- 持久层
		- 业务逻辑
		- 控制器
		- 视图层 
		- Tip：开发顺序是从底层开始写，并且底层代码的复用率高，实体类贯穿所有流程

ctrl + 1 ：提示需要重写的方法；
CTRL+shift+l：xml快捷注释

B：单纯加粗
Strong：强调
效果一样



### JSP+Servlet完成查询+新增
- 源代码:

		package com.blanche.servlet;
		
		import java.io.IOException;
		
		import javax.servlet.ServletException;
		import javax.servlet.annotation.WebServlet;
		import javax.servlet.http.HttpServlet;
		import javax.servlet.http.HttpServletRequest;
		import javax.servlet.http.HttpServletResponse;
		
		import com.blanche.pojo.Flower;
		import com.blanche.service.FlowerService;
		import com.blanche.service.impl.FlowerServiceImpl;
		@WebServlet("/insert")
		public class InsertServlet extends HttpServlet{
			private FlowerService flowerService =new FlowerServiceImpl();
			@Override
			protected void service(HttpServletRequest req, HttpServletResponse res) throws ServletException, IOException {
				req.setCharacterEncoding("utf-8");  //拿文本框数据时,防止将数据插入数据库时,出现乱码
				String name = req.getParameter("name");
				String price = req.getParameter("price");
				String production = req.getParameter("production");
				Flower flower = new Flower();
				flower.setName(name);
				flower.setPrice(Double.parseDouble(price));
				flower.setProduction(production);  
				int index = flowerService.add(flower);
				if(index > 0)
					res.sendRedirect("show");  //
				else
					res.sendRedirect("add.jsp");
			}
		}

- 源代码:
		package com.blanche.servlet;
		
		import java.io.IOException;
		import java.util.List;
		
		import javax.servlet.ServletException;
		import javax.servlet.annotation.WebServlet;
		import javax.servlet.http.HttpServlet;
		import javax.servlet.http.HttpServletRequest;
		import javax.servlet.http.HttpServletResponse;
		
		import com.blanche.pojo.Flower;
		import com.blanche.service.FlowerService;
		import com.blanche.service.impl.FlowerServiceImpl;
		@WebServlet("/show")
		public class ShowServlet extends HttpServlet{
			private FlowerService flowerService = new FlowerServiceImpl();
			/*
			 * 属于doPost和doGet的结合
			 */
			@Override
			protected void service(HttpServletRequest req, HttpServletResponse res) throws ServletException, IOException {
				List<Flower> list = flowerService.show();
				req.setAttribute("list", list);  //设置作用域,将对象存储起来,在转发的时候可以使用
				req.getRequestDispatcher("index.jsp").forward(req, res);
			}
		}
		
- JSP(新增):

		<%@ page language="java" contentType="text/html; charset=UTF-8"
			pageEncoding="UTF-8"%>
		<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
		<html>
		<head>
		<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
		<title>Insert title here</title>
		<script type="text/javascript" src="js/jquery.js"></script>
		
		<script type="text/javascript">
		//页面加载完成后之心
		//相当于:window.onload=function(){}  $(document).ready(function(){});
		$(function(){
			$("form").submit(function(){
			//表单选择器
				if($(":text:eq(0)").val()==""||$(":text:eq(1)").val()==""||$(":text:eq(2)").val()==""){
					alert("请填写完整信息");
					//阻止默认行为
					return false;
				}
			});
		});
		</script>
		</head>
		
		<body>
		
		<form action="insert" method="post">
			<table>
			<!-- colspan:表示列的间距 -->
				<tr>
					<td colspan="2"
						style="text-align: center; font-size: 30px; font-weight: bold">花卉信息</td>
				</tr>
				<tr>
					<td><b>花卉名称:</b></td>
					<td><input type="text" name="name" /></td>
				</tr>
				<tr>
					<td><b>花卉价格:</b></td>
					<td><input type="text" name="price" /></td>
				</tr>
				<tr>
					<td><b>花卉产地:</b></td>
					<td><input type="text" name="production" /></td>
				</tr>
				<tr>
					<td colspan="2" align="center">
						<input  type="submit" value="提交"/>
						<input  type="reset" value="重置"/>
					</td>
				</tr>
		
			</table>
			</form>
		</body>
		</html>

- JSP(查询):

		<%@ page language="java" contentType="text/html; charset=UTF-8"
		    pageEncoding="UTF-8"%>
		   <%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
		<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
		<html>
		<head>
		<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
		<title>Insert title here</title>
		</head>
		<body>
			<table border='1'>
				<tr>
					<th>花卉编号</th>
					<th>花卉名称</th>
					<th>价格(元)</th>
					<th>原产地</th>
				</tr>
				<c:forEach items="${list }" var="flower">
					<tr>
						<td>${flower.id}</td>
						<td>${flower.name}</td>
						<td>${flower.price}</td>
						<td>${flower.production}</td>
					</tr>
				</c:forEach>
			</table>
			<a href="add.jsp">添加花卉信息</a>
		</body>
		</html>
	- Tips:
		- align：放在标签，表示内容居中，放在table表示标签居中
		- post：字节流，2GB，相对更安全，地址不显示数据，相对效率低，开发者工具也可查看数据 
		- get：字符流，2KB，相对相率高，不安全
		- res.setCharacter();将请求头设置为utf-8
		- sendRedirect,重定向,防止表单重复提交,会跳转到转发的地址,不会停留在原来的地址

### 框架是什么?
- 框架:软件的半成品,为解决问题制定的一套约束,在提供功能基础上进行扩充
- 框架中有一些不能被封装的代码(变量),需要使用者新建一个xml文件,在文件中添加变量内容
	- 需要建立特定位置和特定名称的配置文件
	- 需要使用xml解析技术和反射技术

- 常用概念:
	- 类库:提供的类的没有封装一定的逻辑
		- 举例:类库就是名言警句,写作文时引入名言警句

	- 框架:与类库相比,里面有一些约束
		- 举例:框架就是填空题

	- Tip:两者都是jar包,所谓框架就是开发人员写的许多含有逻辑的类,提高使用者的开发效率

- 常用框架整合:
	- SSM:
		- MyBatis:数据访问层框架
		- Spring(辅助功能):IoC,AOP
		- SpringMVC:对servlet封装
	- SSH(企业中比较少用):
		- Spring
		- Struct
		- Hibenate

### MyBatis简介:
- MyBatis 开源免费框架.原名叫IBatis,2010在google code,2013年迁移到github
- 作用:数据访问层框架
	- 底层是对JDBC的封装

- myBatis优点之一:
	- 使用mybatis时不需要编写实现类,只需要写需要执行的sql命令

八、环境搭建
- 导入jar
	![](https://i.imgur.com/2xj4mR9.png)

- 在src下新建全局配置文件（编写JDBC四个变量）
	- 没有名称和地址要求
	- 再全局配置文件中引入DTD或schema
		- 如果导入dtd后没提示
		- Window-->preference-->XML-->XMlcatalog-->add 按钮
![](https://i.imgur.com/J1Q0YH0.png)

	- 全局配置文件内容

			<?xml version="1.0" encoding="UTF-8"?>
			<!DOCTYPE configuration
			  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
			  "http://mybatis.org/dtd/mybatis-3-config.dtd">
			<configuration>
				<!-- default引用environment的id,当前所使用的环境 -->
				<environments default="default">
					<environment id="default">
						<!-- JDBC原生事务类型 -->
						<transactionManager type="JDBC"></transactionManager>
						<dataSource type="POOLED">
							<property name="driver" value="com.mysql.cj.jdbc.Driver"/>
							<property name="url" value="jdbc:mysql://localhost:3306/flower?serverTimezone=UTC"/>
							<property name="username" value="root"/>
							<property name="password" value="mx123123"/>
						</dataSource>
					</environment>
				</environments>
				<mappers>
					<mapper resource="com/blanche/mapper/FlowerMapper.xml"/>
				</mappers>
			</configuration>
- 新建以mapper结尾的包，在包下新建：实体类名+Mapper.xml
	- 文件作用：编写需要执行的SQL命令
	- 把xml文件理解成实现类
	- xml文件内容
		
			<?xml version="1.0" encoding="UTF-8"?>
			<!DOCTYPE mapper
			  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
			  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
			<mapper namespace="a.b">
			<!--	id:方法名字 
					parameterType:定义参数类型
					resultType:返回值类型
					
					如果方法返回值是list,再resultType中写List的泛型,因为mybatis对jdbc封装,一行一行读取数据
					反射需要写全路径:报名+类名
			 -->
			 <select id="selAll" resultType="com.blanche.pojo.Flower">  
			 	select name name3 from flower  //别名name3，格式：字段名name+ 空格 + 别名
			 </select>
			</mapper>
	- 注：
		- 此处的com.blanche.pojo.Flower会使程序在运行时，自动通过实体类的属性与数据库中的字段名一一对应赋值给实体类，若实体类的属性与字段名不同，则需要别名

- 测试结果（只有在单独使用mybatis时使用，最后ssm整合时下面代码不需要编写）

		package com.blanche.test;
		
		import java.io.IOException;
		import java.io.InputStream;
		import java.util.List;
		
		import org.apache.ibatis.io.Resources;
		import org.apache.ibatis.session.SqlSession;
		import org.apache.ibatis.session.SqlSessionFactory;
		import org.apache.ibatis.session.SqlSessionFactoryBuilder;
		
		import com.blanche.pojo.Flower;
		
		public class Test {
			public static void main(String[] args) throws IOException {
				InputStream is = Resources.getResourceAsStream("myabtis.xml");
				//使用工厂设计模式
				SqlSessionFactory factory = new SqlSessionFactoryBuilder().build(is);
				//生产SqlSession
				SqlSession session = factory.openSession();
				
				List<Flower> list = session.selectList("a.b.selAll");
				for(Flower flower :list) {
					System.out.println(flower.toString());
				}
				
				session.close();
			}
		}
			
- 环境搭建详解
	- 1.全局配置文件中内容
		- <transactionManager/> type属性可取值
			- JDBC,事务管理使用JDBC原生事务管理方式
			- MANAGER把事务管理转交给其他容器，原生JDBC事务setAutoMapping（false）；

		- <dataSource/> type属性
			- POOLER使用数据库连接池
			- UNPOOLED 不使用数据库连接池，和直接使用JDBC一样
			- JNDI：java命名目录接口技术

- 数据库连接池
	- 在内存中开辟一块空间，存放多个数据库连接对象
	- JDBC Tomcat Pool，直接有tomcat产生数据库连接池
	- 图示：
		- active：当前连接对象被应用程序使用中
		- idle：等待应用程序使用

		- ![](https://i.imgur.com/YpvngxI.png)
	
	- 使用数据库连接池的目的：
		- 在高频率访问数据库时，使用数据库连接池可以降低服务器系统压力，提升程序运行效率
			- 小型项目不适用于数据库连接池

	- 实现JDBC tomcat Pool的步骤
		- 在web项目的META-INF中存放context.xml，在context.xml编写数据库连接池相关属性

				<?xml version="1.0" encoding="UTF-8"?>
				<Context>
				<!-- 连接池是在应用程序运行时生成还是在Tomcat运行时生成，多数情况下是Tomcat -->
				<!-- 若连接数据对象多久连接不上，则系统不再给与连接 -->
					<Resource 
					driverClassName="com.mysql.cj.jdbc.Driver"
					url="jdbc:mysql://localhost:3306/flower?useSSL=false&amp;serverTimezone=UTC&amp;characterEncoding=utf-8"
					username="root"
					password="mx123123"
					maxActive="70"
					maxIdle="20"
					name="test"
					auth="Container"    
					maxWait="10000"	  
					type="javax.sql.DataSource"
					/>
				</Context>
		- 把项目放不到tomcat中，数据库连接池产生了
			- &用&amp；表示，用于数据库参数配置
			- auth表示数据连接池启动条件，多数时伴随着tomcat启动而启动

		- 可以在java中使用jndi获取数据库连接池对象
			- Context:上下文接口，context.xml文件对象类型
			- 代码：
			
					Context cxt = new InitialContext();
					DataSource ds = (DataSource)cxt.lookup("java:comp/env/test");  //利用jndi获取外部资源，并转化成数据源
					Connection conn = ds.getConnection();
		- 当关闭连接对象时，把连接对象归还给数据库连接池，把状态改成idle

		- 完整代码：

				package com.blanche.servlet;
				
				import java.io.IOException;
				import java.io.PrintWriter;
				import java.sql.Connection;
				import java.sql.PreparedStatement;
				import java.sql.ResultSet;
				import java.sql.SQLException;
				
				import javax.naming.Context;
				import javax.naming.InitialContext;
				import javax.naming.NamingException;
				import javax.servlet.ServletException;
				import javax.servlet.annotation.WebServlet;
				import javax.servlet.http.HttpServlet;
				import javax.servlet.http.HttpServletRequest;
				import javax.servlet.http.HttpServletResponse;
				import javax.sql.DataSource;
				
				@WebServlet("/pool")
				public class DemoServlet extends HttpServlet{
					@Override
					protected void service(HttpServletRequest req, HttpServletResponse res) throws ServletException, IOException {
						try {
							Context cxt = new InitialContext();
							DataSource ds = (DataSource)cxt.lookup("java:comp/env/test");  //利用jndi获取外部资源，并转化成数据源
							Connection conn = ds.getConnection();
							res.setContentType("text/html;charset=utf-8");  //字符集设置，包含html所以用contentType
							PreparedStatement ps = conn.prepareStatement("select * from flower");
							ResultSet rs =ps.executeQuery();
							PrintWriter out = res.getWriter();  //响应，输出到页面上
							while(rs.next()) {
								out.print(rs.getInt(1) + "&nbsp;&nbsp;&nbsp;&nbsp;" + rs.getString(2) + "</br>");
							}
							out.print("success"); 
							out.flush();
							out.close();
						} catch (NamingException e) {
							e.printStackTrace();
						}catch (SQLException e) {
							
							e.printStackTrace();
						}
						
					}
				}
			- 每当web项目发布时，都先经过server，内部的web.xml配置的首个访问的便为第一个访问的页面
				- ![](https://i.imgur.com/eLm5X7j.png)

- 三种查询方式
	- selectList（）返回值为list<resultType 属性控制>
		- 适用于查询结果都需要遍历的需求

				List<Flower> list = session.selectList("a.b.selAll");
				for(Flower flower :list) {
					System.out.println(flower.toString());
				}
	- selectOne() 返回值Object
		- 适用于返回结果只是变量或一行数据时

				Flower flower = session.selectOne("a.b.selByName");  //返回值随着被赋值的变量的类型变换所变换，但是对于select*时，会报错，因为该方法只能返回一条
				System.out.println(flower.toString());
				session.close();
	- selectMap（）返回值Map	
		- 适用于需要在查询结果中通过某列的值渠道这行数据的需求
		- Map<key,resultType控制>，key-value，键-值，key对应数据库中某一列的字段名

				Map<Object, Object> map =  session.selectMap("a.b.c", "name"); //key对应字段名name
				System.out.println(map);
	- 总结：
		- 任何方法的返回值数量是固定好的，

