## 数组的排序
- **Arrays类（隶属于java.util）**
    - sort(int[ ] a) 排序方法
    - fill()  填充方法
    - binarySearch(int []a,int key)  二分法找寻所需值
    - System.out.println(Arrays.toString(value));打印数组
    
    - Tips:以上方法均可通过遍历来实现


##命令行参数(String[] args)
   通过Run as来填充args


##for加强

            for(int i : a) 
            {
                System.out.println(i);
            }

##包装类(wrappclass)
- 类型
    - Integer
    - Character
    - Long
    - Short
    - Doublie
    - Float
    - Boolean
    - Byte

- Tips: 
 包装类既将基本数据类型转化为对象,作为对象,可以调用许多便捷的方法
- Example:

      a.toHexString(500);
      a.doubleValue();
      a.parseInt("985");

##自动装箱和拆箱
    
  Integer a = 1000;  //Integer a - new Integer(1000);

  int c =new Integer（1000）;  //int c = new a.intvalue;


##Date类(从1970.1.1的0点开始计算,通过毫秒计算)
- 常用的方法
    - setTime(value);
    - getTime();
    - before(Date when)

- DateFormat类（实现字符串与时间的转换，子类为SimpleFormat，位于java.text包中）
    
	Date a = new Date(1234123412342L);
	DateFormat df = new SimpleDateFormat("yyyy-M-d");
    String str1 = df.format(a);
        
    String str2 = “1999-7-10”；
    DateFormat df2 = new SimpleDateFormat（“yyyy-M-d”）；//与字符串的格式对应
    Date b = df2.parse（str2）;


##calendar类(子类GregorianCalendar)
- 作用:用来对日期更好的转换
- 常用的方法有:
    - Calendar d = new GregorianCalendar();
    - d.set(year,month,dateofmonth);
    - Date c = d.getTime();
    - d.add(Calendar.Year,30); //在年上增加30个月
    

##异常
- 一个图
 
    ```
    graph TB
    
    A(throwable) --> B(error)
    A(throwable) --> C(Exception)
    C(Exception) --> D(RunTimeException)
    C(Exception) --> E(OtherException)
    
    ```

- 五个关键字
    - try、catch、finally、throws、throw

- 在捕获的时候先捕获小的，再捕获大的

- 异常和重写的关系
    - 继承的类的重写的方法必须抛出与基类中方法一样的异常类型或者不抛出异常

##File类
- 类的说明：File类是用来查看文件或者创建文件的
- 常用的方法以及静态字符串：
    - File.separator -->在windows系统是\,在linux系统是/
    - File f = new File(directory, file);
    
        		if(f.exists()) {
    			System.out.println("文件路径:" + f.getAbsolutePath());
    			System.out.println("文件大小:" + f.length());
                }else {
    			f.getParentFile().mkdirs(); //这里必须调用mkdirs的方法,因为文件多个目录
    			try {   //属于IOException,须抛出异常
    				f.createNewFile();
    			} catch (IOException e) {
    				e.printStackTrace();
    			}
    		}
    - f.getName();  //取得路径下的文件名或者目录名;
    - f.isDirectory();  //判断f是否为路径名,既下一层是否还有文件;
    - f.listFile(); //返回一个File类型的数组,既f中下一层中所包含的全部文件存储在数组中;
        
##Enum类
- Function:用来规定m变量的值只能为枚举的那几个值,这就有利于在编译时期就发现m是否为规定的那几个值,提前发现错误
	
			public enum MyColor = { red, green, white };
			MyColor m = MyColor.red; //MyColor相当于类型,内部枚举的变量相当于是静态变量

##接口（java.util.*）
- **Collection接口**
	- **Set接口** ---->Hashset类     **Tips:只能装不同的对象**
	- **List接口** ---->LinkedList类
	-  / ArrayList类   **Tips:可以装相同的对象,既equal的两个对象**

-  **Map接口** ---->HashMap类	**Tips:一对一对的装对象**
- **容器的作用:**可以在任意时刻扩容的增加对象
- 代码的实现:

		Collection m = new HashSet(); //用父类引用指向子类对象,方便类的变换,这样使代码更加灵活
		m.add(Object e); //往容器一增加一个对象
		System.out.println(m.contains("hello")); //容器里是否包含某对象,返回bool值
		System.out.println(m); //打印的原理是通过toString方法,返回对象的字符串表示

