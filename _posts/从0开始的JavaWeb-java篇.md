---
title: 从0开始的JavaWeb---java篇
date: 2018-10-13 10:12:37
tags:
---

## 软件系统体系结构

### B/S
	1. B/S结构即浏览器/服务器（Browser/Server）
#### 优点
	只需要编写服务器端程序
#### 缺点
	安全性差
### C/S
	1. C/S 结构即 客户端/服务器（Client/Server），例如QQ
	2. 需要编写服务器程序，以及客户端程序，例如我们安装的就是QQ的客户端
#### 缺点
	软件更新时需要同时更新客户端和服务器两端，比较麻烦
#### 优点
	安全性比较好

### Web资源
#### Web资源介绍
	1. html：静态资源
	2. Jsp/Servlet：动态资源
	当然除了JavaWeb程序，还有其他Web程序，例如：ASP，PHP等。

#### 静态资源和动态资源的区别

![](https://i.imgur.com/6CCQ2RM.png)

#### 访问Web资源
	打开浏览器，输入URL：
		协议名：//域名：端口/路径，例如：https://www.baidu.com:8080/index.html

### Web服务器
	Web服务器的作用时接收客户端的请求，给客户端做出响应。
	对于JavaWeb程序而言，还需要有Jsp/Servlet容器，Jsp/Servlet容器的基本功能是把动态资源转会为静态资源，当然Jsp/Servlet容器不知这些功能。
	我们需要使用的是Web服务器和Jsp/Servlet容器，通常这两者会集于一身。下面是对JavaWeb的服务器：
		1. Tomcat(Apache):当前应用最广的JavaWeb服务器
		2. JBoss(RedHat红帽):支持JavaEE，应用比较广
		3. GlassFlsh(Orcale):ORacle开发JavaWeb服务器，应用不是很广
		4. Resin(Caucho)：支持JavaEE，应用越来越广
		5. Weblogic(Orcale):要钱的！支持JavaEE，适合大型项目
		6. Websphere（IBM）：要钱的！支持JavaEE，适合大型项目

### Tomcat
#### Tomcat简述
	Tomcat服务器由Apache提供，开源免费。由于Sun和其他公司参与到了Tomcat的开放中，所以最新的Jsp/Servlet规范总是能在Tomcat中体现出来。
#### 配置Tomcat
##### tomcat的安装
	自行百度
##### tomcat端口改变
	自行百度
##### tomcat配置
	自行百度
##### Tomcat目录结构

![](https://i.imgur.com/J24crxY.png)

	/work	tomcat把由jsp生成的servlet放于目录下
	/webapps	当发布web应用时，默认情况下把web应用文件放于次目录下
	/logs	存放tomcat的日志文件
	/share/lib	存放所有web应用都可以访问的jar文件
	/common/lib	存放tomcat服务器以及所有web应用都可以访问的jar应用
	/server/webapps	存放tomcat自带的两个web应用：admin应用和manager应用
	/server/lib		存放tomcat服务器所需的jar文件
	/server		包含三个子目录：classes。lib和webapps
	/conf	存放tomcat服务器的各种配置文件，其中最重要的文件是server.xml
	/bin	存放Windows平台以及linux平台上启动和关闭tomcat的脚本文件

### Web应用
#### 创建一个静态网站
	1. 在webapps目录下创建一个目录（命名必须不包含中文和空格），这个目录则为项目目录
	2. 在项目目录下创建一个html文件
#### 创建一个动态网站
	1. 在webapps目录下创建一个项目目录
	2. 在项目目录下创建如下内容
		1. WEB-INF目录
			1. WEB-INF目录下创建web.xml文件
				1. xml文件中的内容，可以从其他的项目中复制
			2. 创建一个lib目录，用户存放jar包
			3. classes目录，用于存放自己写的class
		2. 创建静态或动态页面
	WEB-INF下的项目，浏览器是不能访问的，所以为了安全起见，所以一些文件必须放到WEB-INF文件

#### 配置外部应用
##### 方法一
	conf/server.xml:打开server.xml文件，找到<Host>元素，在其中添加<Context>元素：
		<Host name="localhost" appBase="webapps"
				unpackWARs="true" autoDeplay="true">
			<Context path="hello" docBase="C:/hello"/>
		</Host>
	1. path：制定当前应用的名称
	2. docBase：指定应用的物理位置
	3. 浏览器访问路径：http://localhost:8080/hello/index.xml


​	
##### 方法二
	conf/catalana/localhost：在该目录下创建hello.xml文件，在该文件编写<Context>元素
		<Context docBase="C:/hello">
	1. 文件名：指定当前应用的名称
	2. docBase：指定应用的物理位置
	3. 浏览器访问路径：http://localhost:8080/hello/index.xml

#### servet.xml的配置
	1. <Service name="Catalina">	服务，名字为catalina
	服务中又有很多连接 <Connector>
	2. <Connector port="80" protocol="HTTP/1.1"
		connectionTimeout="20000" redirectPort="8443"/>
		用于接待HTTP/1.1的服务，端口是80端口，不处理请求
	3. <Engine> 引擎，用于处理请求，引擎下又分很多主机<Host>
	4. <Host name="主机名" appBase="基础目录"
			unpackWARs="true" autoDeploy="true">主机下又有<Context>上下文
	5. <Context> 上下文，对应的就是一个项目
	6. servet.xml中还有很多监听器
	7. 引擎唯一的，Service唯一的，Host可以多个，Context可以多个

## Servlet
### 什么是Servlet
	Servlet是javaWeb的三大组件之一，它属于动态资源。
	Servlet的作用是处理请求，服务器会把接收到的请求交给Servlet来处理，在Servlet中通常需要：
		1. 接收请求数据
		2. 处理请求
		3. 完成响应
	例如客户端发出登陆亲求，或者输出注册请求，这些请求都应该由Servlet来完成处理！
	Servlet需要我们自己来编写，每个Servlet必须实现javax.servlet.Servlet接口

![](https://i.imgur.com/uJbkkiR.png)

### 实现Servlet的方式
	实现Servlet的三种方式：
		1. 实现javax.servlet.Servket接口
		2. 继承javax.servlet.GenericServlet类
		3. 继承javax.servlet.http.HttpServlet类
	我们通常会去继承HttpServlet类来完成我们的Servlet，但学习Servlet还要从javax.servlet.Servlet接口开始


### 使用Servlet

![](https://i.imgur.com/TGsdd4W.png)

#### servlet的方法
	是由tomcat调用的方法
	1. init()
		1. 在Servlet对象创建之后马上执行，并且只执行一次
	2. service()
		1. 会被调用多次，每次处理请求都是调用这个方法
	3. destroy()
		1. 在Servlet被销毁之前调用，并且它只会被调用一次
	4. getServletConfig()
		1. 获取Servlet的配置信息（从init函数中，可以获得Servlet的配置信息）
	5. getServletInfo()
		1. 获取Servlet的信息（没什么用）

#### 浏览器访问Servlet
	1. 给Servlet指定一个Servlet路径（让Servlet与一个路径绑定在一起）
		1. 需要在web.xml中对Servlet配置
		2.  <servlet>
		   		<servlet-name>XXX随意</servlet-name>
				<servlet-class>Servlet的路径<servlet-class>
			</servlet>
		3.  <servlet-mapping>
				<servlet-name>与上面的name相同</servlet-name>
				<url-pattern>/虚拟路径 例如：/aa/b/c</url-pattern>
			</servlet-mapping>
	2. 浏览器访问Servlet路径
		1. localhost:8080/项目名/虚拟路径名

#### 特性
	1. 单例，一个类只有一个对象；当然可能存在多个Servlet类
	2. 线程不安全的，效率高
	3. Servlet由程序员写，但对象由服务器创建，调用响应的方法

![](https://i.imgur.com/nMe2CKX.png)

![](https://i.imgur.com/XTD10M9.png)

![](https://i.imgur.com/E6X43Wh.png)

### Servlet细节
#### Servlet与线程安全
	因为一个类型的Servlet只有一个实例对象，那么就有可能会出现同一个时间一个Servlet同属处理多个请求
	 那么Servlet是否为线程安全呢？
	 答案是“不是线程安全的”
	这说明Servlet的工作效率很高，但也存在线程安全问题
	所以我们不应该在Servlet中随意创建成员变量
	因为可能会存在一个线程这个成员变量进行写操作，另一个线程对这个成员变量进行读操作
	
	1. 不要在Servlet中创建成员！创建局部变量即可
	2. 可创建无状态成员
	3. 可以创建有状态成员，但是状态必须为只读的

#### 让服务器在启动时就创建Servlet
	默认情况下，服务器在某个Servlet第一次收到请求时创建它，也可以在web.xml中进行配置，使服务器启动的时候就创建Servlet
	<servlet>
		<servlet-name>hello1</servlet-name>
		<servlet-class>cn.itcast.servlet.HelloWorld<servlet-class>
		<load-on-startup>非负整数</load-on-startup>
		<!-- 非负数，越小越先创建 -->
	<servlet>

#### <url-pattern>
	<url-pattern>是<servlet-mapping>的子元素，用来指定Servlet的访问路径，即URL
	它必须是以 "/" 开头
	<servlet-mapping>
		<servlet-name>text</servlet-name>
		<url-pattern>/a</url-pattern>
		<url-pattern>/b</url-pattern>
		<url-pattern>/c</url-pattern>
	</servlet-mapping>
	那么说明这个Servlet绑定了多个url，一般也就一个，你设置多个也没什么用

### ServletContext
	一个项目只有一个ServletContext对象！application
	我们可以在N个Servlet中获取这个唯一的对象，使用它可以给多个Servlet传递数据
	Servlet之间互不一般是互不联系的，所以信息传递只能通过ServletContext
#### servletContext概述
	服务器会为每个应用创建一个ServletContext对象：
	1. ServletContext 对象的创建时在服务器启动时完成
	2. ServletContext 对象的销毁时在服务器关闭时完成
		
	ServletContext对象的作用是在整个Web应用的动态资源之间共享数据！
	例如：
		在A_Servlet中项 ServletContext对象中保存一个值，然后再B_Servlet中就可以获取这个值，这就是共享数据

#### 获取ServletContext
	在Servlet获取ServletContext对象：
	1. 在 void init(ServletConfig config)中：ServletContext context = config.getServletContext();
	
	在GenericeServlet 或 HttpServlet 中获取ServletContext对象：
	1. GenericSeriet类中由getServletContext()方法，所以可以直接使用this.getServletContext()来获取
	2. HttpServlet中有getServletContext()方法获取
	
	在ServletContextEvent中
	1. getServletContext()方法获取
	
	在HttpSession中
	1. getServletContext()方法获取

#### 设置，获取对象
	1. void serAttribute(String name,Objcet value):
		这是一个键值对，name与value对应
	2. Object getAttribute(String name):
		通过名为name 的键，去获得object类型的值
	3. void removeAttribute(String name):
		移除名为name 的键值对
	4. Enumeration getAttributeNames():
		获取所有域属性的名称

#### 获取资源
##### 获取真实路径
	使用ServletContext对象来获取web应用下的资源
	例如在hello应用的根目录下出创建a.txt文件，获取方法：
		String realpath = servletContext.getRealPath("/a,txt"),realpath的为a.txt的绝对路径

##### 获取资源流
	可以通过ServletContext获取资源流，即把资源以输入流的方式获取：
	1. 获取a.txt资源流 InputStream in = ServletContext.getResourceAsStream("/a.txt");

##### 获取指定目录下所有资源路径
	通过ServletContext获取指定目下所有资源路径
	例如获取/WEB-INF下所有的资源路径：
		Set set = context.getResourcePaths("/WEB-INF");

## Java画图（可用于验证码）
	BufferedImage bi = new BufferedImage(150, 35, BufferedImage.TYPE_INT_RGB);
	//得到图片缓冲区，这是长宽，图片格式RGB还是RGBA
	//得到它的绘制环境（画这张图片的笔）
	Graphics2D g2 = (Graphics2D) bi.getGraphics();
	
	g2.setColor(Color.WHITE);//设置颜色
	g2.fillRect(0,0,79,35);//填充图片，就是设置背景色
	
	g2.setFont(new Font("宋体", Font.BOLD, 25));//设置字体
	//Font.BLOD 为字体格式，比如blod就是粗体
	g2.setColor(Color.BLACK);//设置颜色
	
	ge.drawString("hell0", point.x, point.y);//向图片区域中写String的内容
	
	ImageIO.write(bi, "JPEG", new FileOutputStream("F:/a.jpg"));//输出流，bi为图片缓冲区，"JPEG"为图片格式

## response和request
	都是由服务器产生
![](https://i.imgur.com/KpOSoD7.png)

	服务器每次收到请求时，都会为这个请求开辟一个新的线程
	服务器会把客户端的请求数据封装到request对象中，request就是请求数据的载体
	服务器还会创建response对象，这个对象和客户端连接在一起，他可以用来向客户端发送响应

### response
	ServletResponse ---> 与协议无关的类型
	HtppServletResponse ----> 与http协议相关的类型
	二者无关，传入到Servlet中的时HttpServletResponse，所以可以强转为response
	
	http协议中响应内容包括什么呢？
#### 状态码
	200 表示成功， 302 表示重定向， 404 表示客户端错误， 500表示服务器端错误
	1. sendError(int sc)
	2. sendError(int sc, String msg)
	3. setStatus(int sc)
	例如：
		发送404
		response.sendError(404, "您访问的资源存在，就是不给你看");
#### 响应头
	响应头：Content-Type,Refresh,Location等
	1. setHeader(String name, String value):适用于单值的响应头
	2. addHeader(String name, String value):适用于多值的响应头
	3. setIntHeader(String name, String Value):适用于单值的int类型的响应头
	4. addIntHeader(String name, String value):适用于多值int类型的响应头
	5. setDateHeader(String name, long value):适用于单值的毫秒类型的响应头
	6. addDaTeHeader(String name, long value):适用于多值的毫秒类型的响应头；long型值为 毫秒值，代表过期时间，
	例如：
		发送302，设置location头，完成重定向	
			response.setHeader("Location","/项目名/servlet路径");
			response.setStatus(302);
		定时刷新，设置Refresh头，其实就是定时重定向
			PrintWriter write = rsponse.getWriter();
			writer.print("欢迎登陆，5秒后自动跳转到主页");
			response.setHeader("Redresh", "5;URL=/项目名/重定向的servlet或jsp");
		禁用浏览器缓存：Cache-Control, prama, expires
			response.setHeader("Cache-Control","no-cache");
			response.setHeader("prame","no-cache");
			response.setDateHeader("expires",-1);//过期时间-1，立马过期
		<meta>标签可以代替响应头

#### 响应体
	通常是html，也可以是图片
	response的两个流：
		1. ServletOutPutStream,用来向客户端发送字节数据
			ServletOutputStream out = response.getOutputStream();
		2. PrintWriter,用来向客户端发送字符数据!需要设置编码
			PrintWriter writer = response.getWriter();
		两个流不能同时使用
	发送字节流：
		String s = "hello world";
		byte[] bytes = s.getBytes();
		response.getOutputStream().write(bytes);
	发送字节图片：
		//运用commons-io库
		String path = "a.jpg";
		FileInputStream in = new FileInputStream();
		//读取输入流内容的字节到字节数组中
		byte[] bytes = IOUtils.toByteArray(int);
		response.getOutputStream().write(bytes);
#### 重定向
	这个重定向不同与上面的重定向，这个更快
	sendRedirect(String location)方法
	response.sendRedirect("/项目名/servlet虚拟路径或jsp名");

### request
	封装了客户端所有的请求数据
	Http协议中的数据都可以通过request对象来获取
#### 获取常用信息
	获取客户端Ip，请求方式
	Ip：request.getRemoteAddr();
	请求方式：request.getMethod();
#### 获取请求头
	String getHeader(String name),适用于单值头
	int getIntHeader(String name),适用于单值int类型的请求头
	long getDateHeader(String name),适用于单值毫秒类型的请求头
	Enumeration<String> getHeaders(String name),适用于多值请求头
	例如：
		通过user-agent识别用户浏览器类型
			request.getHeader("User-Agent");
		防盗链：如果请求不是通过本站发出的超链接发出的，发送错误状态码404
			Refere这个请求头，表示请求的来源
			String referer = req.getHeader("Rederer");
			if(referer == null || referer.contains("localhost")){
				resp.sendRedirect("https://www.baidu.com");
				System.out.println("baidu");
			} else{
				System.out.println("hello");
			}
#### 获取请求URL
	String getScheme();获取协议
	String getServerName();获取服务器名
	String getServerPort();获取服务器端口
	String getContextPath();获取项目名
	String getServletPath();获取Servlet路径
	String getQueryString();获取参数部分，即问好后面的部分
	String getRequestURI();获取请求URI，等于项目名+Servlet路径
	String getRequestURL();获取请求URL，等于不包含参数的整个请求路径


![](https://i.imgur.com/moO8HuU.png)


#### 获取请求参数
	请求参数时由客户端发送给服务器的
		1. 有可能在请求体中（post）
		2. 可能在URL中（get）
	1. String getParameter(String name):获取指定名称的请求参数值，适用于单值请求
	2. String[] getParameterValues(String name);获取指定名称的请求参数值，适用于多值请求参数
	3. Map<String, String[]> getParameterMap():获取所有请i去参数，其中key为参数名，value为参数值，
	例如：
		超链接参数
		表单数据

#### 请求转发和请求包含
	RequestDispatcher rd = request.getRequestDispatcher("/MyServlet");//参数是被包含或被转发的Servlet虚拟路径
	请求转发：rd.forward(request,response);（常用）
	请求包含：rd.include(request,response);
	
	有时一个请求需要多个Servlet协作才能完成，所以需要一个Servlet跳到另一个Servlet
	1. 一个请求跨多个Servlet，需要使用转发和包含
	2. 请求转发：由下一个Servlet完成相应体，当前Servlet可以设置响应头（留头不留体）
		1. 即request.setHeader()中的内容，可以传递到第二个servlet
		2. response.write()这类的内容不会传递回去，即第一个Servlet的内容不会输出浏览器
	3. 请求包含：由两个Servlet共同完成相应体（都留）
	4. 物理是请求转发还是请求包含，都在一个请求范围内，使用同一个resquest和response

#### 请求转发与重定向不同
	1. 请求转发是一次请求，重定向是两次转发
	2. 请求转发地址栏不变，重定向后会显示一个请求的地址
	3. 请求转发只能转发到本项目其他servet，而重定向哪都能去
	4. 请求转发为服务端行为，重定向是客户端行为

#### request域
	Servlet中三大域对象：request,session,application,
	1. void setAttribute(String name);
	2. Object getAttribute(String name);
	3. void removeAttribute(String name);
	同一个请求范围内使用request.getAttribute()和request.setAttribute()可以使用
	但是如果是重定向则不能获取，因为不是同一个请求

![](https://i.imgur.com/ntAKbGY.png)

## 编码
	常见字符编码：iso-8859-1（不支持中文），gbk（系统默认编码，中国的国标码），utf-8（万国码，支持全世界的编码，所以我们要使用这个）

![](https://i.imgur.com/ix3MrnG.png)

### 响应编码
	1. 当使用response.getWriter()来向客户端发送字符数据时
	   如果在之前没有设置编码，那么默认使用iso，以为不支持中文，所以一定是乱码
	2. 在使用response.getWriter()之前可以使用response.setCharaceterEncoding()
	   来设置字符流的编码为gbk或utf-8
	3. 在使用response.getWriter()之前可以使用resonse.setHeader("Content-type","text/html;charset=utf-8")
	   来设置响应头，通知浏览器服务器这边使用的utf-8
	4. serHeader("Content-Type","text/html;charset=utf-8")的快捷方式是:setContentType("text/html;charset=utf-8");


### 请求编码
	1. 客户端发送给服务器的请求参数是什么编码：
		请求页面时，服务器响应的编码是什么，那么客户端发送请求时的编码就是是什么
	2. 服务器默认使用ISO-8859-1来解码，所以中文肯定出现乱码
	3. 请求编码处理分为两种：get，post：get请求参数不再请求体中，而post请求参数在请求体中，所以处理方式不同


##### GET请求编码处理
	1. Sting username = request.getParameter("name");
	2. byte[] bytes = name.getBytes("ISO-8859-1");
	3. name = new String(bytes, "utf-8");
	4. 在server.xml中配置URIEncoding=utf-8

##### POST请求编码处理
	1. String usernmae = new String(request.getParameter("iso-8859-1"),"utf-8");
	2. 在获取参数之前调用request.setCharacterEncoding("utf-8");

### URL编码
	表单的类型：Content-Type:application/x-www-form-urlencoded	就是把中文转换为%后面跟随两位16进制
	
	1. 他不是字符编码
	2. 它是用来在客户端和服务器之间传递参数用的一种方式
	3. URL编码需要先指定一种字符编码，把字符串解码后得到byte[],
	   然后把小于0的字节+256，再转换为16进制，前面再加%
	4. POST请求默认就是使用URL编码，tomcat会自动使用URL编码
	5. URL编码：String name = URLEncoder.encode(name, "utf-8");
	6. URL解码：String name = URLDecoder.decode(name,"utf-8");


## 路径

	1. web.xml中<url-pattern>路径
		要么以“*”开头要么以"/"开头
	2. 转发和包含路径
		1. 以"/"开头：相对当前项目路径
		2. 不以"/"开头：相对当前Servlet路径
	3. 重定向路径（客户端路径）
		1. 以"/"开头：相对当前主机，所以必须后面自己加上项目名
	4. 页面中超链接和表单路径
		1. 与重定向相同，都是客户端路径，需要添加项目名
		2. <form action="/项目/servlet">
		3. 如果不已"/"开头，那么相对当前页面所在路径
		4. 建议使用以"/"开头的路径，因为如果页面路径改变，那么servlet就找不到了
	5. ServletContext获取资源路径
		1. 相对于当前项目目录，即index.jsp所在路径
	6. ClassLoader获取资源路径
		1. 相对classes目录
	7. Class获取资源路径
		1. 以"/"开头，相对Classes目录
		2. 不以"/"开头，相对当前.class文件所在目录


## JSP
	jsp程序是java为了适应web开发而扩展的一种程序形式，是java程序针对web开发进行的简化。
	
	用户通过浏览器向服务器发送指定页面的请求，接下来web服务器读取jsp文件，jsp文件会被转换为一个普通
	java文件，java文件进行编译，得到一个class文件，web服务器装在解释执行class文件，并将执行结果响应至客户端。
	tomcat把为每个jsp页面创建的java文件和class 文件，放在安装目录下的 \work\Catalina\localhost\同名文件夹内。

### JSP的作用
	Servlet：
	1. 缺点：不适合设置html响应体，需要大量的response.getWriter().print(html);
	2. 优点：动态资源，可以编程
	
	html:
	1. 缺点：html是静态页面，不能包含动态信息
	2. 优点：不用为输出html标签而发愁
	
	JSP：
	1. 优点：在原有html的基础上添加java脚本，构成jsp页面

### JSP和Servlet的分工
	JSP：
	1. 作为请求发起页面，例如显示表单，超链接
	2. 作为请求结束页面，例如显示数据
	
	Servlet：
	1. 作为请求中处理数据的环节

### JSP的组成
```jsp
1. JSP = html + java脚本 + jsp标签（指令）
2. jsp中无创建既可使用的对象有9个，被称为9大内置对象，例如：request,out等
3. 3中java脚本：
	1. <% .... %>：Java片段，用于定义0~N条Java语句
	2. <%=....%>：java表达式，用于输出，用于输出一条表达式的结果
	3. <%!....%>：声明，用来创建类的成员变量和成员方法(基本不用)
```

#### jsp声明语法：
```jsp
<%! 
       String str = "hello world"; 
       String getStr(){
	return "hello world2";
       }
%>
声明必须再"<%!" 和 "%>" 之间进行。声明部分只能定义成员方法（函数）和成员变量，不能直接包含程序域。这里定义了一个str变量
在jsp文件中使用， 例：
<hr>// <hr> 是分割线的意思
<%   out.println(this.str)   %>//通过this 的方法调用变量或者方法（函数）
<hr>
<% = this.getStr()%>//注意加了一个“=”
```

#### jsp程序脚本：
```jsp
包括变量的声明，表达式和程序逻辑
声明的变量转换为_service 方法中的变量，因而是局部变量
语句块可以自由的与页面代码组合使用
<% int i = 100; %>// 这里的 i 是脚本变量  上面的 加了 “!”的是成员变量
<% if (i > 10) 
{  %>
    <h1>i > 10 </h1>
<% }
else
{ %>
    <h1> i <= 10 </h1>
<% } %>  // 这里就是 java 和 jsp 的交叉写法。当然而可以直接用out.prinln 但是正常网页中，显示的不会是单调的黑字输出，而是有样式的输出。

从下面的例子中可以看出 脚本变量 与 成员变量 的区别：
<!% int global = 0 %>
<% int test = 0 
       global ++;
       test ++;
%>
<%
      out.println(global);
      out.println("<br>");
      out.printlin(test);
%>
将其在加载到eclipse的工程中，然后不断刷新页面，会发现global的值会每次刷新都“+1”，但是test的值总是从0 加到 1
就像是全局变量与局部变量的区别。
```

#### jsp注释：
```jsp
语法格式：
<%--你要注释的内容--%>
有点像html 的注释写法，就是多了两个%。
但是，jsp既然嵌套了java语言，那么java的注释写法依然是可用的。
“//”  单行注释
“/*  */”多行注释
java注释一般多用于 "<%%>" 中
```

#### jsp内容输出表达式
```jsp
语法格式：
<% = 输出的变量名 %>
例如：
<% int i = 10 %>
i 的值是 ：<% = i %>
当然你也可以直接用 <% out.println(i) %>，但是嘛 写得多还不好控制格式
```

#### jsp包引入语法
```jsp
语法格式：
<% @ page import = "java.util.Date" %> // 引入一个 java.util.Date 的包
<% @ page import = "java.io.*" %> //一次进入多个 java.io. 的包
<% @ page import = "java.util.Date,  java.io.* "%> //一次引入多个包，用逗号隔开。
```

### JSP的内置对象
- out对象

  - 用于向客户端浏览器输出各种数据
- request对象

  - 封装了来自客户端浏览器的各种信息
- response对象

  - 封装了服务器的响应信息
- exception对象

  - 封装了程序执行中的异常和错误信息
- config对象

  - 封装了引用程序的配置信息
- page对象

  - 指向当前程序本身
- session对象

  - 用来保存回话信息，保存同一用户不同请求之间可以共享数据
- application对象

  - 代表当前应用程序的上下文，在不同的用户之间共享信息
- pageContext对象
  - 提供了对jsp所有命名空间以及对象的访问

#### out对象

- out对象输出
	
```js
out.println("文本1");	//向客户端浏览器输出一行文本，最后输出一个换行
out.print("文本2");	//想客户端浏览器输出一行文本
out.newLine();	//输出一个换行效果

```

- out对象对输出缓冲区进行管理

```jsp
out.println("获取当前缓冲区大小：" + out.getBufferSize());
out.printlb("当前缓冲区剩余字节数目：" + out.getRemaining());
```
> `out.flush()方法`，用于强制刷新服务器缓冲区里的数据，也就是说可以手工将缓冲区里的数据输出到浏览器
> `out.clearBuffer()方法`，用于清空缓冲区的数据
> `out.clear()方法`，用于清空缓冲区的数据，但是（不同于clearBuffer()）如果之前调用过.flush()方法，那么clear()方法则会抛出异常

```java

out.println("文本1");	//向客户端浏览器输出一行文本，最后输出一个换行
out.print("文本2");	//想客户端浏览器输出一行文本
out.newLine();	//输出一个换行效果

//out.flush();
out.clearBuffer()l

```

> 上述情况中，如果注释了out.flush()方法，那么上述print 将没有输出，因为被clearBuffer了
> 但是如果 放开了注释out.flush()，那么将print到页面中，因为先强制输出了，再清空就没有意义了

#### request对象

- Web 应用程序应该是双向的，不仅仅是服务器向客户端展示数据，同时也有客户端向服务器提交信息

- request对象
	- 封装了从客户端到服务器发出的请求信息
		- 客户端ip
		- 用户提交的表单信息
		- cookie
		- 主机名
		- ……
- 服务器通过.getParameter 方法获取用户提交的表单数据
- request的大部分方法都是用于处理客户端提交请求中的各种参数和选项

```html

<form action="" method="post">
	<input type="text" name="username" />
	<input type="submit" value="提交" />
</form>
请求方法名：<%= request.getMethod() %>
获取请求URI字符串，请求的资源：<%= request.getRequestURI() %>(从请求的主机名之后的第一个字符开始，到查询字符串结束的字符串)
请求所使用的协议：<%= request.getProtocol() %>
获取服务器的名称：<%= request.getServerName() %>
请求的服务器端口：<%= request.getServerPost() %>
获取客户端的IP地址：<%= request.getRemoteAddr() %>
获取客户端的主机名：<%= request.getRemoteHost() %>
获取提交的表单数据：<%= request.getParameter("username") %>
```

#### response对象

- 用于服务器对客服端的请求进行回应，负责处理http连接信息
  - 设置文件头
  - cookie信息
  - ……



```jsp
<body>
    <% 
    	response.setHeader("Cache-Control","no-cache"); //设置网页缓存策略为no-cache
    	response.setIntHeader("Refresh", 2);//设置int类型的信息，这里是设置2s刷新一次网页
    	response.sendRedirect("http://www.baidu.com");//设置跳转
		Coolie myCookie = new Cookie("darkmi","Test");//设置键值对
    	myCookie.setMaxAge(3600);//Cookie的最大存活时间3600s
    	response.addCookie(myCookie);//添加Cookie
    %>
</body>
```

​	

#### application对象

-  代表当前的应用程序，存在于服务器的内存空间中，应用一旦启动，就会自动生成一个application对象

```jsp
<%
	application.getServerInfo();//返回当前服务器的详细信息
	application.getServletContextName();//放回当前应用的名称
	application.getVirtualServerName();//获取主机名称
%>
```



#### config对象

- 代表当前jsp程序的配置信息
- config对象是servletConfig类的一个实例



> 在web.xml文件中添加如下信息

```xml
<servlet>
    <servlet-name>config</servlet-name>
    <jsp-file>/13/config.jsp</jsp-file>
    <init-param>
    	<param-name>username</param-name>
        <param-value>darkmi</param-value>
    </init-param>
    <init-param>
    	<param-name>password</param-name>
        <param-value>Testroot</param-value>
    </init-param>
</servlet>
<servlet-mapping>
	<servlet-name>config</servlet-name>
    <url-pattern>/13/*</url-pattern>
</servlet-mapping>
```

- 上述代码，添加了两个配置信息 username 和 password
- 在如下的代码中可以获得config数据

```jsp
<%= config.getInitParameter("username") %>
<%= config.getInitParameter("password") %>
```

#### session对象

- 服务器本身不会记录之前客户端请求的任何信息
- 用session进行辅助则可以`记录客户端之前的信息`



```jsp
<body>
    获取session的ID（唯一标识符）：<%= session.getID() %>
    session的创建时间：<%= new java.util.Date(session.getCreationTime().toString()) %>
    session的最后访问时间：<%= new java.util.Date(session.getLastAccessedTime()) %>
    session的失效时间(单位为s)：<%= session.getMaxInactiveInterval() %>
    判断session是否是新创建：<%= session.isNew()%>
    清除session对象：<%= session.invalidate() %>
</body>
```

- 上述代码中，创建时间和访问时间都是long 型，所以需要通过java的Date 类来转换为 可读的时间



#### exception对象

- JSP引擎在执行编译好的代码的时候，可能会抛出异常
- exception表示jsp引擎在执行的时候抛出的异常
- exception对象需要配置

```jsp
<%@ page errorPage="handle_error.jsp" %> <!-- 设置处理异常的jsp -->
<%@ page isErrorPage="true" %><!-- 在处理异常的jsp中配置 -->
```



```jsp
<%
exception.getMessage()方法用于返回描述异常的信息：out.println(exception.getMessage())
exception对象的字符串描述：exception.toString()
打印异常的堆栈轨迹：exception.printStackTrace()
%>
```



#### page对象

- 有点类似Java中的this指针，因为page对象指向当前jsp本身

```jsp
<%
page对象的字符串描述：out.println(page.toString()) // 字符串 @ 之前是 jsp的完全限定名 之后是HashCode值
返回当前的Object类：page.getClass()
返回page对象的hashcode值：page.hashCode()
比较是否相等：page.equals(object)
%>
```

- 还有一些与线程相关的方法



#### pageContext

- 是jsp中所有对象最大的集成者

```jsp
<% 
JspWriter myout = pageContext.getOut()
// 其他八个内置对象同理

%>
```





















