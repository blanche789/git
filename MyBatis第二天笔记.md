## 一.注解
1. 注解存在的意义:简化xml文件的开发
2. 注解在servlet3.0规范之后大力推广
3. 注解前面@xxx,表示引用一个@interface
	1. @interface表示注解声明
4.	注解可以有属性,因为注解七十四就是一个接口 类
	1.	每次使用注解都要导包

5.	注解语法:@xxxx(属性名=值)
6.	值的分类
	1.	如果值是基本数据类型或字符串:属性名=值
	2.	如果值是数组类型:属性名={值,值}
		1.	如果只有一个值可以省略大括号

	3.	如果值是类类型,属性名=@名称

7.	如果注解只需要给一个属性赋值,且这个属性是默认属性,可以省略属性名

## 二.路径
1. 编写路径为了告诉编译器如何找到其他资源
2. 路径分类
	1. 相对路径:从当前资源出发找到其他资源的过程
	2. 绝对路径:从根目录(服务器根目录或者项目根目录)出发找到其他资源的过程
		1. 标志:只要以/开头的都是绝对路径
3. 绝对路径
	1. 如果是请求转发/表示项目根目录(Webcontent)
	2. 其他重定向,<img/><script/><style/>,location,href等/表示服务器根目录(tomcat/webapps 文件夹)
4. 如果客户端请求的控制器,控制器转发到JSP后,jsp如果使用相对路径,需要按照控制器的路径去找其他资源
	1. 保险方法:使用绝对路径,可以防止上面的问题