### 注意:如若是通过HashSet中的add方法来装对象,如果装相同的对象,打印时会自动忽视相同的对象

	package com.blanche.collection;

	import java.util.ArrayList;
	import java.util.Collection;
	
	public class Test2 {
		public static void main(String[] args) {
		Collection m = new ArrayList();
		m.add("Hello");
		m.add(new Name("Wu","PeiJie"));
		m.add(new Name("Ye","SiTing"));
		System.out.println(m.remove("Hello"));
		System.out.println(m.remove(new Name("Ye","SiTing")));
		}  //remove方法返回的是一个bool值,他是通过equals方法判断两个对象是否相等的,若要remove自己定义的类的对象,那么只有重写equals方法才会返回true
	}
	
	class Name{
		
		private String firstName;
		private String lastName;
		public Name(String firstName,String lastName) {
			this.firstName = firstName;
			this.lastName = lastName;
		}
		
		public  String getFirstName() {
			return firstName;
		}
		public String getLastName() {
			return lastName;
		}
		
		public boolean equals(Object obj) {
			if(obj instanceof Name) {
			Name name = (Name) obj;
			return (firstName.equals(name.firstName)) && (lastName.equals(name.lastName));	
			}
			
			return super.equals(obj);
		}//重写equals方法,将判断对象是否相等改写为判断对象的属性是否相等
		
		public int hashCode() {
			return firstName.hashCode();
		}//通过调用String类的hashCode方法,返回一个整数,若两个对象的lastName相等,那么hashCode自然相等
		}
###注意:若重写了equals方法,那么一定要重写hashCode方法,因为若对象相等了,他们的哈希码应该相等,hashCode方法对于key - value比较高效,可以迅速找到索引

- **Iterator接口**
	- 作用：对于Collection接口下的许多容器类，都不能都迭代遍历，只能够打印全部，Iterator接口解决了这个问题，可以遍历容器内的对象。
	- 作用原理：通过容器类的对象调用iterator方法，返回一个实现了Iterator接口的对象，从而可以调用重写了的Iterator的方法.实际上，这里有应用了多态：①返回的对象实现了Iterator接口、②返回的对象重写了Iterator中的方法、3父类引用指向子类对象
	- Iterator中的方法：
		- boolean hadnext();  //游标右边仍有元素，则返回true
		- E next();			//返回游标右边的Object，同时将游标下移一格
		- void remove();  //移除迭代器返回的对象，调用一次next，返回一个对象，才能remove一个对象
	***	
	- 代码实现
	
			package com.blanche.Iterator;
			import java.util.Collection;
			import java.util.HashSet;
			import java.util.Iterator;




			public class Test1 {
				public static void main(String[] args) {
					Name n1 = new Name("Wu","PeiJie");
					Collection m = new HashSet();
					m.add(n1);
					m.add(new Name("Ye","SiTing"));
					Iterator i1 = m.iterator(); //父类引用指向子类对象
					for(;i1.hasNext();) {  
						System.out.println(i1.next());
					}
					System.out.println(m);
					for(;i1.hashNext;){
					Name name = (Name)i1.next();
					if(name.getFirstName().length()<3){
					i1.remove();	//不可调用m.remove,因为已经被Ieterator对象锁定了整个容器
			}
			}
				}
			}
		    class Name{
				
			private String firstName;
			private String lastName;
			public Name(String firstName,String lastName) {
				this.firstName = firstName;
				this.lastName = lastName;
			}
			
			public  String getFirstName() {
				return firstName;
			}
			public String getLastName() {
				return lastName;
			}
			public boolean equals(Object obj) {
				if(obj instanceof Name) {
				Name name = (Name) obj;
				return (firstName.equals(name.firstName)) && (lastName.equals(name.lastName));	
				}
				
				return super.equals(obj);
			}
			
			public int hashCode() {
				return super.hashCode();
			}
			public String toString() { //重写了toString方法
				
					
			String str1= this.getFirstName();
			String str2 =this.getLastName();
			return str1 + str2;
	
			}
			}		    
- **set接口**
	- 功能:装不同的对象的容器,且对象无序
	- 继承的类:HashSet
	- 常用方法:add();、retain（）；、addAll（）；
	- 代码实现:
	 
			package com.blanche.Set;
			
			import java.util.Collection;
			import java.util.HashSet;
			import java.util.Set;
			
			import com.blanche.collection.Name;
			
			public class Test1 {
				public static void main(String[] args) {
					Set s1 = new HashSet();
					Set s2 = new HashSet();
					s1.add(new Name("a","d"));
					s1.add(new Name("c","d"));
					s2.add(new Name("a","d"));
					s2.add(new Name("c","d"));
			
					s1.add("a");
					s1.add("b");
					s2.add("a");
					s2.add("d");
					Set sn = new HashSet(s1); 
					sn.retainAll(s2);  //求交集
					System.out.println(sn);
					Set sm = new HashSet(s2);
					sm.addAll(s1);  //求并集
					System.out.println(sm);
				}
			}
		- hashCode和equals方法重写的快捷键
			- alt + shift + s + h
			- 作用：两个方法的重写保证了set中元素的唯一性

