---
title: MyBatis学习
date: 2017-11-22 19:13:24
tags:
---
# MyBatis

- MyBatis 不同与 Hiberanat
- MyBatis 比较轻 而 Hiberanat 比较重
`这里的 轻 代表的是 方便学习，开发，维护，简单`

## 初识MyBatis
### MyBatis介绍

#### 历史
iBATIS = "internet" + "abatis" 的组合
是Apache公司的一个开源项目，这个项目是做软件加密的
abatis 翻译过来是 路障，铁丝网的意思
后来转型成为一个基于Java的持久层框架

- 持久层
	- Java中对象有两种状态
		- 瞬态
		- 持久态
	- 瞬态
		- new 了一个对象 用完之后垃圾回收
		- 对象中的属性状态没有保存
	- 持久态
		- 对象的状态属性保持住了
		- 保存的方法又很多种 ：文件，数据库等
	- 如果保存在数据库中，我们可以用JDBC来访问，操作
	- 但是JDBC不是很方便，这样就产生了一种框架，叫做持久层框架	

iBatis 后来改名为 MyBatis
因为跳槽，从Apache 跳槽到 Google 再到 Github

#### 特点
- 开源的优秀持久层框架
- 轻
- SQL语句和代码分离
- 面向配置的编程（面向切片的编程）
- 增强程序的可维护性，可扩展性
- 良好支持复杂数据映射
- 使用JDBC我们会拼装SQL语句，这种语句并不安全，容易造成SQL注入
- MyBatis 使用 动态SQL 技术，替换拼装SQL语句

### MyBatis环境搭建

