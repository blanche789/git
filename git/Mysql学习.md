## 启动和停止MySQL服务
- Mysql是一种C/S结构：客户端和服务端

- 服务端对应的软件：Mysqld.exe
## 开启mysql服务
- Net start 服务（mysql）：开启服务
- Net stop mysql：关闭服务

## 登录和退出MySQL系统
### 登录
- 通过客户端（mysql.exe）与服务器进行连接认证，就可以进行操作
- 通常：服务端与客户端不在同一台电脑上
	- 找到mysql.exe（通过cmd控制台：如果在安装的时候指定了mysql.exe所在的路径为环境变		量，就可以直接访问；如果没有，那么就必须进入到mysql.exe所在路径）
	-  输入对应的服务器地址：-h：host  -h[IP地址/域名]
	-	输入服务器中Mysql监听的端口： -P:port –P:3306
	-	输入用户名：-u:username	-u:root
	-	输入密码：-p：password –p：root

	-	连接认证基本语法：
		Mysql.exe/mysql    -h主机地址   -P端口   -u用户名    -p密码
	- Tips：
		-	通常端口都可以默认：mysql监听的端口通常都是3306
		-	密码的输入可以先输入-p，直接换行，然后再以密文方式输入密码

	- 登陆格式：
	
		 - **mysql -hlocalhost -uroot -p**
		 - **mysql -uroot -p** 

### 退出
- 断开与服务器的连接：通常Mysql提供的服务器数量有限，一旦客户端用完，建议就应该断开连接。

-	建议方式：使用SQL提供的指令
	-	Exit;		//exit带分号
	-	**\q;**		//quit缩写
	-	Quit：
## Mysql服务端架构

- Mysql服务端架构有以下几层构成：

	- 数据库管理系统（最外层）：DBMS，专门管理服务器端的所有内容
	- 数据库（第二层）：DB，专门用于存储数据的仓库（可以有很多个）
	- 二维数据表（第三层）：Table，专门用于存储具体实体的数据
	- 字段（第四层）：Field，具体存储某种类型的数据（实际存储单元）
- 
- 中常用的几个关键字
	- Row：行
	- Column：列（field）
## 数据库基本操作
- 数据库是数据存储的最外层（最大单元）,因为client端逐层访问的,所以先访问数据库
### 创建数据库
- create database 数据库名 [库选项];
- 库选项: 
	- :charset
	- 校对集:collate	

### 显示数据库
- 显示全部
	
		 show databases；
- 显示部分
	- show databases like 'my%';
	
			 show create database mydatabase;
		- 基本语法：show databases like ‘匹配模式’;
			- _：匹配当前位置单个字符
			-  %：匹配指定位置多个字符

### 显示数据库创建语句
- show create 数据库名;

		show create database mydatabase;
	- 显现出来的创建语句是经过加工的
	


### 选择数据库
- use 数据库名;
	
		 use mydatabase;
	- Tip:因为数据是存储到数据表，表存在数据库下。如果要操作数据，那么必须进入到对应的数据库才行。

### 修改数据库选项
- alter database 数据库名 chareset 字符集;
	
		 alter database mydatabase charset utf8;


### 删除数据库
- drop database 数据库名;
	
		 drop database mydatabase;
	- Tips:
		- 删除虽简单，但是切记要做好安全操作：确保里面数据没有问题。（重要）
		-   删除数据库之后：对应的存储数据的文件夹也会被删除（opt文件也被删除）

## 数据表的基本操作
### 创建数据表
- 普通创建数据表:
	- create table 数据库名.数据表名 (字段名 字段类型[字段属性,....])[表选项]
		
			 create table mydatabase2.students(name varchar(10))charset utf8; 
		- tips:
			- 此处的表选项与数据库的相似
				- Engine：存储引擎，mysql提供的具体存储数据的方式，默认有一个innodb（5.5以前默认是myisam）
				- Charset：字符集，只对当前自己表有效（级别比数据库高）
				- Collate：校对集
			- 数据表存储在数据库中:
				- 在数据表名字前面加上数据库名字，用“.”连接即可：数据库.数据表
				- 在创建数据表之前先进入到某个具体的数据库即可：use 数据库名字;
			
- 复制已有表结构
- create table 数据表名 like 已存在的数据表名;
	- create table mydatabase.teacher like mydatabase2.teacher;
	- tip:只要使用数据库.表名，就可以在任何数据库下访问其他数据库的表名

### 显示数据表(显示某个库下的所有表)
- 显示全部表:

 		 show tables;
- 匹配显示表
 - show tables like  ‘匹配模式’;


### 显示表的结构(显示字段名、字段类型、字段属性)
- Describe 表名;
- **Desc 表名;**
- show columns from 表名;

		Describe class;
		Desc teacher;
		show columns from students;

### 显示表的创建语句
- show create table 表名;

		show create table teacher\G
	- 末尾:
		- 加;与\g效果一样,字段信息横排
		- 加\G字段信息列排
		
### 修改表的属性(选项)
- alter table 表名 表选项 


		 alter table class charset utf8;

### 修改表名
- rename table 表名 to 新表名;

		 rename table class to my_school;

### 新增字段
-  alter table 表名 add 字段名 字段类型 [字段位置\first\after 已存在的字段名]
  
		  alter table my_school add age int first;
	- Tips：
		- First：在某某之前（最前面），第一个字段
		- After 字段名：放在某个具体的字段之后（默认的）