- **List接口**
	- 作用：可以存放相同的对象
	- 继承的类：ArrayList（以数组形式存放对象），LinkedList（以链表形式存放对象）
	- 可以利用Collections类里的算法来对list中的元素进行排序
	- 代码实现：
	 
		package com.blanche.List;
		
		import java.util.ArrayList;
		import java.util.Collections;
		import java.util.List;
		
		public class Test1 {
			public static void main(String[] args) {
				List l1 = new ArrayList<>();
				l1.add("a0");
				for(int i=1;i<7;i++) {
					l1.add("a" + i);
			}   
				System.out.println(l1);
				Collections.reverse(l1); //逆序
				System.out.println(l1);
				Collections.shuffle(l1);  //乱序
				System.out.println(l1);
				Collections.sort(l1);  	//顺序
				System.out.println(l1);
				int index = Collections.binarySearch(l1,"a5");  //二分法寻找索引
				System.out.println(index);
			}
		}
- **Comparable接口**
	- 作用：通过对接口的继承，重写compareTo方法，这样就可以比较对象，若对象相同就返回1，对象A小于对象B，则返回-1；反之，则返回1；多数情况下是调用String类里重写的compareTo方法
	- 代码实现：
	
				@Override
			   public int compareTo(Object obj) {
			   	Name name = (Name)obj;
			   	int firstComp = this.firstName.compareTo(name.firstName);
		        return (firstComp != 0 ? firstComp : this.lastName.compareTo(name.lastName));
		    }
- **Map接口**
	- 作用：成对存储对象，分为key - value，
	- 继承的类：HashMap；TreeMap
	- 代码实现
		
			package com.blanche.Map;
	
			import java.util.Collection;
			import java.util.HashMap;
			import java.util.Map;
			import java.util.TreeMap;
			
			public class Test1 {
				public static void main(String[] args) {
					Map m1 = new HashMap();
					Map m2 = new TreeMap();
					//m1.put("one",new Integer(1)); //可以自动装箱，1 = new Integer（1）；
					m1.put("one",1 );   //put（）方法会返回一个value,返回的是先前被顶替掉的value
					m1.put(2, "two");
					m2.put("A", "one");
					m2.put("B", "two");
				System.out.println(m1);
				System.out.println(m2);
					System.out.println(m1.size());
					System.out.println(m2.size());  //长度是以对为基本单位
					Collection c1 = m1.values();
					System.out.println(c1);
					System.out.println(m1.containsKey("1"));  //返回bool值，底层是通过hashCode方法判断的，因为通过equals遍历对象的话效率太低
					System.out.println(m1.containsValue("2"));
					//int i = (Integer)m1.get("one").intValue();
					int i = (Integer)m1.get("one");		//自动拆箱,要强制转换,因为不清楚map返回的value是什么类型,自动拆箱既省略intValue方法
				}
			}
- **Collections类**
	- 作用:为List提供各种排序的方法
	- 常用的方法:sort顺序;shuffle乱序;binarySearch二分法查找索引;
	- 代码实现:
	
			Collections.reverse(l1); //逆序
			Collections.shuffle(l1);  //乱序
			Collections.sort(l1);  	//顺序


- **泛型**
	- 作用：将类里各种方法的Object替换成自身规定的类，那么就可以将自己定义的类的一些特殊的方法保存下来，不用强制转换。增强了代码的稳定性与可读性。
	
	- 作用范围:查看API文档各种类后是否有<>.可以在定义集合、Collection、在类实现接口Comparable的时候利用泛型

##接口总结
- **1136**
	- 1张图：
	- 1个类：Collections
	- 3个知识点：For增强、
	- 
	- 
	- 
	- 泛型（Generic）、Auto-Boxing/unBoxing
	- 六个接口：Collection、Set、List、Map、Iterator、Comparable
***

##IO流（java.IO.*）

- 概念:
	- 从程序的角度来看,分为输入流(inputStream)、输出流（outputStream）
	- 从处理数据单位来看，分为字节流、字符流
	- 从功能来看，分为节点流、处理流
- java.IO包中所有类都继承于四个抽象类：
	- 输入流:InputStream（字节流）、Reader（字符流）  Tips：1个字符长度等于2个字节
	- 输出流：OutputStream（字节流）、Writer（字符流）

- 常用的流（继承类）：
	- **File**(~InputStream、OutputStream、Writer、Reader) ----节点流、文件流