#### 下载 
[MyBatis下载地址](https://github.com/mybatis/mybatis-3/releases) 

- 解压压缩文件
	- 其中mybatis-*.*.*.jar 是 MyBatis 的主jar包
	- lib/ 文件夹是他的部分依赖包，毕竟曾经是Apache的项目
	- mybatis-*.*.*.pdf 是 说明文档
#### 导入工程

- 导入 mybatis-*.*.*.jar 包
- 导入 lib 中相关的 jar
- 导入 mysql 数据库 针对于 JDBC 的jar包

#### 日志配置
- 为什么配置日志
	-当我调试或者观察程序的时候，是通过输出的SQL语句看一下程序的执行状况
	- MyBatis 是通过 日志来完成的，所以要配置日志

- 加入日志配置文件log4.properties
- 改写日志输出级别为debug级别
	- MyBatis 在日志输出的时候，SQL语句一定实在debug级别才能输出
	- 如果是inform级，则不输出
	
```xml

	log4j.rootLogger=DEBUG, Console

	#Console
	log4j.appender.Console=org.apache.log4j.ConsoleAppender
	log4j.appender.Console.layout=org.apache.log4j.PatternLayout
	log4j.appender.Console.layout.ConversionPattern=%d [%t] %-5p [%c] - %m%n

	log4j.logger.java.sql.ResultSet=INFO
	log4j.logger.org.apache=INFO
	log4j.logger.java.sql.Connection=DEBUG
	log4j.logger.java.sql.Statement=DEBUG
	log4j.logger.java.sql.PreparedStatement=DEBUG
```

### MyBatis工作流程

#### 工作流程的步骤
1. 读取配置文件
	- 读取的是基本配置文件
	- 包含的是连数据库的相关信息
2. 生成SqlSessionFactory
	- Sqlsession的工厂，用于建立与数据库之间的会话
3. 建立SqlSession
	- 用于执行Sql语句
4. SqlSession 调用MyBatis提供的API
5. 查询MAP配置
	- Map配置文件里面存放的是sql语句
6. 返回结果
	- 不同的sql语句返回不同的结果
7. 关闭SqlSession
	
#### 工作流程的配置文件
- 基本配置文件

```xml
 
	<?xml version="1.0" encoding="UTF-8" ?>
	<!DOCTYPE configuration
	    PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
	    "http://mybatis.org/dtd/mybatis-3-config.dtd">

	<configuration>
	
	  <environments default="development"> # 一个environments 中有多个 environment 
	    <environment id="development"> # 一个environment 代表连接的一个数据库 里面的是数据库的信息
	      <transactionManager type="JDBC"> #事务由谁来管理 这里是JDBC管理
	      </transactionManager>
	      <dataSource type="POOLED"> #是否用连接池 或者 第三方child
		<property name="driver" value="com.mysql.jdbc.Driver"/> #驱动
		<property name="url" value="jdbc:mysql://localhost:3306/jikebook"/> #链接路径
		<property name="username" value="root"/> # 用户名
		<property name="password" value="123"/> # 密码
	      </dataSource>
	    </environment>
	  </environments>

	  <mappers>
		    <mapper resource="jike/book/map/jikeUser.xml"/>　＃　
	  </mappers>

	</configuration>

```
包含着连数据库的基本信息
- 链接数据库的信息
	- <environments>
	- 就是环境，封装的就是连数据库的信息
- map配置文件的数据位置
	- <mappers>
	- 映射map配置文件的路径信息
	
- map配置文件   
  
```xml
	<?xml version="1.0" encoding="UTF-8" ?>


	<!DOCTYPE mapper
	    PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
	    "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

	<mapper namespace="/">

	  <select id="findById"  parameterType="int"  resultType="jike.book.pojo.JiKeUser">
	  	  select * from jikeUser where id=#{id}
	  </select>
	  
	</mapper>
```

#### SqlSessionFactory, SqlSession

- SqlSessionFactory代表着跟数据库之间的连接
- 连上去之后自然要进行各种各样的操作
- 各种各样的操作是由SqlSession去执行的
- SqlSession是由SQLSessionFactory来建立的

- 生命周期
	- SqlSessionFactory的生命周期是程序级的
		- 一般一个MyBatis程序只有一个SqlSessionFactory
		- 程序开始的时候建立，结束的时候才会消亡
	- SqlSession 是过程级的
		- 比如在一个方法当中会建立一个SqlSession，执行完后SqlSession就应该关闭了
		
- 建立的代码


```java
  
	SqlSessionFactory sqlMapper = new SqlSessionFactoryBuilder().build(reader);
	# reader 是一个输入流，是基本配置文件的路径的流
	SqlSession session = sqlMapper.openSession();
```

#### Map文件

##### 基本配置文件引用map文件
- 相对路径引用


```xml

	<mappers>
		<mapper resource="test/book/map/TestUser.xml"/>
	</mappers>

```
- 绝对路径引用


```xml

	<mappers>
		<mapper url="file:///var/sqlmaps/AuthorMapper.xml" />
	</mappers>  

```
- 包路径引用
```xml

	<package name="com.Test.mybatis.mapperinterface" />  

```

##### 什么是map文件

```xml

	<select id="findById" parameterType="int" resultType="Test.book.pojo.TestUser">
		select * from TestUser where id=#{id}
	</select>  

```
- 上述标签中的id，这是找到这个sql语句的标示
- 上述标签中的parameterType是参数类型
- 上述标签中的resultType指的是返回类型
- 上述的sql语句中id = #{id}，'#'后面的内容代表一个参数

#### 看实战，学操作，我有知识我自豪

##### 建立数据库

```java

	create database jikebook;

	use jikebook;

	create table jikeUser(
		id int not null auto_increment,
	    userName varchar(20) ,
	    password varchar(20) ,
	    primary key(id)
	)engine=InnoDB default charset=utf8;

	insert into jikeUser(id, userName, password)
	values
	(1, 'hello world', '');

```

##### 查询代码 
```java

		TestUser temp = session.selectOne("findById", 1); # 第一个参数是map配置中的id，第二个参数是 mysql数据库中 的id
		System.out.println("name = " +  temp.getUseName());  

```

- jikeUser.xml


```xml

	<?xml version="1.0" encoding="UTF-8" ?>
	<!DOCTYPE mapper
	    PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
	    "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

	<mapper namespace="test.book.map">

		<select id="findById" parameterType="int" resultType="test.book.pojo.TestUser">
			select * from jikeUser where id=#{id}
		</select>

	</mapper>  

```

- MyBatisConfig.xml

```xml

	<?xml version="1.0" encoding="UTF-8" ?>

	<!DOCTYPE configuration
	    PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
	    "http://mybatis.org/dtd/mybatis-3-config.dtd">

	<configuration>

	  <environments default="development">
	    <environment id="development">
	      <transactionManager type="JDBC">
	      </transactionManager>
	      <dataSource type="POOLED">
		<property name="driver" value="com.mysql.jdbc.Driver"/>
		<property name="url" value="jdbc:mysql://localhost:3306/jikebook"/>
		<property name="username" value="root"/>
		<property name="password" value="root"/>
	      </dataSource>
	    </environment>
	  </environments>

	  <mappers>
	  	<mapper resource="test/book/map/jikeUser.xml" />
	  </mappers>

	</configuration>  
 

```

- TestUser.java


```java

	package test.book.pojo;

	public class TestUser {
		private int id;
		private String userName;
		private String password;
		
		public int getId() {
			return id;
		}
		public void setId(int id) {
			this.id = id;
		}
		public String getUserName() {
			return userName;
		}
		public void setUserName(String userName) {
			this.userName = userName;
		}
		public String getPassword() {
			return password;
		}
		public void setPassword(String password) {
			this.password = password;
		}
	}  


```

- MainTest.java


```java

		package test.book.pojo;

		import java.io.IOException;
		import java.io.Reader;

		import org.apache.ibatis.io.Resources;
		import org.apache.ibatis.session.SqlSession;
		import org.apache.ibatis.session.SqlSessionFactory;
		import org.apache.ibatis.session.SqlSessionFactoryBuilder;

		public class Test {

			public static void main(String[] args) {
				// TODO Auto-generated method stub
				String reource = "test/book/map/MyBatisConfig.xml";
				Reader reader = null;
				SqlSession session;
				try {
					reader = Resources.getResourceAsReader(reource);
				} catch (IOException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				session.rollback();//回滚
				}
				System.out.println("111");
				SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(reader);
				System.out.println("222");
				session =sqlSessionFactory.openSession();
				TestUser temp = session.selectOne("findById", 1);
				System.out.println(temp.getUserName());
			}

		}  


```

## MyBatis 基础操作
### 增删改

- 影响行数


#### insert

```xml

	<insert id="insertUser" parameterType="TestUser" statementType="PREPARED" keyProperty="id" useGeneratedKeys="true">
		insert into JikeUser (userName, password) values	(#{userName, jdbcType=VARCHAR}, #{password, jdbcType=VARCHAR})
	</insert>  

```

- 上述代码中
	- StatementType="PERPARED" 代表这是一个 预处理的SQL语句
	- parameterType="TestUser" 代表传入的类
		- 这里传入的应该是一个全路径名称，即com.jike.book.JikeUser 
		- 这里使用了typeAliases 标记 来定义了别名 简化了代码的书写
	- keyProperty 代表 哪一个 参数 是主键

` 上一个大类中完成的基本配置中加上`

```xml  

	  <typeAliases> 
	  	<typeAlias alias="TestUser" type="test.book.pojo.TestUser" />
	  </typeAliases>

```

---

> 着重强调！！！  
> 着重强调！！！  
> 着重强调！！！  

- Alias要写在environments前面，先定义别名，在配置环境，否则会报错  

- 切记 切记

##### 下面介绍代码

- TestUser类依旧不变

- MainTest类修改


```java

	package test.book.pojo;

	import java.io.IOException;
	import java.io.Reader;

	import org.apache.ibatis.io.Resources;
	import org.apache.ibatis.session.SqlSession;
	import org.apache.ibatis.session.SqlSessionFactory;
	import org.apache.ibatis.session.SqlSessionFactoryBuilder;

	public class Test {

		public static void main(String[] args) {
			// TODO Auto-generated method stub
			String reource = "test/book/map/MyBatisConfig.xml";
			Reader reader = null;
			SqlSession session;
			try {
				reader = Resources.getResourceAsReader(reource);
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(reader);
			session =sqlSessionFactory.openSession();
			try {
				TestUser testUser = new TestUser();
				testUser.setUserName("laoziniubi");
				testUser.setPassword("123456");
				session.insert("insertUser", testUser);
				session.commit();//提交sql语句
			} catch (Exception e) {
				e.printStackTrace();
				session.rollback();//回滚
			}finally {
				session.close();
			}
		}

	}  


```

- jikeUser.xml


```xml

	<?xml version="1.0" encoding="UTF-8" ?>
	<!DOCTYPE mapper
	    PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
	    "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

	<mapper namespace="test.book.map">

		<select id="findById" parameterType="int" resultType="test.book.pojo.TestUser">
			select * from jikeUser where id=#{id}
		</select>
		<insert id="insertUser" parameterType="TestUser" statementType="PREPARED" keyProperty="id" useGeneratedKeys="true">
			insert into jikeUser (userName, password) values	(#{userName}, #{password})
		</insert>

	</mapper>  

```

- MyBatisConfig.xml

```xml

	<?xml version="1.0" encoding="UTF-8" ?>

	<!DOCTYPE configuration
	    PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
	    "http://mybatis.org/dtd/mybatis-3-config.dtd">

	<configuration>

		
	  <typeAliases>
	  	<typeAlias alias="TestUser" type="test.book.pojo.TestUser" />
	  </typeAliases>

	  <environments default="development">
	    <environment id="development">
	      <transactionManager type="JDBC">
	      </transactionManager>
	      <dataSource type="POOLED">
		<property name="driver" value="com.mysql.jdbc.Driver"/>
		<property name="url" value="jdbc:mysql://localhost:3306/jikebook"/>
		<property name="username" value="root"/>
		<property name="password" value="root"/>
	      </dataSource>
	    </environment>
	  </environments>
	  
	  <mappers>
	  	<mapper resource="test/book/map/jikeUser.xml" />
	  </mappers>

	</configuration>  


```

#### Update

```xml

		<update id="updateUser" parameterType="TestUser">
			update jikeUser set userName=#{userName, jdbcType=VARCHAR},password=#{password,jdbcType=VARCHAR} where id=#{id,jdbcType=INTEGER}
		</update>  

```

- 上述代码中
	- parameterType 仍然利用别名
	- jdbcType 是 MyBatis 中 自动类型转换的一种设定
		- java当中的数据类型 和 数据库当中的数据类型需要一个转换
		- 这种转换 往往是自动完成的，但当不能自动转换的时候，就需要进行手动转换

##### 下面介绍代码

- 就不介绍xml了，和之前一样，就加上 update 标签就行了
- 写一下调试代码


```java

	try {
		TestUser testUser = new TestUser();
		testUser.setUserName("laoziniubi");
		testUser.setPassword("666666");
		testUser.setId(2);
		session.update("updateUser", testUser);
		session.commit();//提交sql语句
	} catch (Exception e) {
		e.printStackTrace();
		session.rollback();//回滚
	}finally {
		session.close();
	}  

```

#### delete(使用注解方式)
- 在map.xml的包中新建一个interface接口，名为JikeUserMapInterface

```java

	package test.book.map;

	import org.apache.ibatis.annotations.Delete;

	public interface JikeUserMapInterface {
		@Delete("delete from jikeUser where id=#{id}")
		public void deleteUder(int id);
	}  


```

- 在基本配置文件的mapper 标签中添加  

```xml

	  <mappers>  
	  	<mapper resource="test/book/map/jikeUser.xml" />
	  	<mapper class="test.book.map.JikeUserMapInterface" />
	  </mappers>  

```

- 在TestMain调试文件中

```java

	try {
		JikeUserMapInterface jkumi = session.getMapper(JikeUserMapInterface.class);
		jkumi.deleteUder(1);//删除id为1的记录
		session.commit();//提交sql语句
	} catch (Exception e) {
		e.printStackTrace();
		session.rollback();//回滚
	}finally {
		session.close();
	}  

```

### 查询

- 返回集合

#### Select 参数 如何操作 如何得到结果集

```xml

	<select id="selectPerson" parameterType="int" parameterMap="hashmap" resultType="hashmap" resultMap="personResultMap" flushCache="false" userCache="true" timeout="10000" fetchSize="256">  
  
```


| 属性 | 描述 |
| ------ | ------ |  
| id | 在命名空间中唯一的标识符，可以被用来引用这条语句 |   
| parameterType | 将会传入这条语句的参数类的完全限定名或类名 |  
| parameterMap | 这是引用外部parameterMap的已经被废弃的方法。使用内敛参数映射和parameterType属性|  
| resultType | 从这条语句中返回的期望类型的类和完全限定名或别名。注意集合情形，那应该是集合可以包含的类型，而不能是集合。使用resultType或resultMa，但不能同时使用 |  
| resultMap | 命名引用外部的resultMap。返回map是MyBatis最具力量的特性，对其有一个很好的理解的话，许多复杂映射的清醒就能被解决了。 |  
| flushCache | 将其设为true，不能语句什么时候被调用，都会导致缓存被清空。默认值为false |
| userCache | 将其设置为true，将会导致本条语句的结果被缓存。默认值为false |  
| timeout | 设置驱动程序等待数据库返回请求结果，并抛出异常时间的最大值。默认值不设定，驱动自行处理 |  
| fetchSize | 这是暗示驱动程序每次批量返回的结果函数。默认值不设置，程序自行控制 |  
| statementType | STATEMENT，PREPARED或CALLABLE的一种。这会让MyBatis选择使用Statement,PreparedStatement或Callable 的一种 |  
| resultSetType | FORWARD_ONLY，SCROLL_SENSITIVE,SCROLL_INSTENSITIVE中的一种。默认是不设置，驱动自行处理 |  

- parameterType封装：hashmap


```xml
	<select id="loginSelect" resultType="TestUser" parameterType="hashmap">
		select * from jikeUser where userName=#{userName} and password=#{password}
	</select>
```

>  老样子 把上述代码放在map.xml文件中

- 测试


```java
	HashMap(String, String) hm = new HashMap();
	hm.put("userName", "laoziniubi");
	hm.put("password", "666666"); 
```


- 上述的 "userName" 和 "password" 不仅是map的键，同时是 上述 select 标签中传入的参数名称
- 调用session 方法传入 hashmap
	- TestUser ontemp = session.selectOne("loginSelect", 	hm);
	
- 调试代码 `(使用hashmap)`


```java
	try {
		HashMap<String, String> hm = new HashMap<String, String>();
		hm.put("userName", "laoziniubi");
		hm.put("password","666666");
		TestUser testUser = session.selectOne("loginSelect",hm);
		if (testUser != null) {
			System.out.println(testUser.getUserName() + " 欢迎回来");
		}
	} catch (Exception e) {
		e.printStackTrace();
		session.rollback();//回滚
	}finally {
		session.close();
	}
```

- 调试代码 `(使用对象)`
	- 对象参数自动匹配属性
	- 如果对象属性与列名不一样用别名
	
- 这里 要修改xml文件的select标签


```xml

	<select id="login2" resultType="TestUser" parameterType="TestUser" >
		select * from jikeUser where userName=#{userName} and password=#{password}
	</select>  

```

- 然后是TestMain


```java

	try {
		TestUser testUser = new TestUser();
		testUser.setUserName("laoziniubi");
		testUser.setPassword("666666");
		TestUser getone = session.selectOne("login2", testUser);
		if (getone != null) {
			System.out.println(getone.getUserName() + " 欢迎回来");
		}
	} catch (Exception e) {
		e.printStackTrace();
		session.rollback();//回滚
	}finally {
		session.close();
	}  

```

#### 返回多个查询 	
- 上述只是返回一个对象的情况，如果是返回多个对象呢？
	- MyBatis会返回一个list

```xml

	<select id="selectTestUserList" resultType="TestUser">
		select * from jikeUser 
	</select>  

```

- 测试函数中调用List 来接受list
```java

	try {
		List<TestUser> ap = session.selectList("selectTestUserList");
		for (TestUser testUser : ap) {
			System.out.println(testUser.getUserName() + " 欢迎回来");
		}
	} catch (Exception e) {
		e.printStackTrace();
		session.rollback();//回滚
	}finally {
		session.close();
	}  

```

#### resultType 与 resultMap
- resultType 与 resultMap 一样用于返回结果操作
	- 但是，resultType 与 resultMap 只能用其中一个

- 区别是 resultMap 中可以解决一些比较复杂的映射问题
	- 例如：一个对象含有另一个对象的引用
	
```xml
	<resultMap id = "TestUserMap" type= "TestUser">
		<id property="id" column="id" />
		<result property="userName" column="userName" />
		<result property="password" column="password" />
	</resultMap>
```
- 上述中，如果类中的参数名与数据库中的参数名不一致的时候，可以使用resultMap来改变映射关系

- 使用resultMap
```xml
	<select id="selectUsers" resultMap="TestUserMap">
		select id,userName,password from jikeUser
	</select>
```
- 上述代码中，resultMap 指明了使用 哪个resultMap
- 会按照resultMap的设定来返回对应的值

- TestMain中的测试代码


```java

	try {
		List<TestUser> ap = session.selectList("selectUsers");
		for (TestUser testUser : ap) {
			System.out.println(testUser.getUserName() + " 欢迎回来");
		}
	} catch (Exception e) {
		e.printStackTrace();
		session.rollback();//回滚
	}finally {
		session.close();
	}
```

###事物处理
#### 事务处理配置
- MyBatis的事务处理又两个选项
	1. JDBC
		- JDBC代表的事
		- 务处理由JDBC完成
	2. MANAGED
		- MANAGED代表的事务处理由第三方的一些插件完成，例如Spring

- 事务处理的配置写在`基本配置文件当中`
> 在基本配置文件当中（就是那个调用map.xml的xml文件啦）
> 有个 transactionManager 标签，tpye属性当中就是上述的JDBC或者MANAGED

#### 事务处理方法
- MyBatis JDBC事务管理（典型代码）

1. 关闭自动提交
```java
	try{
		session = sqlMapper.openSession(false); // 关闭自动提交
		操作 balabalbala.....
		session.commit();// 提交事务	 
	}
	catch(Exception e){
		session.rollback();//回滚
	}
	finally{
		session.close(); //关闭session
	}
```