### 修改字段名
- alter table 表名 change 旧字段名 新字段名 字段类型 [列属性] [新位置]


		alter table my_class2 change id  class_id int ;


### 修改字段类型(属性\位置)
- alter table 表名 modify 字段名 字段类型;
	
		 alter table my_school modify age  varchar(20);
### 删除字段
- alter table 表名 drop 字段名;
	
		 alter table my_school drop age;

### 删除表结构
- drop table 表名;
	
		 drop table my_school;

## 数据基础操作
### 插入操作
- 插入部分数据；
		
		insert into teacher (name) values('高其');
	- insert into 表名 [(字段名)] values (字段列表) ;
		- tip:后面（values中）对应的值列表只需要与前面的字段列表相对应即可（不一定与表结构完全一致）

- 插入全部数据

		insert into teacher values(20,'方立勋');
	- insert into 表名 values (字段列表);
		- tip:值列表必须与字段列表一致
### 查询操作
- 查询所有数据

		select * from teacher;
	- 查询表中全部数据：select * from 表名;	//*表示匹配所有的字段

- 查询部分数据

		select name from teacher;
 - 查询表中部分字段：select 字段列表 from 表名;		//字段列表使用逗号“,”隔开

### 删除操作
- 删除某条数据

		delete from teacher where age = 20;
 - delete from 表名 [where 条件];	//如果没有where条件：意味着系统会自动删除该表所有数据（慎用）

### 更新操作
- 更新某条数据

		update teacher set age = 28 where name = '高其';
	- update 表名 set 字段名 = 新值 [where 条件];//如果没有where条件，那么所有的表中对应的那个字段都会被修改成统一值。 
## 字符集
### 设置客户端所有字符集
	set names utf8;

 - set names 字符集;
 - 输入sql语句乱码原因:
 	- 	用户是通过mysql.exe来操作mysqld.exe
	-	真正的SQL执行是Mysqld.exe来执行
	-	mysql.exe将数据传入mysqld.exe的时候，没有告知其对应的符号规则（字符集），而mysqld也没有能力自己判断，就会使用自己默认的（字符集）
- 解决办法:
	- mysql.exe客户端在进行数据操作之前将自己所使用的字符集告诉mysqld(客户端默认的字符集可通过my.ini配置文件查看)

- Set names gbk;**(这样做可以保证我输入的数据是什么,显示出来的就是什么数据)**
	- Set character_set_client = gbk;	//为了让服务器识别客户端传来的数据
	- Set character_set_connection = gbk;//更好的帮助客户端与服务端之间进行字符集转换
	- Set character_set_results = gbk;//为了告诉客户端服务端所有的返回的数据字符集

字符集转换过程图:

