---

title: Java基础学习
date: 2017-12-23 23:03:02
tags:



---

# 真～Java基础

- Java SE：Java Platform， Standard Edition

	- 标准版：各应用平台的基础，桌面开发和低端商务应用的解决方案

- Java EE：Java Platform，Enterprise Edition

	- 企业版：以企业为环境而开发应用程序的解决方案

- Java ME：Java Platform，Micro Edition

	- 微型版：致力于消费产品和嵌入式设备的最佳解决方案

## 体系特点

- 一种纯面向对象的编程语言
- 一种与平台无关（跨平台）的语言
  - 它提供了在不同平台下运行的解释环境
- 一种健壮的语言，吸收了C/C++语言的优点
- 有较高的安全性
  - 自动垃圾回收
  - 强制类型检查
  - 取消指针

## Java跨平台

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181216204618646.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JhaWR1XzQxNjcxNDcy,size_16,color_FFFFFF,t_70)

- 对于不同的运行平台，有不同的JVM（Java Virtual M×××）
	- JVM屏蔽了底层运行平台的差别，实现了“ 一次编译，随处运行”
- 垃圾回收（GC）
	- 不再使用的内存空间应当进行回收
	- 垃圾回收在Java程序运行过程中自动启用，用于检查并释放那些可以被释放的空间

## 程序开发的步骤
- 程序：是为了实现特定目标或解决特定问题而用计算机语言编写的命令序列的集合

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181216210837407.png)

## 第一个Java程序

```java
/**
 *public：共有的
 *class：类
 *Hello：类名
 */
public class Hello{
    public static void main(String[] args){
        System.out.println("hello world");
        // static 静态关键字
        // main 主函数，程序入口方法
        // void 没有返回值
    }
}
```

### 代码格式：

- java 代码的位置
- java 严格区分大小写
- java 是一种自由格式的语言
- 代码分为结构定义语句和功能执行语句
- 功能执行语句的最后必须用分号结束

## Java基本语法

### 变量

- `变量`就是系统为程序分配的一块内存单元，用来存储各种类型的数据
- 根据所存储的数据类型的不同，有各种不同类型的变量
- 变量名代表这块内存中的数据



#### 变量的分类

- 变量的分类：
  1. 按所属的数据类型划分
     1. 基本数据类型
     2. 引用数据类型
  2. 按被声明的位置划分
     1. 局部变量：方法或语句块内部定义的变量
     2. 成员变量：方法外部，类的内部定义的变量



### 数据类型

|   数据类型   | 关键字  | 占用字节 |        取值范围        |  默认值  |
| :----------: | :-----: | :------: | :--------------------: | :------: |
|    布尔型    | boolean |    1     |      true、false       |  false   |
|    字节型    |  byte   |    1     |       -128～127        |    0     |
|    短整型    |  short  |    2     |     -2^15～2^15-1      |    0     |
|     整型     |   int   |    4     |     -2^31～2^31-1      |    0     |
|    长整形    |  long   |    8     |     -2^63～2^63-1      |    0     |
|    字符型    |  char   |    2     |       0～2^16-1        | '\u0000' |
| 单精度浮点型 |  float  |    4     | 1.4013E-45～3.4028E+38 |   0.0F   |
| 双精度浮点型 | double  |    8     | 4.9E-324～1.7977E+308  |   0.0F   |



### 基本数据类型转换

- 自动类型转换：
  - 容量下的类型自动转换成容量大的数据类型
  - byte,short,int->float->long->double
  - byte,short,int不会相互转换，他们三者在计算时会转换成int类型
- 强制类型转换：
  - 容量大的类型转换成容量小的数据类型时，要加上强制转换符
  - long n = 100L;
  - int i = (int)n;
- `boolean 类型不能转换成任何其他数据类型`



### 关键字

|  abstract  |    assert    |  boolean  |   break   |  byte  |
| :--------: | :----------: | :-------: | :-------: | :----: |
|    case    |    catch     |   char    |   class   | const  |
|  continue  |   default    |    do     |  double   |  else  |
|    enum    |   extends    |   final   |  finally  | float  |
|    for     |     goto     |    if     | implement | import |
| instanceof |     int      | interface |   long    | native |
|    new     |   package    |  private  | protected | public |
|   return   |   strictfp   |   short   |  static   | super  |
|   switch   | synchronized |   this    |   throw   | throws |
| transient  |     try      |   void    | volatile  | while  |

**键盘输入：Scanner input = new Scanner(System.in)**