- 代码实现
		 
			package com.blanche.IO;
			import java.io.FileNotFoundException;
			import java.io.FileReader;
			import java.io.FileWriter;
			import java.io.IOException;
			
			public class Test1 {
				public static void main(String[] args) {
					FileReader f1 = null;
					FileWriter w1 = null;
					int b = 0;
					try {
						try {
							f1 = new FileReader("E:\\test\\test1.txt");
							w1 = new FileWriter("E:\\test\\test2.txt");
							while((b=f1.read())!=-1) {
								w1.write(b);
							}
							f1.close();
							w1.close();
						} catch (FileNotFoundException e) {
							System.out.println("未找到文件");
							e.printStackTrace();
						}
						} catch (IOException e) {
							System.out.println("输入失败");
							e.printStackTrace();
						}
			
				}
			}
	- **Buffered**（~InputStream、OutputStream、Writer、Reader） ----处理流（管子包装）、缓冲流
	- 常用的方法：read（）；write（）；close（）（一定记得关闭流）
	- Buffered~常用的方法：读：readLine ~整行读  写：newLine ~ 换行
		- 代码实现
		
			 	package com.blanche.IO;
			
				import java.io.BufferedReader;
				import java.io.BufferedWriter;
				import java.io.FileReader;
				import java.io.FileWriter;
				import java.io.IOException;
				
				public class Test4 {
					public static void main(String[] args) {
						try {
							BufferedReader b1 = 
									new BufferedReader(new FileReader("e:\\test\\test5.txt"));
							BufferedWriter b2 =
									new BufferedWriter(new FileWriter("E:\\test\\test6.txt"));
							String str1 = null;
						while((str1=b1.readLine())!=null) {
							System.out.println(str1);
						}
						
						for(int i=0;i<=1000000;i++) {
							b2.write(String.valueOf(Math.random()));
							b2.newLine();
						}
						b2.flush();
						b1.close();
						b2.close();
					} catch (IOException e) {
						// TODO Auto-generated catch block
						e.printStackTrace();
					}
				}
				//	String str1 ="Hello";
				//	byte[] b1 = str1.getBytes();
				//	System.out.println(b1[0]);
				}
				
	
	- **InputStreamReader\OutputStreamWriter(转换流)（处理流）**
	- 功能：将字节流转换为字符流
	- 常用的方法：
		- ①getEncoding（）；//获得编码类型  
		- ②FileOutputStream(String file,boolean)  //boolean值表明文件是否要保持原来的内容 
		- ③System.in中in的类型位InputStream,流接在键盘上 
	- 代码实现：
		- Test1：
			
				package com.blanche.IO;
				
				import java.io.FileOutputStream;
				import java.io.IOException;
				import java.io.OutputStreamWriter;
				
				public class TransformIO {
					public static void main(String[] args) {
						try {
							OutputStreamWriter osw = new OutputStreamWriter(new FileOutputStream("E:\\test\\test7.txt"));
							System.out.println(osw.getEncoding());
							osw.write("MicroSoft is not bad!");
							osw.close();
							osw = new OutputStreamWriter(new FileOutputStream("E:\\test\\test7.txt",true),"ISO8859_1"); 
							osw.write("MicroSoft is not bad!");
							System.out.println(osw.getEncoding());
							osw.close();
						} catch (IOException e) {
							e.printStackTrace();
						}
					}
		- Test2：
		
				package com.blanche.IO;
				
				import java.io.BufferedReader;
				import java.io.FileInputStream;
				import java.io.IOException;
				import java.io.InputStreamReader;
				
				public class TransformIO2 {
					
					public static void main(String[] args) {
						try {
							InputStreamReader isr = new InputStreamReader(System.in);
							BufferedReader br = new BufferedReader(isr);
							String str = null;
							while((str=br.readLine())!=null) {
								if(str.equalsIgnoreCase("exit")) break;
								System.out.println(str.toUpperCase());
								}
							isr.close();
							br.close();
						} catch (IOException e) {
								e.printStackTrace();
						}
					}
				}
	- **DataIO(数据流、处理流)** 
		- 功能：可以将不同的数据类型以多字节的形式存入文件中
		- 代码实现：
		
				package com.blanche.IO;
				
				import java.io.ByteArrayInputStream;
				import java.io.ByteArrayOutputStream;
				import java.io.DataInputStream;
				import java.io.DataOutputStream;
				import java.io.IOException;
				
				public class DataIO1 {
					public static void main(String[] args) {
						ByteArrayOutputStream bos = new ByteArrayOutputStream();
						DataOutputStream ds = new DataOutputStream(bos);
						try {
							ds.writeDouble(Math.random());
							ds.writeBoolean(true);  //***
							ByteArrayInputStream bis = new ByteArrayInputStream(bos.toByteArray());
							DataInputStream dis = new DataInputStream(bis);
							System.out.println(dis.readDouble());
							System.out.println(dis.readBoolean());
							ds.close();
							dis.close();
						} catch (IOException e) {
							System.out.println("输入输出错误"); 
							e.printStackTrace();
						}
						
					}
				}

    - **Print流（处理流、输出流）**
	    - 功能：将各种数据打印在文件上
	    - 代码实现：
		    - Test1:
		    
					package com.blanche.IO;
					
					import java.io.FileOutputStream;
					import java.io.IOException;
					import java.io.PrintStream;
					
					public class PrintStream1 {
						public static void main(String[] args) {
							
							try {
								FileOutputStream fs = new FileOutputStream("E:\\test\\test8.txt");
								PrintStream ps = new PrintStream(fs);
								System.setOut(ps);
								char c = 0;
								int i = 0;
								for(;c<=60000;c++) {
									System.out.print(c + " ");
									if(i>=100) {
										System.out.println();
										i=0;
									}
								}
								System.out.println("Hello");
							} catch (IOException e) {
								e.printStackTrace();
							}
						}
					}
			- Test2
			
					package com.blanche.IO;
					
					import java.io.BufferedReader;
					import java.io.FileReader;
					import java.io.IOException;
					import java.io.PrintStream;
					
					public class PrintStream2 {
						public static void main(String[] args) {
						String fileName = args[0];	
						PrintStream ps = System.out;
						list(fileName,ps);
						}
						
						public static void list(String fileName,PrintStream ps) {
							try {
								FileReader fr = new FileReader(fileName);
								BufferedReader br = new BufferedReader(fr);
								String str = br.readLine();
								while(str!=null) {
									ps.println(str);
									str = br.readLine();
								}
							} catch (IOException e) {
									e.printStackTrace();
							}
							
						}
					}
				- Test3
				
						package com.blanche.IO;
						
						import java.io.BufferedReader;
						import java.io.FileWriter;
						import java.io.IOException;
						import java.io.InputStreamReader;
						import java.io.PrintWriter;
						import java.util.Date;
						
						public class PrintStream3 {
							public static void main(String[] args) {
								try {
									BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
								
										FileWriter bw = new FileWriter("E:\\test\\test11.txt");
										PrintWriter pw = new PrintWriter(bw);
										String str = br.readLine();
										while(str!=null) {
											if(str.equalsIgnoreCase("exit")) break;
											System.out.println(str.toUpperCase());
											pw.println("-----------");
											pw.println(str);
											pw.println(str.toUpperCase());
											pw.println("=====" + new Date() + "=====");
											str=br.readLine();
										}
										
										pw.close();
										bw.close();
						
								} catch (IOException e) {
									
									e.printStackTrace();
								}
							}
						}
- Tips：
	- ①全部方法皆可通过抛IOException来解决
	- ②Buffered~的构造方法的参数可以是相应基类的任何子类
	- ③写文件时若在目录下没有文件，将自行创建
	- ④IO流可以通过一个水管怼入文件来理解
***
## 线程
- 概念：

	- ①线程：在cpu中运行的称之为线程，一个cpu只能同时运行一个线程。在java中，以分支来定义线程，一个分支既一个线程，main方法是主分支，也是主线程。若要将实现java的多线程，那么需要通过Thread类以及Runnable接口来实现。
	- ②进程：一个静态的概念。eg：一个.exe文件，一个.class文件。 
- 实现多线程方法：
	- ①：
		- 通过实现Runnable接口，重写public void run()，将所需要实现的方法写在run内部；
		- 然后new一个Thread对象出来，通过Thread类中的start方法来启动线程（start方法内部调用了run方法）。必须通过start来通知cpu启动线程，不可直接调用run方法，那样无法实现一个程序多线程。
	- ②：
		- 通过继承Thread类，重写public void run()，将所需要实现的方法写在run内部；
		- 然后直接new一个子类对象，调用start方法。
	
	- Tips：建议使用第一种方法，比较灵活，可以实现多个接口，继承其他类

- 线程中常用的方法：
	- sleep：可以让线程进入阻塞状态，可以通过Thread类的interrupt方法来中断sleep，那样会抛出异常。在那个方法里调用Thread.sleep()就会让那个方法进入阻塞状态
	- setPriotiry(int newPriority):将线程的优先级提高,最大的优先级为10,最小为1
	- yield:暂时让出cpu的位置
	- join:让分支线程合并到主线程,那么就变为一个线程了 
	- isAlive:判断线程是否还存在.Thread.currentThread().isAlive()
	- 如何关闭死循环的线程,可以封装一个布尔值变量,通过调用方法来关闭线程.
		- 代码实现:
			
				class MyThread7 implements Runnable{
				private boolean flag = true;
				@Override
				public void run() {
					while(flag) {
						System.out.println("I am Jay!");
					}
				}
				public void shutDown() {
					flag = false;
				}
				}
- 线程同步:
	- Synchronized:
		- 当同一个对象出现在多个线程中时，若对象的某个方法被锁定了，只有这个方法在其所在的线程被执行完毕，才能解锁对象，那么该对象才能在另外一个线程中起作用。如Test2，在m1和m2都被关键字synchronized修饰后，若他们在不同的线程被同一个对象调用，那么只有m1结束后，在主线程才能够继续执行m2.但若m2未被synchronized锁定，那么就可以同时实现m1和m2.
		
		- 代码实现:
			- Test1
			
					package com.blanche.Thread;
					
					public class TestSynchronized implements Runnable{
						Run r1 = new Run();
					
					 public static void main(String[] args) {
						  
						 	TestSynchronized ts1 = new TestSynchronized();
						 	Thread t1 = new Thread(ts1);
						 	Thread t2 = new Thread(ts1);
						 	t1.setName("ts1");
						 	t2.setName("ts2");
						 	t1.start();
						 	t2.start();
					}
					
					@Override
					public void run() {
						// TODO Auto-generated method stub
						r1.add(Thread.currentThread().getName());
						System.out.println();
					}
					 
					}
					
					class Run {
						private static int num = 0;
						public synchronized void add(String name) {
							num++;
							System.out.println(name+ "是第" + num + "个执行线程");
						}
					}
			- Test2

					package com.blanche.Thread;
					
					public class TestSynchronized2 implements Runnable{
						 int b = 0;
						public synchronized void m1() {
							b = 1000;
							try {
								Thread.sleep(5000);
							} catch (InterruptedException e) {
								e.printStackTrace();
							}
							System.out.println("b=" + b);
						}
						
						public synchronized void  m2() {
							b = 2000;
						}
						@Override
						public void run() {
							m1();
						}
						public static void main(String[] args){
							TestSynchronized2 ts1 = new TestSynchronized2();
							Thread t1 = new Thread(ts1);
							t1.start();
							try {
								Thread.sleep(1000);
							} catch (InterruptedException e) {
								// TODO Auto-generated catch block
								e.printStackTrace();
							}
							ts1.m2();
							System.out.println(ts1.b);
						}
					}
		- 若加上synchronized，那么程序的效率将会降低；
		- 若面对于数据的修改，若不用synchronized修饰，那么可能会造成同一个数据紊乱。
		- 在面对改数据时，最好加上synchronized；在读数据时，最好不加synchronized。
	- **生产者消费者问题**
		- 代码实现：
		
		
				package com.blanche.Thread;
				
				public class ProducerConsumer {
					public static void main(String[] args) {
						SyncStack ss = new SyncStack();
						Producer p = new Producer(ss);
						Consumer c = new Consumer(ss);
						new Thread(p).start();
						new Thread(c).start();
					}
				}
				class WoTou {
					int id;
					WoTou(int id) {
						this.id = id;
					}
					public String toString() {
						return "WoTou : " + id;
					}
				}
				
				class SyncStack {
					int index = 0;
					WoTou[] arrWT = new WoTou[6];
					public synchronized void push(WoTou wt) {
						while (index == arrWT.length) {  //使用while而不是用if，因为通过try-cathch异常之后，还会执行接下来的代码，所以必须通过while循环进行判断。
							try {
								this.wait();
							} catch (InterruptedException e) {
								e.printStackTrace();
							}
						}
						this.notifyAll();
						arrWT[index] = wt;
						System.out.println("set: " + arrWT[index]);
						index++;
					}
					public synchronized WoTou pop() {
						while (index == 0) {
							try {
								this.wait();
							} catch (InterruptedException e) {
								e.printStackTrace();
							}
						}
						this.notifyAll();
						index--;
						System.out.println("get :" + arrWT[index]);
						return arrWT[index];
					}
				}
				
				class Producer implements Runnable {
					SyncStack ss = null;
					Producer(SyncStack ss) {
						this.ss = ss;	}
					public void run() {
						for (int i = 0; i < 20; i++) {
							WoTou wt = new WoTou(i);
							ss.push(wt);
							try {
								Thread.sleep((int) (Math.random() * 200));
							} catch (InterruptedException e) {
								e.printStackTrace();
							}
						}
					}
				}
				
				class Consumer implements Runnable {
					SyncStack ss = null;
					Consumer(SyncStack ss) {
						this.ss = ss;
					}
					public void run() {
						for (int i = 0; i < 20; i++) {
							WoTou wt = ss.pop();
							try {
								Thread.sleep((int) (Math.random() * 1000));
							} catch (InterruptedException e) {
								e.printStackTrace();
							}
						}
					}
				}
 			
 			- 总结：生产者与消费者问题介绍了wait和notify方法，wait方法的作用是使当前线程放弃对象锁，并且进入阻塞状态；notify的作用是唤醒正在等待的线程，当当前线程执行完成synchronized的代码块时，才会放弃对象的锁，开始执行被唤醒的线程。
***
##网络编程
	
- IP协议:为每台电脑提供了独一无二的地址。4个字节
- TCP协议:A方
- 发送一条消息到B方，在B方接收之后，才能够接收下一条消息（可靠，但效率低）
- UDP协议：A方发送N条消息，不用确认B方是否高）接收到消息（不可靠，但效率）![](http://chuantu.biz/t6/346/1532059809x-1404755451.png)
- Socket编程（java.net）：
	- 两个java应用程序可通过一个双向的网络通信连接实现数据交换，这个双向链路的一端称为一个Socket.
	- 实现client-server连接
	- Socket和ServerSocket分别用来实现client和server端
	- 建立连接时所需寻址信息为远程计算机的IP地址和端口号(Port number)
		- TCP端口:
			- 代码实现:
			
					 TestServer.java
		
					package com.blanche.Socket;
					
					import java.io.DataInputStream;
					import java.io.DataOutputStream;
					import java.io.IOException;
					import java.io.InputStream;
					import java.io.OutputStream;
					import java.net.ServerSocket;
					import java.net.Socket;
					
					public class TestServer {
						public static void main(String[] args) {
							ServerSocket ss = null;
							try { 
								ss = new ServerSocket(5555); //端口号,在此端口进行监听
								while(true) {
								Socket s = ss.accept(); //阻塞式编程,唯有接收到client端的连接才能继续执行代码;s表示连接client的通道,并通过s调用IO来进行读写
								OutputStream os = s.getOutputStream(); 
								InputStream is = s.getInputStream();//
								DataOutputStream dos = new DataOutputStream(os);
								DataInputStream dis = new DataInputStream(is);
								dos.writeUTF("Hello,Client");
								System.out.println(dis.readUTF());
								System.out.println(s.getInetAddress());
								System.out.println(s.getPort()); //取得client端的端口号
								dos.close();
								dis.close();
								}
							} catch (IOException e) {
								// TODO Auto-generated catch block
								e.printStackTrace();
							}
					
							}
					}
			- TestClient.java:
	
					package com.blanche.Socket;
					
					import java.io.DataInputStream;
					import java.io.DataOutputStream;
					import java.io.IOException;
					import java.io.InputStream;
					import java.io.OutputStream;
					import java.net.Socket;
					import java.net.UnknownHostException;
					
					public class TestClient {
						public static void main(String[] args) {
							Socket s;
							try {
								s = new Socket("localhost",5555);  //client端通过IP和端口号寻找到server端
								InputStream is = s.getInputStream();
								OutputStream os = s.getOutputStream();
								DataInputStream dis = new DataInputStream(is);
								DataOutputStream dos = new DataOutputStream(os);
								System.out.println(dis.readUTF());
								dos.writeUTF("Hello,Server!"); 
								s.close();
							} catch (UnknownHostException e) {
								// TODO Auto-generated catch block
								e.printStackTrace();
							} catch (IOException e) {
								// TODO Auto-generated catch block
								e.printStackTrace();
							}
							
						}
					}

		- UDP端口:
			- 代码实现:
				
				- Server:
					
						package com.blanche.Socket;
						
						import java.io.ByteArrayInputStream;
						import java.io.DataInputStream;
						import java.net.DatagramPacket;
						import java.net.DatagramSocket;
						
						public class UDPServer {
							public static void main(String[] args) {
								byte[] buf = new byte[1024]; 
								DatagramPacket dp = new DatagramPacket(buf, buf.length);
								try {
									DatagramSocket ds = new DatagramSocket(6666);
									while(true) {
										ds.receive(dp);
										ByteArrayInputStream bas = new ByteArrayInputStream(buf);
										DataInputStream dis = new DataInputStream(bas);
										long n = dis.readLong();
										System.out.println(n);
										
									}
								} catch (Exception e) {
									// TODO Auto-generated catch block
									e.printStackTrace();
								}
							}
						}

			- Client 
			
					package com.blanche.Socket;
					
					import java.io.ByteArrayOutputStream;
					import java.io.DataOutputStream;
					import java.net.DatagramPacket;
					import java.net.DatagramSocket;
					import java.net.InetSocketAddress;
					
					public class UDPClient {
						public static void main(String[] args)throws Exception{
							long n = 10000;
							byte[] buf;
						//	String str = "Hello";
							ByteArrayOutputStream bas= new ByteArrayOutputStream();
							DataOutputStream dos = new DataOutputStream(bas);
							dos.writeLong(n);
							buf = bas.toByteArray(); 
					//		System.out.println(buf.length);
								try {
								/**
								 * 模板
								 */
								DatagramPacket dp = new DatagramPacket(buf, buf.length, new InetSocketAddress("localhost",6666));
								DatagramSocket ds = new DatagramSocket(5678);
								ds.send(dp);
								
							} catch (Exception e) {
								e.printStackTrace();
							}
					
						}
					}

- 总结:
	- IP:为每台机器提供独一无二的地址
	- TCP\UDP端口:每个端口依附在ip上,均由四个字节组成
	- 均有固定的模板
***
##GUI(java.awt.*)
- 这一章所涉及的类的分布如下：
	![](http://chuantu.biz/t6/347/1532344767x-1404755439.png)

- Frame（边框）：可以将各种组件和panel装入其中
- panel：也可以装载各种组件，但是不可视
- 布局管理器：可以直接将Container里的内容进行排版，调用container中的额方法setLayout
	- 常用的布局管理器：
		- FlowLayout（水平布局管理器）：为panel默认的布局管理器
		- BorderLayout（边界布局管理器）：为Frame默认的布局管理器。分东西南北居中
		- GridLayour（表格布局管理器）：分几行几列
		- CardLayout ~
		- GridBagLayout ~
- 事件模型：
	- 监听器：实现了某种监听器接口的类
	- 通过监听器来监听某个组件，当这个组件发生了事件之后，将会封装一个Event对象发送给监听器，监听器做出相应的反应。
		- 代码实现：

				package com.blanche.GUI;
				
				import java.awt.Button;
				import java.awt.FlowLayout;
				import java.awt.Frame;
				import java.awt.event.ActionEvent;
				import java.awt.event.ActionListener;
				
				public class TestFrame {
					public static void main(String[] args) {
						MyFrame mf = new MyFrame("Test");
					}
				}
				
				class MyFrame extends Frame{
					public MyFrame(String str) {
						super(str);
						this.setBounds(300, 300, 120, 120);
						this.setLayout(new FlowLayout());
						Button b = new Button("Hello");
						Button c = new Button("Hi");
						this.add(c);
						this.add(b);
						b.addActionListener(new Monitor());
						this.pack();
						this.setVisible(true);
						
					}
				}
				
				class Monitor implements ActionListener{
				
					@Override
					public void actionPerformed(ActionEvent e) {
						System.out.println("你好");
						
					}
					
				}
	- TextField_ActionEvent:通过事件e可以调用文本框内的信息.e.getSource,从而对文本框中的内容进行操作
	- 持有对方引用:
		- 作用:	以此来调用另外一个类里的component
![](http://chuantu.biz/t6/347/1532347722x-1566688718.png)
	- 内部类:
		- 作用: 可以直接调用类的组件,无需引用
![](http://chuantu.biz/t6/347/1532347924x-1404817491.png)
	- Paint(Graphics g)方法:当frame被重画时(第一次显现时、改变窗口大小的时候、盖住再显现的时候),会自动调用paint;
	- repaint：先调用updata再调用paint，此方法的作用在于可以使frame的动态变化可以及时显现出来，因为paint方法只有在frame被重画时才会自动调用，所以我们要主动去调用paint的话只能采用repaint方法。
	- Adapter：当监听的接口需要重写的方法过多时，可以采用其中的Adapter方法，从而来减少重写的方法
	- WindowEvent：
	  可以控制窗口的关闭。Window事件，windowLisenner处理事件：窗口被激活（点击两个窗口的那个窗口），窗口被返回为非激活状态，窗口关闭后的相应，窗口正在关闭时的相应（应该处理这个，WindowClosing），窗口图标化，窗口最大化。

	- KeyEvent：
	  KeyEvent中定义了特别多的静态常量，用来表示键盘上的每个键的值<int类型>（VK代表虚拟的键）。而对于KeyeEvent中可以将封装过来的键盘事件的信息，用方法getKeyCode（返回值为int比较VK_UP等值）

	- 关闭窗口：setVisible（false）；<让窗口不可见>，System.exit（传0或-1在windows    中）；使系统退出。但是这个类只出现在一个方法中，也只调用了一次，所以可以使用局部匿名类，将这个类定义在某个方法中，不需要写继承，只需要new这个类想要的父类，或者接口（本质上是将这个类当做这个类子类的一个对象）。不推荐这样写，但是要认识。