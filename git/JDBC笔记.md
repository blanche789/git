### 驱动类加载&建立Connection
- 导入mysql的驱动包（Build path ➡ Add External Ar.. ）
- Class.forName先实例化驱动,创建一个Driver对象
	- Class.forName(String className)
- 连接数据库
	- Connection conn = DriverManager.getConnection(String url, String user, String password) 
- 代码

		Class.forName("com.mysql.jdbc.Driver");
	 	Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/mydb?useSSL=false","root","mx123123");
		System.out.println(conn);

- Tips:
	- 需要捕捉异常
	- Class非类class,是lang包中的一个类,用来注册驱动

### PreparedStatement接口
-  作用：包装Sql语句
-  常用方法：
	-  setObject(int parameterIndex, Object x) ；
	-  setDate(int parameterIndex, Date x) ；
	-  execute（） //在此 PreparedStatement 对象中执行 SQL 语句，该语句可以是任何种类的 SQL 语句。返回booleand
	-  executeQuery(); //在此 PreparedStatement 对象中执行 SQL 查询，并返回该查询生成的 ResultSet 对象。
	-  Tip：
		-  index是从1开始 
	- 代码实现：

		ps = conn.prepareStatement(sql);
		ps.setObject(1,"小二");
		ps.setDate(2, new Date(System.currentTimeMillis())); //时间
		ps.execute();
### ResultSet接口（结果集）
- 作用：遍历数据表
- 常用方法：
- next（），遍历结果集，每执行一次方法，则光标移到下一行，并判断下一行是否有值，若有则返回true，否则返回false，并且获取这一行的所有数据
- getInt（int columnIndex）//从next中遍历的一行数据中获取第几列的值，数据类型需要与表中的数据类型相同
- getString（int columnIndex）
- 代码实现：

		String sql2 = "select * from my_buy where id >?";
		ps = conn.prepareStatement(sql2);
		ps.setObject(1, 3);
		rs = ps.executeQuery(); 
		while(rs.next()) {
			System.out.println(rs.getInt(1) +"----"+ rs.getString(2) +"----"+ rs.getInt(3) + "----" + rs.getInt(4));
			}
		}
	

### 释放资源
- 释放顺序：后定义，先释放（像多重门一样，要先关里面的）
- 代码实现：

		finally {  
				try {
					rs.close();
				} catch (SQLException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
				try {
					ps.close();
				} catch (SQLException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
				try {
					conn.close();
				} catch (SQLException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
			}
- Tip：
	- 放在finally块里无论前面的try-catch如何，都会执行
	- 不可将close方法同时放在一个try模块里，否则报错一个close后，后续的close方法全部覆盖，不再释放资源

### 批量处理（Batch）
- 作用：同时插入大量数据到表中

- 代码实现：

		package com.blanche.JDBC;
		
		import java.sql.Connection;
		import java.sql.Date;
		import java.sql.DriverManager;
		import java.sql.SQLException;
		import java.sql.Statement;
		


		public class Demo3 {
			public static void main(String[] args) {
				Connection conn = null;
				Statement stmt = null;
				
			
			try {
				Class.forName("com.mysql.jdbc.Driver");
				conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/mydb?useSSL=false","root","mx123123");
				conn.setAutoCommit(false);  //关闭自动事务
				long start = System.currentTimeMillis();
				stmt = conn.createStatement();
				for(int i=0;i<20000;i++) {
					stmt.addBatch("insert into my_name (name) values ('杰"+i+"')");
				}
				stmt.executeBatch();
				conn.commit(); //开启自动事务
				long end = System.currentTimeMillis();
				System.out.println("插入20000条数据耗时:" + (end-start) + "ms");
				
				
			} catch (ClassNotFoundException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			} catch (SQLException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			} finally {  
				
				try {
					stmt.close();
				} catch (SQLException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
				try {
					conn.close();
				} catch (SQLException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
			}
	
	
		}
		}
- Tip：
	- 先将大量的插入语句存储到statement对象中，最后调用executeBatch（）方法，可以提高效率
	- 需要先关闭自动事务，然后再commit

## 总结
- Statement和PreparedStatemen
	- 区别：PreparedStatement可以使sql语句预编译，可以提高效率（在处理批量语句时）
	- 优点：PreparedStatemen可以防止sql注入式攻击，因为？作为占位符会将"1=1"等语句当作参数,不会识别未sql指令