# Java面向对象编程

## 基础

### 类与对象的关系

1. 类表示一个共性的产物，是一个综合的特征，而对象是一个个性的产物，是一个个性的特征
2. 类由属性和方法组成
   - 属性：相当于特征，人的名字等
   - 方法：相当于行为，人会吃饭等



### 定义一个类

```java
class 类名称{
    属性名称;
    返回值类型 方法名（）{}
}
```

- 类的定义
  - 一个类要想真正的进行操作，则必须依靠对象，对象的定义格式如下
  - 类名称 变量名 = new 类名称();



### 封装

1. 封装性是面向对象思想的三大特征之一
2. 封装性就是隐藏实现细节，仅对外提供访问接口
3. 封装有
   - 属性封装
   - 方法封装
   - 类的封装
   - 组件封装
   - 模块化封装



#### 封装的好处

1. 模块化
2. 信息隐藏
3. 代码重用
4. 插件化易于调试
5. 具有安全性



#### 如何封装

```java
class Dog{
    private String Name;
    private int age;
    public void setName(String name){
        this.Name = name;
    }
    public String getName(){
        return this.Name;
    }
    public void setName(int age){
        this.age = age;
    }
    public String getName(){
        return this.age;
    }
    
}
```

**通过使用方法来获取和设置类的属性，而不是让直接操作属性值**

**在set方法中，我们还可以格式化传入的参数，改变其为我们想要的类型**



### 构造方法

- 什么是构造方法？
  - 构造方法就是类构造对象时调用的方法，用于对象的初始化工作
  - 构造方法是实例化一个类的对象时，也即是new的时候，最先调用的方法

- 构造方法的定义
  - 构造方法是在类中定义的，构造方法的定义格式：方法名与类名相同，无返回参数类型

```java
class Dog{
    private String Name;
    private int age;
    // 无参构造函数
    Dog(){
        this(Name, age);
    }
    // 带参构造函数
    Dog(String Name, int age){
        this.setName(Name);
        this.setage(age);
    }
    public void setName(String name){
        this.Name = name;
    }
    public String getName(){
        return this.Name;
    }
    public void setName(int age){
        this.age = age;
    }
    public String getName(){
        return this.age;
    }
}
```

#### 注意事项

1. 每个类默认会有一个无参构造函数
2. 方法名与类名相同，无返回值
3. 构造方法可以用来初始化属性
4. 如果类中又带参的构造方法，那么需要默认的无参构造方法时必须显示的写出来
5. 在构造方法中调用其他的构造方法使用 this(参数) 而且必须在第一句



### 值传递与引用传递

- 实例一，值传递

```java
public class ValueDemo{
    public static void main(String[] agrs){
        int x=10;
        method(x);
        System.out.println("x=" + x);
        // 最后 x 等于 10
    }
    public static void method(int mx){
        mx  = 20;
    }
}
```

- 实例二，引用传递

```java
public class RefDemo1{
    public static void main(String[] args){
        Weapon w = new Weapon();
        method(w);
        System.out.println("weapon age = " + w.age);
        // 最后 w.age 等于 
    }
    public static void method(Weapon w){
        w.age = 5l
    }
}
class Weapon {
    int age = 2;// 
}
```

**如果是自定义的类，那么绝对是引用传递；如果是java自己封装的类，大多是值传递**

**正确的解释是，如果值在 栈 中，那么是值传递；如果值 在 堆中，那么是引用传递**



### static 关键字

- static关键字的作用：
  - 使用static关键字修饰一个属性
    - 声明为static的变量实质上就是一个全局变量
  - 使用static关键字修饰的一个方法
    - 通常是 无需实例化对象就可以调用的方法 类名().方法名()
  - 使用static关键字修饰一个类
    - 普通类不能定义为static，内部类可以

#### 注意

1. 静态变量或方法属于类，而不是对象
2. 所以调用静态变量或方法时直接使用类名调用，而不要用对象调用
3. 静态变量在内存中只会保存一份，由这个类的所有对象共享
4. 静态数据（变量和方法）在第一次使用时即载入内存，知道程序退出
5. 静态方法不能调用非静态属性，反之可以使用（因为静态方法先于非静态属性，方法）



#### 注意

- 声明为static的方法有以下几个限制
  - 他们仅能调用其他的static方法
  - 他们只能访问static数据
  - 他们不能以任何方式引用this或super





