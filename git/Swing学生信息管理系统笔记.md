##Java学生信息管理系统笔记
###Java中Vector和ArrayList的区别
   -   首先看这两类都实现List接口，而List接口一共有三个实现类，分别是ArrayList、Vector和LinkedList。List用于存放多个元素，能够维护元素的次序，并且允许元素的重复。3个具体实现类的相关区别如下：

	- ArrayList：
		- 最常用的List实现类，内部是通过数组实现的，它允许对元素进行快速随机访问。数组的缺点是每个元素之间不能有间隔，当数组大小不满足时需要增加存储能力，就要讲已经有数组的数据复制到新的存储空间中。当从ArrayList的中间位置插入或者删除元素时，需要对数组进行复制、移动、代价比较高。因此，它适合随机查找和遍历，不适合插入和删除。
	- Vector（线程安全）：
		- 与ArrayList一样，也是通过数组实现的，不同的是它支持线程的同步，即某一时刻只有一个线程能够写	Vector，避免多线程同时写而引起的不一致性，但实现同步需要很高的花费，因此，访问它比访问ArrayList慢。
	- LinkedList：
		- 是用链表结构存储数据的，很适合数据的动态插入和删除，随机访问和遍历速度比较慢。另外，他还提供了List接口中没有定义的方法，专门用于操作表头和表尾元素，可以当作堆栈、队列和双向队列使用
		。
- Swing中tableModel的addRow（Vector<> data）方法的实现过程是将所有传进来的vector集合先存储起来,等所有vector传输完毕才统一上传到table上.
- vector对象必须是不同的,不然的话在上传到table过程中时,所有vector都会指向最后一次赋值的vector对象
- 源代码:
	
				Vector<String> currentRow1 = new Vector<String>();
				currentRow1.addElement("男");
				currentRow1.addElement(manNum + "");
				dtm.addRow(currentRow1);
		
				Vector<String> currentRow2 = new Vector<String>();
				currentRow2.addElement("女");
				currentRow2.addElement(womenNum + "");
				dtm.addRow(currentRow2); 

###Set迭代遍历
- 迭代遍历：  
	
			Set<String> set = new HashSet<String>();  
			Iterator<String> it = set.iterator();  
			while (it.hasNext()) {  
			  String str = it.next();  
			  System.out.println(str);  
			}  
- for循环遍历：  
			for (String str : set) {  
			 System.out.println(str);  
			}  

- Tips:
	- 可利用set集合的不重复性来剔除List中重复的数据

###数组不能通过toString方法转为字符串
- 任何类都继承父类的Object的toString方法,但是除了String类重写了之外,其他类并没有重写.直接调用toString方法,输出值为[类型@哈希值]
- 数组转化为String的两种方法
	- 直接再构造String时转换
	
			char[] data = {'a', 'b', 'c'};
			String str = new String(data);
	- 调用String类的方法转换

			String.valueOf(char[] ch);

### 数据库关键词
- 如果数据库中用关键字作为字段，那么在书写sql语句的时候，需要给该关键字加上反引号·

		String sql = "insert into user(`right`) values(?)";

### JTable排序
- API：java.swing/RowSorter
- 需要将JTable与RowSorter关联
- RowSorter是一个抽象类，需要其子类TabelRowSorter来实例化
- 源代码：

		DefaultTableModel dtm = (DefaultTableModel) studentInfoTable.getModel();
		dtm.setRowCount(0); // 设置成0行
		
		//实现排序功能,调用了swing的API,需要将RowSorter与JTable进行关联,而关联的桥梁便是TableModel
		//RowSorter是抽象类.需要其子类实例化啊对象
		RowSorter<DefaultTableModel> sorter = new TableRowSorter<DefaultTableModel>(dtm);
		studentInfoTable.setRowSorter(sorter);