![](http://chuantu.biz/t6/348/1532504098x-1566688748.jpg)

- 输入sql的过程:通过client告诉服务端客户端字符集为gbk.然后通过connection在服务端通过gbk来存储数据;
- 读数据过程:通过result的字符集来储存所取出来的结果,并且以result的字符集显示在cmd窗口上

### 修改客户端字符集
	set character_set_client = utf8;

### 查看所有字符集
	show variables like 'character_set%';
	
- Tips：
	- gbk中文2个字节，英文1个字节
	- utf-8中文3个字节，英文1个字节 


## 列类型
### 整型类型:
- Tinyint
迷你整形，系统采用一个字节来保存的整形：一个字节 = 8位，最大能表示的数值是0-255
- Smallint
小整形，系统采用两个字节来保存的整形：能表示0-65535之间
- Mediumint
中整形，采用三个字节来保存数据。
- Int
整形（标准整形），采用四个字节来保存数据。
- Bigint
大整形，采用八个字节来保存数据。

- 创建数据表

		create table mydatabase.my_int(int_1 Tinyint,int_2 SmallInt,int_3 Mediumint,int_4 int,int_5 bigint);

- 插入整型数据

		insert my_int values(100,1000,10000,1000000,100000000);
	- Tip:Mysql默认的整型为负数,所以任何数据范围都包含负数,tinyint范围为-128~127,其余以此类推;


##### 无符号标识设定

- 基本语法：在类型之后加上一个 unsigned

		alter table my_int add int_6 tinyint unsigned first;

##### 显示长度
- Tinyint(3)： 表示最长可以显示3位，unsigned说明只能是正数，0-255永远不会超过三个长度
- Tinyint(4)：表示最长可以显示4位，-128~127
	- tip:显示长度只能表示数据的最高位为多少,不会自动填充,若要自动填充,需要增加zerofill属性.

- zerofill(填充类型)
	- 自动填充


			alter table my_int add int_7 tinyint(2) zerofill;
	- tip:
		- 可以指定整型数据的最高位,若存放的数据达到或者超过最高位,那么zerofill将不再填充.
		- 超过最高位的数据只要不超出数据类型的范围则没问题.

### 浮点型
- Float:精度为7位有效数字左右
- Double:精度位15位有效数字左右
- 创建浮点型数据

		create table my_float (float_1 float,float_2 float(10,2));
- 插入浮点型数据


		insert my_float values(1000000,12345678.90);
	- tip:float(M,D),M表明有效数字最高位,D表明小数的最高位数

### 定点数
- decimal:保持整数不变,每9个数字分配四个字节
- decimal(M,D):M最长位65,D最长为30

### 总结:
- 浮点数与定点数的相同点与区别:

	- 相同点:若M,D规定后,整数的位数就是M-D,不能再长;小数后都可以取多位,但系统会自动截取;
	- 区别:若浮点数是系统导致自动进位,如999999.99,那么不会出错;但是定点数是不允许进位的,为了保持整数的精准.

## 时间日期类型
- **Date**


	日期类型：系统使用三个字节来存储数据，对应的格式为：YYYY-mm-dd，能表示的范围是从1000-01-01 到9999-12-12，初始值为0000-00-00
- **Time**

	时间类型：能够表示某个指定的时间，但是系统同样是提供3个字节来存储，对应的格式为：HH:ii:ss，但是mysql中的time类型能够表示时间范围要大的多，能表示从-838:59:59~838:59:59，在mysql中具体的用处是用来描述时间段。
- **Datetime**

	日期时间类型：就是将前面的date和time合并起来，表示的时间，使用8个字节存储数据，格式为YYYY-mm-dd HH:ii:ss，能表示的区间1000-01-01 00:00:00 到9999-12-12 23:59:59，其可以为0值：0000-00-00 00:00:00
- **Timestamp**

	时间戳类型：mysql中的时间戳只是表示从格林威治时间开始，但是其格式依然是：YYYY-mm-dd HH:ii:ss
- **Year**
	
	年类型：占用一个字节来保存，能表示1900~2155年，但是year有两种数据插入方式：0~99和四位数的具体年
- Tips:
	- year进行两位数插入的时候，有一个区间划分，零界点为69和70：当输入69以下，那么系统时间为20+数字，如果是70以上，那配系统时间为19+数字
	- timestamp当对应的数据被修改的时候，会自动更新（这个被修改的数据不是自己）
	- 在进行时间类型录入的时候（time）还可以使用一个简单的日期代替时间，在时间格式之前加一个空格，然后指定一个数字（可以是负数）：系统会自动将该数字转换成天数 * 24小时，再加上后面的时间。

## 字符串型
### char和varchar
- **Char**
	- 定长字符：指定长度之后，系统一定会分配指定的空间用于存储数据
	- 基本语法：char(L)，L代表字符数（中文与英文字母一样），L长度为0到255

- **Varchar**
	- 变长字符：指定长度之后，系统会根据实际存储的数据来计算长度，分配合适的长度（数据没有超出长度）
	- 基本语法：Varchar(L)，L代表字符数，L的长度理论值位0到65535
	- Tip:
		- 因为varchar要记录数据长度（系统根据数据长度自动分配空间），所以每个varchar数据产生后，系统都会在数据后面增加1-2个字节的额外开销(是用来保存数据所占用的空间长度
		如果数据本身小于127个字符：额外开销一个字节；如果大于127个，就开销两个字节)
- **Char和varchar的区别**
	- char一定会使用指定的空间，varchar是根据数据来定空间
	- char的数据查询效率比varchar高：varchar是需要通过后面的记录数来计算


		- 如果确定数据一定是占指定长度，那么使用char类型；
		- 如果不确定数据到底有多少，那么使用varchar类型；
		- 如果数据长度超过255个字符，不论是否固定长度，都会使用text，不再使用char和varchar
		
### Text和Enum
#### Text
- 文本类型：本质上mysql提供了两种文本类型
	- Text：存储普通的字符文本
	- Blob：存储二进制文本（图片，文件），一般都不会使用blob来存储文件本身，通常是使用一个链接来指向对应的文件本身。
- Text：系统中提供的四种text
	- Tinytext：系统使用一个字节来保存，实际能够存储的数据为：2 ^ 8 + 1（字符）
	- Text：使用两个字节保存，实际存储为：2 ^ 16 + 2
	- Mediumtext：使用三个字节保存，实际存储为：2 ^ 24 + 3
	- Longtext：使用四个字节保存，实际存储为：2 ^ 32 + 4

- Tips:
	- 在选择对应的存储文本的时候，不用刻意去选择text类型，系统会自动根据存储的数据长度来选择合适的文本类型。
	- 在选择字符存储的时候，如果数据超过255个字符，那么一定选择text存储

#### Enum
- 枚举类型：在数据插入之前，先设定几个项，这几个项就是可能最终出现的数据结果。enum有规范数据的功能，能够保证插入的数据必须是设定的范围

- 如果确定某个字段的数据只有那么几个值：如性别，男、女、保密，系统就可以在设定字段的时候规定当前字段只能存放固定的几个值：使用枚举

- 基本语法：enum(数据值1,数据值2…)


		 create table my_gender (gender enum('男','女','保密'));
- 系统提供了1到2个字节来存储枚举数据：
	- 通过计算enum列举的具体值来选择实际的存储空间：如果数据值列表在255个以内，那么一个字节就够，如果超过255但是小于65535，那么系统采用两个字节保存。**每一个枚举的数据都可以用一个数据来表示，通过其数据的大小来分配空间**


- tips:
	- 插入数据：合法数据，字段对应的值必须是设定表的时候所确定的值
	- 枚举enum的存储原理：实际上字段上所存储的值并不是真正的字符串，而是**字符串对应的下标**：当系统设定枚举类型的时候，会给枚举中每个元素定义一个下标，这个下标规则从1开始
	Enum(1=>‘男’,2=>’女’,3=>’保密’)
	- 	既然实际enum字段存储的结果是数值：那么在进行数据插入的时候，就可以使用对应的数值来进行。
	- 特性:在mysql系统中,当数据遇到"+、-、*、/"，那么就会自动转换为数值，所以可以查询出Enum类型数据所对应的数值为多少。
		- **select 字段名 + 0 from 表名****；**

				select gender + 0 from my_gender;
#### Set
- 集合：是一种将多个数据选项可以同时保存的数据类型，本质是将指定的项按照对应的二进制位来进行控制：1表示该选项被选中，0表示该选项没有被选中。

- 基本语法：set(‘值1’,’值2’,’值3’…)
- 系统为set提供了多个字节进行保存，但是系统会自动计算来选择具体的存储单元
	- 1个字节：set只能有8个选项
	- 2个字节：set只能有16个选项
	- 3个字节：set只能表示24个选项
	- 8个字节：set可以表示64个选项


- Set和enum一样，最终存储到数据字段中的依然是数字而不是真实的字符串
- Set集合的意义：
	- 规范数据
	- 节省存储空间
- Tips:
	- Enum：单选框
	- Set：复选框

#### mysql记录数据长度
- 在mysql中每个数据最长为65535个字节，varchar类型的字段存放的数据为65535个字符，这就超出了长度，所以总共能够存储的字符数为：
- 65535/3 - 1=21844（减1的原因是要提供额外的字节来给记录数据所占用的字节数作为开销） ===>UTF8
- 65535/2 (余1)-1 = 32766  ===>提供两个字节作为记录开销

## 列属性
- 概念:列属性又称之为字段属性,在Mysql中一共有六个属性:null,默认值,列描述,主键,唯一键,自动增长

### Null属性
- 概念:代表字段为空

### 默认值
- Default:
	- 如果不插入数据,默认条件下会给字段插入默认的数据.默认值通常为Null
	- 通过default来代表比较长的字符串,提高效率

			create table my_null2(name varchar(10) Not null default 'user1',age int default 18);
			insert into my_null (name)values('Blanche');
			insert into my_null2 (age)values(20);

### 列描述
- 概念:Comment,是专门用于给开发人员进行维护的一个注释说明.
- 基本语法:comment '字段描述';

- tip:查看comment时,必须查看创建表的语句

### 主键
- 概念:主要的键.primary key,在一张表里,附带主键属性的字段,里面的数据具有唯一性

- ##### 创建主键
	- 创建表的过程中,直接在字段后面增加主键属性
	- 在所有字段之后增加primary key选项:primary key(字段名1,字段名2...)
	- 表后增加:alter table 表名 add primary key(字段名1,字段名2...)

			create table my_pri1 (username varchar(10) primary key);
			create table my_pri2 (username varchar(10),primary key(username));
			create table my_pri3 (username varchar(10)) charset utf8;
			alter table my_pri3 add primary key(username);

- ##### 查看主键
	- 查看表结构
	- 查看表的创建语句

- ##### 删除主键
	- alter table 表名 drop
 
### 复合主键
- 概念:将多个字段符合在一个主键,作用时约束点变为多个字段名唯一,唯有复合的字段都唯一时约束才能起作用.
	- 案例


		- 案例：有一张学生选修课表：一个学生可以选修多个选修课，一个选修课也可以由多个学生来选：但是一个学生在一个选修课中只有一个成绩。
		- 分析:当同一个学生,同一门课程时,只能录入一次数据,再次录入将会出Bug

### 主键约束
- 概念:主键一旦增加,那么对对应的字段有数据要求
	- 字段NULL属性不能为空
	- 字段数据不能重复

### 主键分类
- 业务主键:主键所在的字段,具有业务意义(学生ID,课程)
- 逻辑主键:自然增长的整型(应用广泛)

### 自动增长
- 概念:auto_increment,当给某个字段附加该属性之后,若其在插入数据时未插入数值,那么系统就会自动增加,填充数据.(通常自动增长用于逻辑主键)
- tip：若有自动增长，则一定要附加主键属性
- 修改自动增长;
	- Alter table 表名 auto_increment = 值;

- 增加自动增长 
	- Alter table 表名 modify 字段名 字段类型 primary key auto_increment;

- 删除自动增长
	- Alter table modify 表名 字段名 字段类型;(等于在原来字段的基础上不加自动增长属性)

- 初始设置
	- 在系统中，有一组变量用来维护自增长的初始值和步长
	
			Show variables like ‘auto_increment%’;
			set auto_increment_increment = 5;
			set auto_increment_offset = 2;
	- **auto_ increment_increment 步长**

	- **auto_ increment_offset 初始值**

- #### 细节问题:
	- 一张表只有一个自增长：自增长会上升到表选项中
	- 自增长修改的时候，值可以较大，但是不能比当前已有的自增长字段的值小
	- 如果主动插入数据,那么auto_increment将会跳到初始值以步长为公差的范围内,比如原来auto_increment=20,那如果下次插入数据时为21,那么auto_increment=20将会跳到23(步长为2,初始值为1,23=1+11*2)
	- 如果主动插入数据,但是插入数据的值比原来的auto_increment要小,那么auto_increment将不变

### 唯一键
- 概念:unique key,用来保证字段的唯一性
- 主键与唯一键的区别
	- 唯一键在一张表中可以有多个。
	- 唯一键允许字段数据为NULL，NULL可以有多个（NULL不参与比较）

- **创建唯一键**
	- 附加字段属性
	
				 create table my_uni (username varchar(10) unique);

	- 所有字段定义完之后,在定义
	
			 create table my_uni2(username varchar(10),id int,unique key(username));
	- 定义完字段后,再增加
	
			 create table my_uni (username varchar(10) unique);
			 alter table my_uni2 add unique key(username);
- **查看唯一键**
	- 在查看表创建语句的时候，会看到与主键不同的一点：多出一个“名字”

- **删除唯一键**
	- Index关键字：索引，唯一键是索引一种（提升查询效率）
	- 删除的基本语法：alter table 表名 drop index 唯一键名字;

- **复合唯一键**
	- 唯一键与主键一样可以使用多个字段来共同保证唯一性；
	- 一般主键都是单一字段（逻辑主键），而其他需要唯一性的内容都是由唯一键来处理。

- **修改唯一键**
	- 先删除后增加

## 表关系
##### 一对一
- 概念:一张表中的一条记录与另外一张表中最多有一条明确的关系：通常，此设计方案保证两张表中使用同样的主键即可
- 解决方案：将两张表拆分，常见的放一张表，不常见的放一张表,在不常见的表中维护一个字段,该字段
- 为常用表中的主键字段

##### 一对多
- 概念:一对多，通常也叫作多对一的关系。
- 解决方案:通常一对多的关系设计的方案，在“多”关系的表中去维护一个字段，这个字段是“一”关系的主键。


##### 多对多
- 概念:一张表中的一条记录在另外一张表中可以匹配到多条记录，反过来也一样。
- 解决方案:既然通过两张表自己增加字段解决不了问题，那么就通过第三张表来解决。增加一个中间表，让中间表与对应的其他表形成两个多对一的关系：多对一的解决方案是在“多”表中增加“一”表对应的主键字段。

## 高级操作
- **插入多条数据**


		 create table my_insert (name varchar(10) not null);
		
		insert into my_insert values('张三'),('李四'),('王五'),('赵六');
		
		select * from my_insert;
- **主键冲突**
	- 解决方案：

			insert into my_prim values('2','小杰') on duplicate key update name = '小杰'; 
			
			replace into my_prim values('3','小婷');
- **蠕虫复制**

		insert into my_prim (name)select (name) from my_prim;  //注意主键无法复制，需在为主键的字段附加自动增长属性。
- **更新数据（限制数量）**

		Update my_prim set name = '小杰' where name = '张三' limit 4; //在重复的多个数据里，选取前四个更改
- **删除数据（auto——increment）**


		create table my_tru(id int primary key auto_increment,name varchar(10));
		select * from my_tru;
		insert into my_tru values(22,'小杰');
		delete from my_tru;
		insert into my_tru values(null,'小杰');
		show create table my_tru;
		Truncate my_tru;  // ==>drop + create table,自动增长的属性的默认值是无法随着删除数据而被删除的,唯有用Truncate才可以消除其默认值,从1开始.
		insert into my_tru values(null,'小杰');
- **查询数据**
	- 完整查询指令：
	- Select select选项 字段列表 from 数据源 where条件 group by分组 having条件 order by排序 limit限制;
		- Select选项：
			- All==*  全部  
			- Distinct 去重

					select distinct * from my_auto7;
		- 字段列表（决定列是哪些字段）：
			- 别名：

					select distinct username as name1,username name2 from my_auto7;
		- From 数据源（决定从哪个表选取数据）：
			- 单表数据：from + 一张表
			- 多表数据：from + 表1，表2
				- Tip：得出来的结果类似于笛卡儿积


						select * from my_null,my_auto; //若表1有7条记录，表2有3条记录，那么结果有21条记录
			- 动态数据：from (select 字段列表 from 表) as 别名;
				- Tip：相当于从另外一张表中的几个字段列表拼凑成一张新的列表，再从中查询

						select * from(select username,id from my_auto) as my_self;
		- Group by 子句：Group by表示分组的含义：根据指定的字段，将数据进行分组：分组的目标是为了统计
			- 聚合函数：
				- count（）：加*则统计每组中的记录，如果为括号内为字段名，那么不统计null
				- avg（）：求平均值
				- sum()：求和
				- max()：求最大值
				- min()：求最小值
				- Group_concat()：为了将分组中指定的字段进行合并（字符串拼接）
				- Tip:括号内接字段名

						select class_id,count(*),max(height),min(age),avg(age) from my_class group by class_id;
			- 多分组：将数据按照某个字段进行分组之后，对已经分组的数据进行再次分组
				- group by 字段1，字段2； //排序按照字段先后顺序

					select class_id,gender,count(*) from my_class group by class_id,gender;
			- 分组排序：分组默认有排序的功能：按照分组字段进行排序，默认是升序（asc），降序为desc.
				- group by 字段 [asc|desc]，字段 [asc|desc]

		- 回溯统计：根据分组，向每一组的上一级汇报时，将两组数据相加，组成一个分组字段，并且分组字段名为null
			- group by 字段 [asc|desc] with rollup;

					 select class_id,gender,count(*) from my_class group by class_id asc ,gender desc with rollup;
		- Having 子句
			- Having的本质和where一样，是用来进行数据条件筛选。
			- Having在group by分组之后，可以使用聚合函数或者字段别名（where是从表中取出数据，别名是在数据进入到内存之后才有的），所以where无法使用聚合函数

					select class_id,count(*) as number from my_class group by class_id having number >=3;

			- Tip：having是在group by之后，group by是在where之后：where的时候表示将数据从磁盘拿到内存，where之后的所有操作都是内存操作。

		- Order by 子句：根据校对规则对数据进行排序
			- order by 字段 [asc|desc];		//asc升序，默认的

					select * from my_class order by age asc;
		- litmit 子句：主要是用来限制记录数量获取
			- 记录数限制
				- limt 数量;

						select * from my_class limit 2;
			-分页
				- limit offset,length;

						select * from my_class limit 0,3;  //分页操作，表示从0开始，查询前三条数据
				- 第几页=pagesize*（pageNum-1）
			- Tips：
				- **from后面的条件决定了行**
				- Mysql中记录的数量从0开始
				- Limit通常在查询的时候如果限定为一条记录的时候，使用的比较多：有时候获取多条记录并不能解决业务问题，但是会增加服务器的压力。
				- limit后面的length表示最多获取对应数量，但是如果数量不够，系统不会强求

## 运算符
- **算术运算符**：+、-、*、/
	- Tips：
		- 通常用于select 字段中
		- 除法的运算结果都是用**浮点数**表示
		- 除法中除数为0，那么运算结果为**NULL**
		- NULL进行任何运算结果都是**NULL**

				select int_1 +int_2,int_1 - int_2,int_2 * int_3,int_2 / int_4 from my_ysf;

- **关系运算符**：>、>=、<、<=、=、<>   
	- Tips：
		- 在条件比较中，=就是表示等于，没有对应的==符号
		- 在select字段中，表示=需要用<>括起来,否则表示赋值
		- 在Mysql中,比较数据时,数据会先转换成同类型如整数转换成字符
		- 再mysql中,无bool值,1表示true,0表示false
	
				select '1' <=> 1,'b' <> 2 ,'c' <=> 3;
	- between 条件1 and 条件2
		- Tips:
			- [条件1,条件2]
			- 条件1必须<=条件2

- **逻辑运算符**:and、or、not

		select * from my_class where age >=18 or height <=180;  //逻辑或
- **in运算符**:用来替代=，当结果不是一个值，而是一个结果集的时候
	-  语法:
		-  in (结果1,结果2,结果3…)

			select * from my_class where id in ('stu1','stu2');
- **is运算符**:专门用来判断字段是否为NULL的运算符,=无法判断null条件
	- 语法:
		- is null / is not null

			select * from my_ysf where int_4 is null;
- **like运算符**
	- 语法:
		- like ‘匹配模式’;
		- tips:
			- 匹配对应的单个字符
			- %：匹配多个字符
## 联合查询
- 概念:
	
	联合查询是可合并多个相似的选择查询的结果集(纵向合并,字段数不变)。等同于将一个表追加到另一个表，从而实现将两个表的查询组合到一起，使用谓词为UNION或UNION ALL。
- 基本语法:


	Select 语句
	
	Union [union 选项]
	
	Select 语句;
	
	- union 选项:
		- ALL:将全部记录数纵向合并
		- distinct:去掉重复的记录数,再合并(默认)

				select * from my_class
				union all
				select * from my_class;
	- Tip:
		- union理论上只要保证字段数一样，不需要每次拿到的数据对应的字段类型一致。永远只保留第一个select语句对应的字段名字。

- Order by的使用
	- Tips:
		- 在联合查询中，如果要使用order by，那么对应的select语句必须使用括号括起来
		- order by在联合查询中若要生效，必须配合使用limit：而limit后面必须跟对应的限制数量（通常可以使用一个较大的值：大于对应表的记录数）
					
				(select * from my_class where gender = 1 order by height desc limit 5)
				union
				(select * from my_class where gender = 2 order by height asc limit 5);
	
## 连接查询
- 概念:
	- 将多张表连到一起进行查询(横向合并,会导致记录数行和字段数列发生改变)

### 交叉连接:
- 概念:
	- 将两张表的数据与另外一张表彼此交叉(笛卡儿积)

- 原理:
	- 从A表里依次取出一条记录
	- 每取出一条记录则与B表里的每条记录进行合并
	- 记录数 = 第一张表记录数 * 第二张表记录数；字段数 = 第一张表字段数  + 第二张表字段数（笛卡尔积）

- 语法:
	- 表1 cross join 表2;

		select * from my_class cross join my_class2;

### 内连接
- 概念:
	- 从一张表中取出所有的记录去另外一张表中匹配：利用匹配条件进行匹配，成功了则保留，失败了放弃。

- 原理:
	- 从A表里依次取出一条记录
	- 每取出一条记录则与B表里的每条记录依次进行匹配
	- 条件匹配成功则合并数据,否则继续向下匹配,如果全表匹配失败，结束

- 语法:
	- 表1 [inner] join 表2 on 匹配条件;

			select * from my_class as c inner join my_class2 s on c.class_id = s.id;
- Tips:
	- 内连接因为不强制必须使用匹配条件（on）因此可以在数据匹配完成之后，使用where条件来限制，效果与on一样（建议使用on）
### 外连接
- 概念:
	- 按照某一张表作为主表（表中所有记录在最后都会保留），根据条件去连接另外一张表，从而得到目标数据。
	- 外连接分为两种：左外连接（left join），右外连接（right join）
		- 左连接：左表是主表
		- 右连接：右表是主表

- 原理:
	- 确定连接主表：左连接就是left join左边的表为主表；right join就是右边为主表
	- 拿主表的每一条记录，去匹配另外一张表（从表）的每一条记录
	- 如果满足匹配条件：保留；不满足即不保留
	- **如果主表记录在从表中一条都没有匹配成功，那么也要保留该记录：从表对应的字段值都为NULL**
- 语法:
	- 左连接：主表 left join 从表 on 连接条件;
	- 右连接：从表 right join 主表 on连接条件;
	
			select * from my_class2 as c left join my_class s on c.id = s.class_id; 
			
### Using关键字
- 概念:是在连接查询中用来代替对应的on关键字的，进行条件匹配。

- 原理:
	- 连接查询时,用using代替on
	- 使用using的条件是对应两张表的判断字段是同名的
	- 如果使用using关键字，那么对应的同名字段，最终在结果中只会保留一个。

- 语法:
	- 表1 [inner,left,right] join 表2 using(同名字段列表); //连接字段


			select * from my_class2 as c left join my_class s using (class_id); 
## 子查询
- 概念：
	- 子查询是一种常用计算机语言SELECT-SQL语言中嵌套查询下层的程序模块。**当一个查询是另一个查询的条件时，称之为子查询。**
	
- 主查询：
	- 主要的查询对象，第一条select语句，确定的用户所有获取的数据目标（数据源），以及要具体得到的字段信息。

- 子查询分类：
	- 按功能分：
		- 标量子查询：子查询返回的结果是一个数据（一行一列）
		- 列子查询：返回的结果是一列（一列多行）
		- 行子查询：返回的结果是一行（一行多列）
		- Exists子查询：返回的结果1或者0（类似布尔操作）

	- 按位置分：
		- Where子查询：子查询出现的位置在where条件中
		- From子查询：子查询出现的位置在from数据源中（做数据源）
		
**标量子查询**
- 概念：
	- 标量子查询：子查询得到结果是一个数据（一行一列）

- 语法：
	- select * from 数据源 where 条件判断 =/<> (select 字段名 from 数据源 where 条件判断); //子查询得到的结果只有一个值

			select classname from my_class2 as s where s.class_id = (select class_id from my_class where my_class.name = '婷婷'); 
- 原理：
	- where里的条件会筛选出一个值
	
**列子查询**
- 概念：
	- 子查询得到的结果是一列数据（一列多行）

- 语法：
	- 主查询 where 条件 in (列子查询);

			select classname from my_class2 as s where s.class_id in (select class_id from my_class);//in里有多个选择，主查询会逐条逐条进行匹配

**行子查询**

- 概念：
	- 子查询返回的结果是一行多列
- 语法：
	- 主查询 where 条件[（构造一个行元素）] = (行子查询);

	select * from my_class where (height,age) = (select max(height),max(age) from my_class);  //选取一个班里身高以及年纪最大的个人信息

**表子查询**（唯一的from+子查询）

- 概念：
	- 子查询返回的结果是多行多列，表子查询与行子查询非常相似，只是行子查询需要产生行元素，而表子查询没有。

- 语法：
	- Select 字段表 from (表子查询) as 别名 [where] [group by] [having] [order by] [limit];

			select * from (select * from my_class order by height desc) as temp group by class_id; //筛选出每个班级最高的人 

**Exists子查询**

- 概念：
	- 查询返回的结果只有0或者1，1代表成立，0代表不成立

- 语法：
	- where exists(查询语句); //exists就是根据查询得到的结果进行判断：如果结果存在，那么返回1，否则返回0

			select classname from my_class2 as s where exists(select id from my_class c where s.class_id = c.class_id);  //筛选出哪个班级里有人

### 总结：
- 表查询为**from + 子查询** ， 其余全为**where + 子查询**
- 若在having后使用聚合函数，那么无论前面是否有group by条件，都将会进行group by
- 标量：where **=**
- 列：where **in（....）** 
- 行:wher **(字段1,字段2)** = (字段1,字段2)
- 表:from **(select ....)**
- exists:where exists(**select语句**)

## 子查询关键字

**In**:
	
- 主查询 where 条件 in (列子查询);

**Any**:

- 概念:
	- = any(列子查询)：条件在查询结果中有任意一个匹配即可，等价于in
	- <>any(列子查询)：条件在查询结果中不等于任意一个

			select * from my_class2 where class_id =any(select class_id from my_class);  //等于其中任意一个即可

			select * from my_class2 where class_id <>any(select class_id from my_class); //不等于其中任意一个
	
**Some**:

- 与any完全一样

**All**:

- = all(列子查询)：等于里面所有
- <>all(列子查询)：不等于其中所有

		select * from my_class where class_id =All(select class_id from my_class2);
		select * from my_class where class_id <>All(select class_id from my_class2);
**Tips:**
	
- 如果对应的匹配字段有NULL，那么不参与匹配()

## 整库数据备份与还原
- 概念:
	- 整库数据备份也叫SQL数据备份：备份的结果都是SQL指令
	- 在Mysql中提供了一个专门用于备份SQL的客户端：mysqldump.exe

- 语法:
	- mysqldump/mysqldump.exe   -hPup   数据库名字 [表1   [表2…]]  >  备份文件地址

### 整库备份(只需要提供数据库名字):
	
	mysqldump -uroot -p mydatabase2 > D:/sql代码/sql.sql //只需提供已存在的数据库名字,将他存储到指定文件下,若文件不存在则自动创建

### 单表备份
### 多表备份
	mysqldump -uroot -p mydatabase2 my_auto my_time > d:/sql代码/auto_time.sql  //只需把已存在的数据库名字 + 需要备份的表的名字则可以进行多表备份

### 数据还原

- Mysql提供了多种方式来实现：两种
	- 利用mysql.exe客户端：没有登录之前，可以直接用该客户端进行数据还原
Mysql.exe –hPup 数据库 < 文件位置

			mysql -uroot -p mydb < d:/sql代码/auto_time.sql  //已备份的sql指令存储到已创建的一个表中.此处的mydb必须是已创建的表

	- 提供了一种导入SQL指令的方式
Source  SQL文件位置;		//必须先进入到对应的数据库

			source d:/auto_time.sql;  //进入存储还原数据的库

## 用户权限管理
- 概念:
	- 用户权限管理：在不同的项目中给不同的角色（开发者）不同的操作权限，为了保证数据库数据的安全。

### 用户管理
- Mysql中所有的用户信息都是保存在mysql数据库下的user表中。
- 在安装Mysql的时候，如果不选择创建匿名用户，那么意味着所有的用户只有一个：root超级用户

![](http://chuantu.biz/t6/351/1532956471x-1566688299.png)

- 在mysql中，对用的用户管理中，是由对应的Host和User共同组成复合主键来区分用户。
- User：代表用户的用户名
- Host：代表本质是允许访问的客户端（IP或者主机地址）。如果host使用%代表所有的用户（客户端）都可以访问(非服务端的ip,服务端的ip是localhost)

### 创建用户
- 基本语法：create user 用户名 identified by ‘明文密码’;
- 用户：用户名@主机地址
- 主机地址：‘%’


		create user 'user1'@'%' identified by '123456'; //%表示任何客户端均可登陆该用户
		create user 'user2';

### 删除用户
- mysql中user是带着host本身的（具有唯一性）
- 基本语法：drop user 用户名@host;
	
		drop user user2;

### 修改用户密码
- 基本语法:
	- alter user 'user'@'host' identified by '明文密码' password expire never(用不过期);
	
			UPDATE mysql.user SET authentication_string='mx123123' WHERE user='root' and host='localhost';
			ALTER USER 'root'@'localhost' IDENTIFIED BY 'mx123123' PASSWORD EXPIRE NEVER;

### 权限管理
- 在mysql中将权限管理分为三类：
 -	数据权限：增删改查（select\update\delete\insert）
 -	结构权限：结构操作（create\drop）
 -	管理权限：权限管理（create user\grant\revoke）：通常只给管理员如此权限

##### 基本语法：grant
- 基本语法：grant 权限列表 on 数据库/*.表名/* to 用户;
	- 权限列表：使用逗号分隔，但是可以使用all privileges代表全部权限
	- 数据库.表名：可以是单表（数据库名字.表名），可以是具体某个数据库（数据库.*），也可以整库（*.*）
			
			grant select on mydb.my_auto to 'user1@%'; 
			grant create on *.* to 'user1@%';
			
##### 取消权限：revoke
	- 基本语法：revoke 权限列表/all privileges on 数据库/*.表/* from 用户;
			
			revoke create on *.* from 'user1@%';
			revoke select on mydb.my_auto from 'user1@%';

##### 刷新权限：flush
- 基本语法：flush privileges;

### 密码丢失的解决方案
- 先net stop mysql,然后mysqld --console --skip-grant-tables --shared-memory(跳过权限管理)
- mysql.exe -u root,在另外一个cmd直接进入客户端
- alter user 'user'@'host' identified by '明文密码' password expire never(用不过期); 再直接修改密码
- 然后cmd,再net start mysql,即可利用新密码进入

## 外键(foreign key)
- 概念:

	- 一张表（A）中有一个字段，保存的值指向另外一张表（B）的主键
	- B：主表
	- A：从表
- 方案1
	- 语法:
		- 在字段之后增加一条语句[constraint `外键名`] foreign key(外键字段) references 主表(主键字段);外键名需要用反引号
	![](http://chuantu.biz/t6/351/1532958117x-1404817491.png)
	MUL：多索引，外键本身是一个索引，外键要求外键字段本身也是一种普通索引
	![](http://chuantu.biz/t6/351/1532958148x-1404817491.png)

- 方案2
	- 在创建表后增加外键
	- Alter table 从表 add [constraint `外键名`] foreign key(外键字段) references 主表(主键字段名字);

			alter table my_student add  foreign key(class_id) references my_class(class_id);
##### 修改&删除外键
- 外键不允许修改，只能先删除后增加
- 基本语法：
	- alter table 从表 drop foreign key 外键名字;
- 外键不能删除产生的普通索引，只会删除外键自己

		alter table my_student drop foreign key `my_student_ibfk_1`;

![](http://chuantu.biz/t6/351/1532958539x-1376440240.png)

- 如果想删除对应的索引：alter table 表名 drop index 索引名字;
					
		alter table my_student drop index `student_class_ihfk_1`;  --删除普通索引,`反引号