![在这里插入图片描述](https://img-blog.csdnimg.cn/20181217002007661.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JhaWR1XzQxNjcxNDcy,size_16,color_FFFFFF,t_70)







# JDBC编程

目前市面上数据库管理系统已经非常多，mysql，Oracle，SQLserver等等
在ODBC出现之前，对这些数据库的访问是一件非常麻烦的事情，因为这些数据库虽然都支持sql，但他们针对自己数据库的访问方法，所以当用户访问不同个的数据库时，就必须使用不同API来编写相应的数据库访问程序

- ODBC（Open Database Connectivity）
  通过ODBC访问不同的数据库，无需对数据库访问程序进行修改，这样ODBC的应用越来越广泛
- JDBC（java data base connectivity）
  按照ODBC的模式来制定的，它是一个通用的底层的支持sql功能的Java API

## JDBC的组成

JDBC提供了两种接口

1. JDBC API
   - 面向开发人员的API
2. JDBC Driver API
   - 面向底层驱动程序开发商的API

### JDBC API

 JDBC API 是一系列的应用编程接口，可以用来进行数据库连接，访问数据等

 `JDBC API`的主要编程接口：

1. DriverManager

- 驱动程序管理类
- 用来装载驱动程序，并为创建数据库链接提供支持

1. Connection

- 是一个接口
- 用来连接某一个指定的数据库

1. Statement

- 是一个接口
- 提供了执行SQL语句，获取查询结果的方法

1. PreparedStatement

- 用于执行预编译的SQL语句

1. ResultSet

- 提供了对接口集进行处理的方法

### JDBC Driver API

主要有四种类型

1. JDBC-ODBC bridge
   - 通过将JDBC的调用全部委托给其他编程接口来实现	
2. 部分java技术的本地API驱动程序
   - 驱动程序部分实现通过JAVA语言
   - 其他的部分则委托给本地的数据库的客户段代码来实现
3. 全部基于java技术的本地API程序
   - 这种驱动程序的实现全部通过Java语言
   - 通常由某个中间件服务器提供
   - 客户端程序可以使用数据库无关的协议和中间件服务器进行通信
   - 中间件服务器再讲客户端的调用转发给服务器进行处理
4. 全部基于java技术的本地协议驱动程序
   - 全部基于java语言
   - 包含了特定数据库的访问协议，使得客户端可以直接同服务器进行通信

## 使用JDBC进行增删改

### 首先建表

- 修改Mysql-WorkBench快捷键
  - 自动补全 ctrl+space
    - 但是和Ubuntu的输入法切换冲突
    - 修改/usr/share/mysql-workbench/data/main_menu.xml文件
    - modifier + Space 就是 Ctrl+space的意思，修改为不冲突的快捷键例如F2
    - 或者 直接 菜单栏 edit->auto complete 启动自动补全
- 创建用户表

```
use jsp_db;
create table tbl_user(
  id int(11) unsigned not null auto_increment,
  name varchar(50) not null default '',
  password varchar(50) not null default '',
  email varchar(50) default '',
  primary key(id)
  )engine=InnoDB default charset=utf8;
```

- 创建地址表

```
CREATE TABLE tbl_address (
  id INT(11) UNSIGNED not null auto_increment,
  city varchar(20) default null,
  country varchar(20) default null,
  user_id int(11) unsigned not null,
  primary key(id)
) engine=InnoDB default charset = utf8; 
```

- 表中插入记录

```
insert into tbl_user(id,name,password,email)
values
(1, 'xiaoming', '123456','xiaoming@qq.com'),
(2, 'xiaozhang', '123456', 'xiaozhang@qq.com');

insert into tbl_address(city, country, user_id)
values
('beijing', 'china', 1),
('tianjin', 'china', 2);
```

### 查询初体验

- JDBC执行流程

![](https://i.imgur.com/4GC8UgG.png)

- Eclise中
  - Alt+ '/' 可以进行生成函数
- 数据库查询

​```
package com.JDBC.Test;

import java.sql.DriverManager;
import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

import com.mysql.jdbc.Driver;

public class JDBCTest {
​	public static void main(String[] args) {
​		String sql = "select * from tbl_user";
​		Connection connection = null;
​		Statement statement = null;
​		ResultSet resultSet = null;
​		

```
	try {
		// 用于注册Mysql JDBC的驱动程序
		// forName 方法用于初始化参数指定的类，并创建一个对应的实例对象
		Class.forName("com.mysql.jdbc.Driver");
		// 这里url 指定了 数据库的 地址 端口 以及具体访问的库名
		String url = "jdbc:mysql://localhost:3306/jsp_db";
		String user = "root";
		String password = "root";
		// 获取Mysql 数据库的连接 这里使用的是 DriverManage 的 getConnection 方法
		connection = DriverManager.getConnection(url, user, password);
		// 创建一个Statement对象
		statement = connection.createStatement();
		// 使用Statement对象的executeQuery方法来发送Sql语句
		// executeQuery 方法返回一个 ResultSet对象
		resultSet = statement.executeQuery(sql);
		// 遍历ResultSet对象
		while (resultSet.next()) {
			System.out.println(resultSet.getInt("id"));
			System.out.println(resultSet.getString("name"));
			System.out.println(resultSet.getString("password"));
			System.out.println(resultSet.getString("email"));
		}
	} catch (Exception e) {
		// TODO: handle exception
		e.printStackTrace();
	} finally {
		try {
			// 关闭ResultSet对象的结果集
			resultSet.close();
		} catch (Exception e2) {
		}
		try {
			// 关闭Statement对象
			statement.close();
		} catch (Exception e2) {
		}
		try {
			// 关闭数据库连接
			connection.close();
		} catch (Exception e2) {
		}
	}
}
```

}

​```

### 增删改查

- 首先写一个Connection的函数，这样执行就不用每次都写 那几条固定语句

```
public static Connection getConnection() {
	Connection conn = null;
	try {
		Class.forName("com.mysql.jdbc.Driver");
		// 这里url 制定了 访问数据库的 地址 端口 以及 具体 库的名字
		String url = "jdbc:mysql://localhost:3306/jsp_db";
		String user = "root";
		String password = "root";
		// 获取Mysql 数据库的连接 这里使用的是 DriverManage 的 getConnection 方法
		conn = DriverManager.getConnection(url, user, password);
		
	} catch (Exception e) {
		// TODO: handle exception
	}
	return conn;
}
```

- `然后就是增删改的函数了`
- 增

```
public static void insert() {
	Connection conn = getConnection();
	try {
		// 存储sql语句，用来向用户表中插入记录
		String sql = "insert into tbl_user(name,password,email)" 
					+ "values" 
					+"('Tom', '123456','Tom@qq.com'),('Anny', '123456', 'Anny@qq.com')";
		Statement st = conn.createStatement();
		// Statement中的executeUpdate方法，可以执行DML语句，包括insert update 以及 delete
		// 也可以执行没有返回结果的语句 例如：DDL语句 
		// 参数是一个字符串形式的sql语句，如果执行的是DML语句，那么返回影响的记录条数，如果是DDL语句则返回0
		// 会抛出sqlExcuption 以及 sqlTimeOut 的异常
		int count = st.executeUpdate(sql);
		System.out.println("向表中插入了" + count + "条语句");
		conn.close();
	} catch (Exception e) {
		// TODO: handle exception
		e.printStackTrace();
	}
}
```

- 改

```
public static void update() {
	Connection conn = getConnection();
	try {
		// 存储sql语句，用来向用户表中插入记录
		String sql = "update tbl_user set email='Tomm@163.com' where name = 'Tom'";
		Statement st = conn.createStatement();
		// Statement中的executeUpdate方法，可以执行DML语句，包括insert update 以及 delete
		// 也可以执行没有返回结果的语句 例如：DDL语句 
		// 参数是一个字符串形式的sql语句，如果执行的是DML语句，那么返回影响的记录条数，如果是DDL语句则返回0
		// 会抛出sqlExcuption 以及 sqlTimeOut 的异常
		int count = st.executeUpdate(sql);
		System.out.println("向表中更新了" + count + "条语句");
		conn.close();
	} catch (Exception e) {
		// TODO: handle exception
		e.printStackTrace();
	}
}
```

- 删

```
public static void delete_db() {
	Connection conn = getConnection();
	try {
		// 存储sql语句，用来向用户表中插入记录
		String sql = "delete from tbl_user where name='Tom'";
		Statement st = conn.createStatement();
		// Statement中的executeUpdate方法，可以执行DML语句，包括insert update 以及 delete
		// 也可以执行没有返回结果的语句 例如：DDL语句 
		// 参数是一个字符串形式的sql语句，如果执行的是DML语句，那么返回影响的记录条数，如果是DDL语句则返回0
		// 会抛出sqlExcuption 以及 sqlTimeOut 的异常
		int count = st.executeUpdate(sql);
		System.out.println("向表中删除了" + count + "条语句");
		conn.close();
	} catch (Exception e) {
		// TODO: handle exception
		e.printStackTrace();
	}
}
```

- 之后只需要在 main 函数中 调用inset 等 方法就 能插入 修改 删除了
- 需要注意的是，不要把sql语句写错
- 执行之后，控制台会输出修改的语句的个数
- main方法

```
public static void main(String[] args) {
	//insert();
	//update();
	delete_db();
}
```

## JDBC事务处理

数据库是一个多用户使用的共享资源
当多个用户使用数据库存取资源的时候，就会产生不同用户存取同一数据的情况
因此需要控制并发

- 原子性
  - 事务中包含的操作都被看做是一个逻辑单元
  - 这个逻辑单元的操作 要么全部成功 要么全部失败
  - 事务中所有元素作为一个整体，提交或回滚
  - 事务的所有元素是不可分割的，是一个完整的操作
- 一致性
  - 事务开始之前和事务结束以后，数据库都处于一致性状态
  - 数据库的完整性约束，没有被破坏
- 隔离性
  - 对数据库进行修改的多个事务，是彼此隔离的
  - 事务必须是独立的，不应该以任何形式影响其他事务
- 持久性
  - 事务完成之后，对于系统的影响是永久的
  - 该修改真实的修改了数据库，即使系统出现故障也会一直保留

### 事务语句

- 开始事务
  - Begin transaction
- 提交事务
  - Commit transaction
- 回滚事务
  - Rollback transaction

举个例子：
​	我们有 user 和 address 表
​	在 address 表中 插入 Tom 的地址信息
​	在 user 表中 插入 id 为 1 的 Tom的个人信息

- 不难发现，由于user表中原来就有id 为 1 的信息，所以user表插入失败
- 但是，address 表却可以插入，因为没有主键冲突
- 这就是 `完整性 缺失`

### 代码实例

​```
public class TransAction {

```
public static Connection getConnection() {
	Connection conn = null;
	try {
		Class.forName("com.mysql.jdbc.Driver");
		String url = "jdbc:mysql://localhost:3306/jsp_db";
		String user = "root";
		String password = "root";
		conn = DriverManager.getConnection(url, user, password);
		
	} catch (Exception e) {
	}
	return conn;
}
// 使用 throws SQLException 来捕获异常，因为如果数据插入失败的时候会抛出异常
// 通过 这种方法 将异常传递给 上层函数 通过上层函数捕捉异常 进行回滚
public static void insertUser(Connection conn) throws SQLException {
	String sql = "insert into tbl_user(name,password,email)" 
			+ "values" 
			+"('Tom', '123456','Tom@qq.com'),('Anny', '123456', 'Anny@qq.com')";
	Statement st = conn.createStatement();
	int count = st.executeUpdate(sql);
	System.out.println("向表中插入了" + count + "条语句");
}

public static void insertAddress(Connection conn) throws SQLException {
	String sql = "insert into tbl_address(id,city,country)" 
			+ "values" 
			+"(1, 'beijing','china'),(2, 'tianjing', 'china')";
	Statement st = conn.createStatement();
	int count = st.executeUpdate(sql);
	System.out.println("向表中插入了" + count + "条语句");
}

public static void main(String[] args) {
	Connection conn = null;
	try {
		conn = getConnection();
		//关闭自动提交
		conn.setAutoCommit(false);
		insertAddress(conn);
		insertUser(conn);
		
		conn.commit();
	} catch (SQLException e) {
		System.out.println("=====偶哟，捕获到SQL异常了呢====");
		e.printStackTrace();
		try {
			// 如果捕获到异常 那么说明数据插入失败，则要回滚到插入之前的状态
			// 避免出现，部分插入，部分没插入 所导致的 完整性缺失问题
			System.out.println("====现在开始数据回滚呢，请等会哦====");
			conn.rollback();
			System.out.println("====回滚成功呢，请再看看是哪里的代码有问题呢====");
		} catch (Exception e2) {
			e2.printStackTrace();
		}
	} finally {
		try {
			// 如果 conn 连接 不为空的时候，最后要关闭连接
			if (conn != null) {
				conn.close();
			}
		} catch (Exception e3) {
			e3.printStackTrace();
		}
	}
}
```

}
​```

## JDBC 优化

前面的写法都是直接将 数据库链接，用户名，密码等直接内嵌到代码中
但是这样的写法其实重用性特别差，一旦修改了密码那么所有的文件都需要修改

这个时候最好的方法就是写一个 `配置文件`，然后所有的数据链接都用这个配置文件
这里 默认 `配置文件`的后缀是 `.properties`

```
driver=com.mysql.jdbc.Driver
dburl=jdbc\:mysql\://localhost\:3306/jsp_db
user=root
password=root
```

直接写上面的内容就行了 不需要上面花里胡哨的
​

```
​package com.JDBC.Test;
​	
import java.io.InputStream;
import java.sql.Connection;
import java.sql.DriverManager;
import java.util.Properties;

import com.mysql.jdbc.Driver;

public class DataConnectFactory {
	private static String driver;
	private static String dburl;
	private static String user;
	private static String password;
	private static final DataConnectFactory factory = new DataConnectFactory();
	private Connection connection;
	static {
		Properties prop = new Properties();
		try {
			InputStream in = DataConnectFactory.class.getResourceAsStream("dbconfig.properties");
			prop.load(in);
		} catch (Exception e) {
			System.out.println("==配置问价出错了呢==");
		}
		
		driver = prop.getProperty(driver);
		dburl = prop.getProperty(dburl);
		password = prop.getProperty(password);
		user = prop.getProperty(user); 
	}
	//定义默认构造函数
	private DataConnectFactory(){
		
	}
	// 单例模式
	public static DataConnectFactory getInstance() {
		return factory;
	}
	
	public Connection makeConnection() {
		try {
			Class.forName(driver);
			connection = DriverManager.getConnection(dburl, user, password);
		} catch (Exception e) {
			e.printStackTrace();
		}
		return connection;
	}
}
```

这里使用了静态代码块



# Java 上传下载 文件

## 上传

- 文件上传的作用
  - 上传照片
  - 上传文档
  - 上传简历
  - ……
- 文件上传对页面的要求
  - 必须使用表单，而不是超链接
  - 表单的method 必须是 POST，而不能是GET
  - 表单的enctype 必须是 multipart/form-data;
  - 在表单中添加file表单字段，即&lt;input typt="file" name="file" .../>



```html
<form action="..." method="post" enctype="multipart/form-data">
	用户名：<input type="text" name="username" />
    照  片：<input type="file" name="picture" />
   	<input type="submit" value="提交" />
</form>
```





- 上传对Servlet限制
  - request.getParametere("")在表单为 enctype="multipart/form-data"时作废，返回null
    - `整个表单都不能用`
  - 调用 request.getInputStream(); 方法，返回 ServletInputStream，返回数据包含整个请求的体
- 多部件表单的体
  - 每个分开的多个部件，即一个表单项一个部件
  - 一个部件中有自己的请求头和空行，还有请求提
  - 普通表单项：
    - 一个头：Content-Disposition：包含name="xxx"，即表达项名称
    - 一个体：表单项的值
  - 文件表单项：
    - 两个头：
      - Content-Disposition：包含name="xxx"，表单项名称，还有一个filename，即上传文件的名称
      - Content-Type：它是上传文件的MIME类型，例如：image/pjpeg，.....



### Servlet写法

```java
protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
	// TODO Auto-generated method stub
	
	request.setCharacterEncoding("UTF-8");
	response.setContentType("text/html;charset=utf-8");
	
	ServletInputStream in = request.getInputStream();
	String s = IOUtils.toString(in);
	System.out.println(s);
}
```

- 这里的 IOUtils 是 commons-io.jar 包，你需要手动导入到路径中
  - `这里的jar包，一定要放到lib 文件夹中，否则无效，我也不知道为啥`
- 使用 commons-fileupload.jar 和 commons-io.jar 工具包
  - 帮我们解析 request 中上传的数据
  - 解析后的结果是一个表单项数据，封装到一个FileItem对象中
  - 调用FileItem的方法即可获取数据



### 上传三步

- 相关类
  1. 工厂：DiskFileItemFactory	
  2. 解析器：ServletFileUpload
  3. 表单项：FileItem
- 创建工厂
  - DiskFileItemFactory factory = new DiskFileItemFactory();
- 创建解析器
  - ServletFileUpload sfu = new ServletFileUpload(factory);
- 使用解析器来解析request，得到FileItem集合
  - List&lt;FileItem> fileItemList = sfu.parseRequest(request);
- FileItem 的 API
  - boolean isFormField() 是否为普通表单项
    - true 为普通表单项
    - false 文件表单项
  - String getFileName()  返回当前表单项的名称
  - String getString(String charset) 返回表单项的值（不适用于文件表单项）
  - String getName() 返回上传的文件名称
  - long getSize() 返回上传文件的字节数
  - InputStream getInputStream() 返回对应文件的输入流
  - void write(File destFile) 将上传的文件内容保存到指定的文件中
    - 如果文件存在，则替换文件
    - 如果文件不存在，则创建文件
- Servlet文件，注意`这里导入的是 org.apache.commons.fileupload 包，并且io包和fileupload 包一定要放到WEB-INF 的lib中`

```java
package up;

import java.io.File;
import java.io.IOException;
import java.util.List;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.apache.commons.fileupload.*;
import org.apache.commons.fileupload.disk.DiskFileItemFactory;
import org.apache.commons.fileupload.servlet.ServletFileUpload;
/**
 * Servlet implementation class upPic
 */
@WebServlet("/upPic")
public class upPic extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    /**
     * @see HttpServlet#HttpServlet()
     */
    public upPic() {
        super();
        // TODO Auto-generated constructor stub
    }

	/**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		System.out.println("get");
	}

	/**
	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		request.setCharacterEncoding("utf-8");
		response.setContentType("text/html;charset=utf-8");
		/*
		 *上传三步
		 *1. 得到工厂
		 *2. 通过工厂创建解析器
		 *3. 解析request，得到FileItem集合
		 *4. 遍历FileItem集合，调用其API 
		 */
		DiskFileItemFactory factory = new DiskFileItemFactory();
		ServletFileUpload sfu = new ServletFileUpload(factory);
		try {
			List<FileItem> fileItems = sfu.parseRequest(request);
			// 我们这里明确知道只有两个表单项，所有就不便利数组了
			//FileItem fil1 = fileItems.get(0);// 普通表单项
			FileItem fil2 = fileItems.get(1);// 上传的图片表单项
			System.out.println("Content-Type : " + fil2.getContentType());
			System.out.println("size : " + fil2.getSize());
			System.out.println("filename : " + fil2.getName());
			File picture = new File("/home/cong/picture.jpg");
			fil2.write(picture);
		} catch (Exception e) {
			// TODO: handle exception
		}			
	}

}

```

- jsp文件

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<form action="upPic" method="post" enctype="multipart/form-data">
		用户名：<input type="text" name="username" />
	    照  片：<input type="file" name="picture" />
	   	<input type="submit" value="提交" />
	</form>
</body>
</html>
```



### 上传的细节

- 把上传的文件放到`WEB-INF`目录下
  - 如果没有把用户的文件存放到WEB-INF目录下，那么用户可以通过浏览器直接访问上传的文件，这个是非常危险的
    - 加入用户上传了一个a.jsp文件，再通过浏览器链接访问a.jsp，那么就会执行a.jsp，而如果jsp文件中有"shutdown -h now"，那么后果嘛
  - 通常我们会在WEB-INF目录下创建一个uploads目录，来存放上传的文件，而在Servlet中找到这个目录需要使用ServletContext 的 getRealPath(String) 方法
    - ServletContext servletContext = this.getServletContext();
    - String savepath = servletContext.getRealPaht("/WEB-INF/uploads");
- 文件名称相关问题
  - 有点浏览器上传的文件名是绝对路径，这需要切割
  - 乱码问题，文件名乱码
    - request.serCharacterEncoding("utf-8")
  - 上传文件同名问题
  - 目录打散问题
    - 一个目录不能存放过多文件
    - 一般一个目录存放1000个文件就是上限
    - 如果文件太多就会导致打开卡顿
    - 打散方法很多：
      1. 按 日期 生成 文件夹
      2. 按 首字母 分 文件夹
  - 上传的单个文件的大小限制
    - ServletFileUpload类的setFileSizeMax(long)就可以了
    - 参数是上传文件的上限字节数
    - 一旦文件超过上限就会抛出FileUploadBase.FileSizeLimitExceededException异常
  - 缓存大小与临时目录



## 下载文件

- 下载就是向客户端响应字节数据
  - 原来响应的都是HTML字符数据
  - 现在响应字节数据
  - 把一个文件变成字节数组，使用response的流(outputstream)响应给浏览器
- 下载的要求
  - 两个头，一个流
    - 头：响应头
    - 流：字节流
  - 头1：Content-Type：
    - 你传递给客户端的文件是什么MIME类型
    - 例如：image/pipeg
  - 头2：Content-Disposition：
    - 一般来说，如果不设置头，那么默认不弹出下载框
    - 默认值为：inline，在浏览器窗口中打开，打不开就弹窗
    - 修改为   "attachment;filename=***"	
  - 流：要下载的文件数据

### Servlet代码演示

- Java代码

```
package com.upload.pic;

import java.io.FileInputStream;
import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.ServletOutputStream;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.swing.filechooser.FileNameExtensionFilter;

import org.apache.tomcat.util.http.fileupload.IOUtils;

/**
 * Servlet implementation class DownLoad
 */
@WebServlet("/DownLoad")
public class DownLoad extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    /**
     * @see HttpServlet#HttpServlet()
     */
    public DownLoad() {
        super();
        // TODO Auto-generated constructor stub
    }

	/**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		System.out.println("get");
		/**
		 * 两个头一个流
		 * 1. content-type
		 * 2. content-dsidposition
		 * 3. 下载文件的数据流
		 */
		String wen_inf_path = getServletContext().getRealPath("/WEB-INF");
		String filename = "3.Servlet获取到上传表单的数据.mp4";
		String filepath = wen_inf_path + "/3.Servlet获取到上传表单的数据.mp4";
		filename = new String(filename.getBytes("GBK"),"ISO-8859-1");
		String contentType = this.getServletContext().getMimeType(filepath);//通过文件名称获取mime类型
		String contentDisposition = "attachment;filename=" + filename;//带中文则乱码，最好是英文
		System.out.println(filename);
		System.out.println(filepath);
		FileInputStream input = new FileInputStream(filepath);
		
		response.setHeader("Content-Type", contentType);
		response.setHeader("Content-Disposition", contentDisposition);
		
		// 获取绑定了客户端的流
		ServletOutputStream output = response.getOutputStream();
		
		IOUtils.copy(input, output);
		
		input.close();
		
	}

	/**
	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		System.out.println("post");
	}

}


```

### 下载的细节

- 显示在下载框中的中文名称会出现乱码
  - IE浏览器会出乱码
  - 火狐会出现乱码
- 解决方案
  1. 使用浏览器的编码
     - Firefox 使用 Base64编码
     - 其他大部分浏览器都是用 URL 编码
  2. 通用方案
     - filename = new String(filename.getBytes("GBK"),"ISO-8859-1");
     - 虽然不懂为什么，但是就是有用
     - 注意，上述代码中分 filepath 和 filename
       - filepath 为 文件路径 不能 改变编码方式
       - filename 为 文件名称 可以 修改编码方式



## 发送Mail

```java
package com.mail.send;

import java.util.Properties;

import javax.mail.Authenticator;
import javax.mail.MessagingException;
import javax.mail.PasswordAuthentication;
import javax.mail.Session;
import javax.mail.Transport;
import javax.mail.internet.AddressException;
import javax.mail.internet.InternetAddress;
import javax.mail.internet.MimeMessage;
import javax.mail.internet.MimeMessage.RecipientType;
public class SendMail {
	public static void SendYourMail(String address) throws AddressException, MessagingException{
		/**
		 * 创建连接
		 */
		Properties properties = new Properties();
		properties.setProperty("mail.host", "smtp.163.com");
		properties.setProperty("mail.smtp.auth", "true");// 制定验证为True 是否需要身份验证
		properties.setProperty("mail.transport.protocol", "SMTP");
		
		Authenticator auth = new Authenticator() {
			@Override
			protected PasswordAuthentication getPasswordAuthentication(){
				return new PasswordAuthentication("SZMT_TEAM", "szmt317");
                // 这个szmt317 不是我163的密码 而是我的
			}
		};
		Session session = Session.getInstance(properties, auth);
		
		// 编辑邮件
		
		MimeMessage msg = new MimeMessage(session);					
		msg.setFrom(new InternetAddress("SZMT_TEAM@163.com"));		//设置发件人
		msg.setRecipients(RecipientType.TO, address);	//设置收件人，正常发送
		msg.setRecipients(RecipientType.CC, address);	//设置收件人，抄送（即再发送一份样的）
		msg.setRecipients(RecipientType.BCC, address);	//设置收件人，暗送
		
		msg.setSubject("测试，测试，测试"); // 邮件的标题
		msg.setContent("你的验证码是 ****", "text/html;charset=utf-8");	//邮件内容
		
		// 发送邮件
		Transport.send(msg);
		System.out.println("发送成功");
	}

}
```

- 这里的问题就是 你的 163 邮箱需要开启服务
  - 设置 客户端授权密码 上述的 Authenticator 中并不是我的163账户密码，而是授权密码








