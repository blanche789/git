> import 与 from...import
> 在 python 用 import 或者 from...import 来导入相应的模块。
> 
> 将整个模块(somemodule)导入，格式为： import somemodule
> 
> 从某个模块中导入某个函数,格式为： from somemodule import somefunction
> 
> 从某个模块中导入多个函数,格式为： from somemodule import firstfunc, secondfunc, thirdfunc
> 
> 将某个模块中的全部函数导入，格式为： from somemodule import *


## 标准数据类型
- Python3 中有六个标准的数据类型：

	- Number（数字）
	- String（字符串）
	- List（列表）
	- Tuple（元组）
	- Set（集合）
	- Dictionary（字典）
	- Python3 的六个标准数据类型中：

- 不可变数据（3 个）：Number（数字）、String（字符串）、Tuple（元组）；
- 可变数据（3 个）：List（列表）、Dictionary（字典）、Set（集合）。

- isinstance 和 type 的区别在于：
	- type()不会认为子类是一种父类类型。
	- isinstance()会认为子类是一种父类类型。

当你指定一个值时，Number 对象就会被创建：
> var1 = 1
> var2 = 10

您也可以使用del语句删除一些对象引用。
del语句的语法是：

> del var1[,var2[,var3[....,varN]]]

您可以通过使用del语句删除单个或多个对象。例如：
> del var
> del var_a, var_b

### 数值运算
> var1 = 2/4 # 除法，得到一个浮点数
> var2 = 2//4 # 除法，得到一个整数
> var3 = 2 ** 5 # 乘方
> print(var1,var2,var3)

### String（字符串）
- Python中的字符串用单引号 ' 或双引号 " 括起来，同时使用反斜杠 \ 转义特殊字符。
- 字符串的截取的语法格式如下：

	> 变量[头下标:尾下标]
- Python 使用反斜杠(\)转义特殊字符，如果你不想让反斜杠发生转义，可以在字符串前面添加一个 r，表示原始字符串
- Tips：
	- 与 C 字符串不同的是，Python 字符串不能被改变。向一个索引位置赋值，比如word[0] = 'm'会导致错误。
		- 1、反斜杠可以用来转义，使用r可以让反斜杠不发生转义。
		- 2、字符串可以用+运算符连接在一起，用*运算符重复。
		- 3、Python中的字符串有两种索引方式，从左往右以0开始，从右往左以-1开始。
		- 4、Python中的字符串不能改变。

### List（列表）
列表是写在方括号 [] 之间、用逗号分隔开的元素列表。

和字符串一样，列表同样可以被索引和截取，列表被截取后返回一个包含所需元素的新列表。

列表截取的语法格式如下：

> 变量[头下标:尾下标]

	a = [1,2,'blanche','jay']
	print(a)
	print(a[1])
	print(a[0:2])  # 截断2号索引
- Tips：
	- 1、List写在方括号之间，元素用逗号隔开。
	- 2、和字符串一样，list可以被索引和切片。
	- 3、List可以使用+操作符进行拼接。
	- 4、List中的元素是可以改变的。

### Tuple（元组）
- 元组（tuple）与列表类似，不同之处在于元组的元素不能修改。元组写在小括号 () 里，元素之间用逗号隔开。
- 元组与字符串类似，可以被索引且下标索引从0开始，-1 为从末尾开始的位置。也可以进行截取（看上面，这里不再赘述）。其实，可以把字符串看作一种特殊的元组。
- 虽然tuple的元素不可改变，但它可以包含可变的对象，比如list列表。

- 构造包含 0 个或 1 个元素的元组比较特殊，所以有一些额外的语法规则：

		tup1 = ()    # 空元组
		tup2 = (20,) # 一个元素，需要在元素后添加逗号
- string、list 和 tuple 都属于 sequence（序列）。

- Tips：
	- 1、与字符串一样，元组的元素不能修改。
	- 2、元组也可以被索引和切片，方法一样。
	- 3、注意构造包含 0 或 1 个元素的元组的特殊语法规则。
	- 4、元组也可以使用+操作符进行拼接。

### Set（集合）
- 集合（set）是由一个或数个形态各异的大小整体组成的，构成集合的事物或对象称作元素或是成员。
基本功能是进行成员关系测试和删除重复元素。
- 可以使用大括号 { } 或者 set() 函数创建集合，注意：创建一个空集合必须用 set() 而不是 { }，因为 { } 是用来创建一个空字典。
		
		student = {'Tom', 'Jim', 'Mary', 'Tom', 'Jack', 'Rose'}
		 
		print(student)   # 输出集合，重复的元素被自动去掉
	
		# 成员测试
		if 'Rose' in student :
		    print('Rose 在集合中')
		else :
		    print('Rose 不在集合中')
		 
		# set可以进行集合运算
		a = set('abracadabra')
		b = set('alacazam')
		 
		print(a)
		 
		print(a - b)     # a 和 b 的差集
		 
		print(a | b)     # a 和 b 的并集
		 
		print(a & b)     # a 和 b 的交集
		 
		print(a ^ b)     # a 和 b 中不同时存在的元素

### Dictionary（字典）
- 字典（dictionary）是Python中另一个非常有用的内置数据类型。列表是有序的对象集合，字典是无序的对象集合。两者之间的区别在于：字典当中的元素是通过键来存取的，而不是通过偏移存取。
- 字典是一种映射类型，字典用 { } 标识，它是一个无序的 键(key) : 值(value) 的集合。
-  键(key)必须使用不可变类型。
- 在同一个字典中，键(key)必须是唯一的。

		dict={'name':'blanche','age':21}
		print(dict) # 输出完整的字典
		print(dict.keys()) # 输出所有键
		print(dict.values()) # 输出所有值
- Tips：
	- 1、字典是一种映射类型，它的元素是键值对。
	- 2、字典的关键字必须为不可变类型，且不能重复。
	- 3、创建空字典使用 { }。