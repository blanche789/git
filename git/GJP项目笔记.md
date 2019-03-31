### 知识点
- 对于任何局部变量都不可以采用修饰符修饰，只可在作为全局变量（属性）的时候可以用修饰符修饰
	- 变量和属性是有区别的：
	- 变量是方法体中定义的，我们称为临时变量。
	- 属性是类体中定义的。
	- 而权限标示符只用于修饰属性和方法。不修饰变量。
	- 方法中定义的临时变量在方法调用完成之后就不存在了，不需要用修饰符定义！
- toString（）方法是任何继承了Object类都有的方法，它会在打印对象的时候默认调用
	- 测试代码：

			package cn.itcast.gjp.service;
			
			public class Test {
			
				public static void main(String[] args) {
					Test obj = new Test();
					System.out.println();
				}
			
			}
	
		**console：**
		 cn.itcast.gjp.service.Test@1175e2db
- 空参构造器：
	- 作用： 任何子类的构造方法的第一行必定是super（）（父类无参的构造函数），若父类中定义了有参构造函数，那么JVM就不会自动给父类编译无参构造函数，那么将会报错。因此，在父类中编写空参构造器可以使代码更加完善。super（parm1，parm2）（父类中有参构造器）

- 快捷键：
	- Alt+Shift+S，快速构造，重写toString
	- Alt + shift + M ：快速将代码块封装成方法
	- ctrl+1 ：快速创建1个类中没有的方法
- 分层处理：
	- 作用：合理的划分逻辑层，有利于程序的维护
	- View层：定义各种接口，调用controller层方法
	- Controller层：接受view层数据，调用service层方法，将数据传递给service层
	- Service层：接受controller层数据，调用dao层方法，将数据传给dao层
	- Dao层：接受service层数据，查询数据库，返回结果集存储到Bean对象，再存储到List

- List<e>:
	- list存储Bean对象,方便遍历 

- Scanner类
	- nextLine（）：将输入的整行字符串返给程序，包括空格
	- next（）：将有效字符前的空格、Tab、Enter键过滤掉，只返回有效字符。
	- Tip：
		- 在nextInt（）后nextLine会自动跳过，原因是nextInt（）只读取了整数，在缓冲区残留了\r,nextLine会直接读取,导致直接跳过了nextLine()方法,解决的办法有两种:
			- 将nextLine()都替换成next()(因为next不会接收残留在缓冲区中的\r)
			- 或者在nextInt()和nextLine()中插入一个in.nextLine

- QueryRunner类：
	- update（sql，param）：可返回insert的行数（int）

- 学习疑问：
	- 打包问题
	- javabean学习
	- debug