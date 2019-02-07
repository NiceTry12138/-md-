---
title: Ajax
date: 2017-11-20 21:12:01
tags:
---
## 什么是Ajax
	允许浏览器与服务器通信而无须刷新当前页面的技术都叫Ajax
	异步的Js和XML的通信

### 不用刷新整个页面就可以与服务器通讯的方法
	1. Flash
	2. Java appleet
	3. 框架：如果使用一组框架构造了网页，可以只更新其中一个框架，而不用惊动整个页面
	4. 隐藏的iframe
	5. XMLHttpRequest:该对象是对JavaScript的一个扩展，可使网页与服务器进行通信。
	   是创建Ajax应用的最佳选择，实际上通常把Ajax当成XMLHttpRequest对象的代名词

![](https://i.imgur.com/1TQnuU0.png)

### Ajax工具包
	Ajax并不是一项新技术，它实际上是几种技术，每种技术各尽其职，以一种全新的方式聚合在一起：
	1. 服务器端语言：服务器必须具备向浏览器发送特定信息的能力。Ajax与服务器语言无关
	2. XMLL:Ajax程序需要某种格式化的格式来在服务器和客户端之间传递信息，XML是其中一种选择
	3. XHTML：使用扩展HTML和CSS标准化呈现
	4. DOM：实现动态交互和显示
	5. 使用Javascript绑定和处理所有数据
	6. 使用XMLHTTP组件XMLHttpRequests对象进行异步数据读取

### Ajax的缺陷
	1. 由JavaScript和Ajax引擎会导致引擎的兼容性问题（现在少）
	2. 页面局部刷新，导致 后退功能不好用
	3. 对流媒体的支持没有Flash和JavaApple好
	4. 一些手持设备支持性差（现在少）

## XMLHttpRequest
	
### 创建XMLHttpRequest对象
	function getHTTPObject(){
		var xhr = false;
		if(window.XMLHttpRequest){
			xhr = new XMLHttpRequest();
		} else if(window.ActiveXObject()){
			xhr = new ActiveXObject("Microsoft.XMLHttp");
		}
		return xhr;
	}

- 大多数浏览器都支持 `var xmlhttp = new XMLHttpRequest()`
- IE6.0： `var xmlhttp = new ActiveXObject("Msxml2.XMLHTTP")`
- IE5.5及更早版本的IE： `var xmlHttp = new ActiveXObject("Microsoft.XMLHTTP");`
- 对window.XMLHttpRequest的调用会返回一个对象或null，如果XMLHttpRequest对象存在，啧把xhr的值设为该对象的新实例

### 属性
#### 以下用于发送：
1. abort()停止当前请求
2. getAllResponseHeader() 把HTTP请求的所有响应首部作为键值对返回
3. getResponseHeader("header"); 返回指定首部的串值
4. open("method","url",bool);建立对服务器的调用，Method参数可以是put或post，url可以是相对url也可以是绝对url, 请求是否为异步请求
5. send(content) 向服务器发送请求，没有为null，最好send里面有东西（就算是null）
6. setRequestHeader("header","value");设置首部及其值，在设置任何首部之前必须先调用open()

#### 以下用于请求：
1. onreadystatechange	每个状态改变的是都会出发这个事件处理器，通常会条用一个JavaScript函数
2. readyState	请求的状态，有五个可取值：0=未初始化，1=正在加载，2=已经加载，3=交互中，4=完成
3. responseText	服务器的响应，表示为一个串
4. responseXML	服务器的响应，表示为XML，这个对象可以解析为Dom对象
5. status	服务器的HTTP状态码
6. statusText	HTTP状态码对应的文本（OK或NotFount等）

### 一个简单的案例
	目标，不刷新，不跳转界面，只alert 出 a.xml
	<script>
		window.onload = funtion(){
		//获取a节点
		document.getElementByTagName("a")[0].onclick = function(){
			// 创建一个XMLHttpRequest对象
			var request = new XMLHttpRequest();

			// 准备发送请求的数据：url加上时间戳
			var url = this.href + "?time="+new Date();
			var method = "GET";

			// 调用XMLHttpRequest 对象的open方法
			request.open(method, url);

			// 调用XMLHttpRequest 对象的send方法
			request.send(null);

			// 为 XMLHttpRequest 对象添加onreadystatechange
			
			// 判断响应是否完成：XMLHttpRequest对象的readyState属性为4的时候
			// 再判断响应是否可用：XMLHttpReqeust对象status属性值为200
			request.onreadystaechange = function(){
				if(request.readyState == 4){
					if(request.status == 200 || request.status == 304)
					alert(request.responseText);
				}
				
			}

			//返回false，取消原有功能，也就是说返回false后，不会跳转页面
			return false;
		}		
	}
	</script>
	<html>
		<a href="a.xml">跳转</a>
	</html>

### 发送请求
- 利用XMLHttpRequest实例与服务器进行通信包含一下三个关键部分：
1. onreadystatechange 事件处理函数
2. open 方法
3. send 方法

#### onreadystatechange
	该事件处理函数由服务器出发，而不是用户
	在Ajax执行过程中，服务器会通知客户端当前的通信状态
	这依靠更新XMLhttpRequest对象的readyState来实现
	改变readyState属性是服务器对客户端连续操作的一种方式
	每次readyState属性的改变都会触发readystatechange事件

#### open(methdo, url, asynch)
- XMlHttpRequest对象的open方法允许程序员用一个Ajax调用向服务器发送请求

- method：请求类型，类似“GET”或“POST”的字符串。

- 在某些情况下，有些浏览器会把多个XMLHttpRequest请求的结果缓存到用一个URL，
- 如果每个请求的相应不同，但是得到的结果却会一样。所以此时加一个 时间戳 到url最后，以确保url的唯一性

- url：路径字符串，指向你所请求的服务器上的那个文件，可以是绝对路径，也可以是相对路径

- asynch：表示是否要异步传输，默认是true

#### send(data)

1. open方法定义了Ajax请求的一些细节，send方法可以为已经待命的请求发送指令
2. data：将要发送给服务器的字符串
3. 若用"GET"请求，则不用发任何数据，即request.send(null);
4. 当向send()方法提供参数时，要确保open()中指定的方法是"POST",如果没有数据发送，则使用null

#### setRequestHeader(header, value)
1. 当浏览器向服务器请求页面时，它会伴随这个请求发送一组首部信息，当这些首部信息是一系列描述请求的元数据（metadata）。首部信息来声明一个请求时get还是post
2. Ajax请求中，发送首部信息的工作可以是由setRequestHeader完成
3. 参数header:首部的名字；参数value:首部的值
4. 如果用POST请求向服务器发送数据，需要将 "Content-type"的首部设置为 "application/x-www-form-urlencoded"。
	- 他会告知服务器正在发送数据，并且数据已经符合url编码了
5. 该方法必须在open()之后才能调用

##### post示例

```html
var url = "../jsp/forumServlet";
var nameValue = trim(document.forumiddform.name.value);
xhr.open("POST", url);
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
xhr.send("method=name_isExist" + "&name" + nameValue);
```

### 接收响应
	
#### readyState
1. readyState 属性表示Ajax请求的当前状态
	0. 0代表未初始化，没调用open方法
	1. 1代表正在加载，open()调用了而send()没有调用
	2. 2代表send()调用了，请求开始
	3. 3代表交互中，服务器正在发送响应
	4. 4代表完成
2. readyState值的变化会出发 readystatechange 事件，如果把onreadystaechange事件赋给函数，则每次变换调用函数
3. readyState的值因浏览器不同有所差异，但是请求结束时，每个浏览器都会把 readyState 的值设为 4

#### status
	服务器发送的每一个响应也都有首部信息
	
	常用的状态码及其意义：
	1. 404 没有页面
	2. 403 禁止访问
	3. 500 内部服务器错误
	4. 200 一切正常
	5. 304 没有被修改
	
	在 XMLHttpRequest 对象中，服务器发送的状态码都保存在status属性中。

#### responseText
	XMLHttpRequest 的 responseText 属性包含了从服务器发送的数据。它是一个HTML，xml或普通文本
	当 readyState 属性值变成 4 时，responseText 属性才可以用，表明Ajax请求已经结束

## 数据格式
	在服务器端Ajax时一门与语言无关的技术，在业务逻辑层使用何种服务器端语言都可以
	从服务器端接收数据的时候，那些数据必须以浏览器能够理解的格式来发送。服务器端的编程语言只能以如下三种格式返回数据：
		1. XML
		2. JSON
		3. HTML
		
### 解析HTML
	HTML由一些普通文本组成，如果服务器通过XMLHttpRequest发送HTML，文本将存储在responseText属性中
	
	不必从responseText属性中读取数据。他已经是希望的格式，可以直接将它插入到页面中

	插入HTML代码最简单的方法是更新这个元素的innerHTML属性

#### 例如

```
document.getElementById("id").innerHTML = request.responseText;
```

#### 优点
	1. 从服务器端发送的HTML代码在浏览器端不需要用Javascript解析
	2. HTML的可读性好
	3. HTML代码块与innerHTML 属性搭配，效率高

#### 缺点
	1. 如需要通过Ajax更新一篇文档的多个部分，HTML不合适
	2. innnerHTML并非DOM标准（问题不大，现在浏览器大都兼容）

### XML
	1. 需要进行解析，之后再插入到HTML中
	2. 获得的 responseHTML 不能直接使用，必须先创建对应的节点作为容器
		result = request.responseXML;
	3. xml可以使用DOM的方式进行解析
		var name = result.getElementsByTagName("key")[0].firstChild.nodeValue;
		var aNode = document.createElement("a");//创建a标签
		aNode.appendChild(document.createTextNode(name));
		aNode.href = "url";

#### 优点
	1. XMl是一种通用的数据格式
	2. 不必把数据强加到以定义好的格式中，而是要为数据自定义合适的标记
	3. 利用DOM可以完全掌控文档

#### 缺点
	1. 当浏览器接收到长的XML文件后，DOM解析可能会很复杂
	2. 如果文档来于服务器，就必须得到保证文档含有正确的首部信息。若文档类型不正确，那么responseXML的值将是空的
	
### JSON
- 一种简单那的数据格式，比XML更轻巧。
	- SON是JavaScript原生格式，这意味着JavaScript中处理JSON数据必须要任何特殊的API 或 工具包
	
- JSON的规则很简单：对象是一个无序的" '名称/值'对 "的集合。
	- 一个对象以"{" 开始， "}"结束。每个“名称” 后跟一个 ":"冒号；“'名称/值'对”之间使用 “,” 逗号分隔
		
- Json用冒号来赋值
- 赋值语句用逗号分开
- 整个对象用大括号封装
- 可用大括号分装嵌套数据
- 对象描述中存储的数据可以是字符串，数字，布尔值，甚至函数方法
	
```javascript
var jsonObjec = {
	"name" : "test",
	"age":12,
	"address":{"city":"wuhan", "contury":"chind"}
	"teaching" : function () {
	  alert("this is a funtion"); 
	}
};
alert(jsonObjec.name);
jsonObjec.teaching();
```
- 其实嘛，json可以用jar包打包，不用自己写
	
#### 字符串转为json对象
- Json保存在responseText中
- 需要借助JavaScript的eval语句
	- 函数eval会把一个字符串当做它的参数，然后这个字符串会被当做JavaScript代码来执行
	- var JsonResponse = xmlHttp.responseText;
	- var personJson = eval("(" + JsonResponse + ")");
	- 上述的 左括号和右括号 一定要加

- Json 提供了json.js 包，下载[http://www.json.org/json.js](http://www.json.org/json.js) 后，使用parseJSON()方法将字符串解析
	-  var JsonResponse = xmlHttp.responseText;
	- personJson = JsonResponse.parseJSON();
	


## 看实战学操作
### 发送post请求，判断账户名是否存在
`如果发送请求时带有参数，一般都用post请求`

- 请求头有个 `默认值` 是 Content-Type: application/x-www-form-urlencoded
- open : xmlHttp.open("post", .....);

- 添加一步：设置Content-Type请求头：
> xmlHttp.setRequeestHeader("Conten-Type","application/x-www-form-urlencoded");

- send : xmlHttp.send("username=zhanshan&password=123");

#### JSP的写法

```html
<%--
  User: cong
  Date: 18-11-22
  Time: 下午3:48
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
    <title>Ajax</title>
    <script src="http://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js"></script>
  </head>
  <body>
  <form method="post" action="">
    <span>用户名：</span><input type="text" id="username" name="username" /><span id="can1" style="color: red" ></span>
    <br>
    <span>密 码：</span><input type="password" id="password" name="username"/>
    <br>
    <input type="submit" value="注册"/>
  </form>
  </body>
  <script>
    window.onload = function () {
        var username = document.getElementById("username");
        function createXMLHttpRequest() {
            try {
                return new XMLHttpRequest();
            } catch (e) {
                try {
                    return new ActiveXObject("Msxm12.XMLHTTP");
                } catch (e) {
                    try {
                        return new ActiveXObject("Microsoft.XMLHTTP");
                    } catch (e) {
                        alert("浏览器太几把差了");
                        throw e;
                    }
                }

            }
        }
        username.onblur = function() {
            // 当失去焦点的时候 触发函数
            // 获取异步对象
            var xmlHttp = createXMLHttpRequest();
            // 打开链接
            xmlHttp.open("post", "Exist", true);
            // 设置请求头
            xmlHttp.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");

            // 发送请求 给出请求体
            xmlHttp.send("username=" + username.value);

            // 给xmlHttp的onreadystatechange事件注册监听
            xmlHttp.onreadystatechange = function () {
                if (xmlHttp.readyState === 4) {
                    if (xmlHttp.status === 200){
                        // 4 代表 运行完成  200 代表状态码
                        var text = xmlHttp.responseText;
                        var can1 = document.getElementById("can1");
                        if (text == "1") {
                            can1.innerHTML = "用户名已存在"
                        } else {
                            can1.innerHTML = "";
                        }
                    }
                    else{
                        alert("false");
                    }
                }
            }
        }
    }

  </script>
</html>

```

#### Servlet写法

```java
package com.ajax.test;

import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * Servlet implementation class Exist
 */
@WebServlet("/Exist")
public class Exist extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    /**
     * @see HttpServlet#HttpServlet()
     */
    public Exist() {
        super();
        // TODO Auto-generated constructor stub
    }

	/**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		// response.getWriter().append("Served at: ").append(request.getContextPath());
		System.out.println("get");
	}

	/**
	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		// doGet(request, response);
		System.out.println("post");
		request.setCharacterEncoding("utf-8");
		response.setContentType("text/html;charaset=utf-8");
		String username = request.getParameter("username");
		if(username.equalsIgnoreCase("lc")) {
			response.getWriter().print("1");
			System.out.println("1");
		}else {
			response.getWriter().print("0");
			System.out.println("0");
		}
	}

}
```

### 响应内容为XML

- 首先就要设置响应头
- 服务器端：
	- Contentype 设置为 text/xml;charset=utf-8
- 客户端：
	- var doc = xmlHttp.responseXML; //得到的是Documented对象
	- 获取服务器的响应结果
	- 使用dom运用
	

## JQuery的Ajax
- jQuery对Ajax操作进行了封装
	- 在jQuery中最底层的方式是 $.ajax()
	- 第二层是load()，$.get() 和 $.post()
	- 第三层是$.getScript()和$.getJSON()

### ajax 方法（底层接口）
- $.ajax(url,setttring)
	- url 参数地址
	- setttring 例如下面（包括大括号都是）
		- {type:'post', data : {id : 1, name : "test"} ,beforeSend:function(xhr){},success:function (data){},error(xhr){},conplete:function(){}}
		- data 为 服务端的响应体
		- success 为 响应成功的时候的回调函数
			- 其中 data 的数据类型 会通过 服务端的 设置 自动转换
		- data 为 传递参数
			- post 通过请求体传递
			- get 通过 url 传递
		- 通过设置dataType 设置 返回的参数类型
		- error 请求不正常(状态码不为200)的时候执行的函数
		- complete 请求完成(readystatus 到达 4 )时执行的回调函数
		- beforeSend 在 执行 xmlHtpp.open 之前调用的回调函数
	- setting 还有其他参数 放在下面的链接里面咯
		- [jQuery.Ajax](https://www.jquery123.com/jQuery.ajax/) 
	- 其实嘛 你也可以吧 url 放入 setting 里面 
	
#### 为什么使用jQuery呢
`在访问一个不存在的页面时 会返回一个404页面`
- 如果用原生js
	- 返回的是一个404页面代码 
	- 即 一串 html 代码
- 如果是jQuery
	- 返回空 


### load方法

- load()
	- `载入远程HTML文件代码并插入至DOM中`
	- load(url,[data],[callback]);
	- url 待装入HTML网页的网址，必须是JSON格式，一旦url不为空，那么请求方式就默认改为POST
	- data（可选） 发送至服务器的 key/value 数据，在jQuery1.3中也可以接受一个字符串
	- callback（可选）载入成功时回调函数 
	- 如果只需要加载目标HTML网页内的某些元素，则可以通过load()方法的URL参数来达到目的
		- 通过URL参数制定选择符就可以方便的从加载过来的HTML文档中挑选内容
		- 语法结构是 "url selector"(注意：url 和 选择器 中间有个空格)
		- 如果返回的是&lt;h2>文本1&lt;/h2>&lt;h3>文本2&lt;/h3>
		- 如果url  后面 加上 " h2" ，那么就只会得到 h2 部分
	- 传递方式： load()方法的传递参数根据参数data来自动自定
		- 如果没有参数传递，采用GET方式传递，否则POST
	- 对于必须在加载完才能继续的操作，load()方法提供了回调函数
		- 该回调函数有三个参数
			- data 代表请求返回内容
			- textStatus 代表请求状态
			- XMLHttpRequest 代表请求状态
	- 任何一个节点都可以使用load()方法来加载Ajax，结果直接插入到html节点中
	
	
### get和post 方法
	
- $.get() （或$.post()）方法

- $.get() 方法使用GET方式来进行异步请求
	- 它的结构是 $.get(url, [data], [callback], [type]);
	- url，String类型，请求HTML页面的URL地址
	- data，Object类型，发送到服务器的key/value数据会作为Query/String附加到URL中
	- callback， function类型，载入成功时的回调函数
	- type，String类型，服务器返回内容的格式，包括xml,html,script,json等 
	
- $.get()方法的回调函数只有两个参数
	- data， 代表返回的内容，可以是一个XML文档，JSON文件，HTMl片段等
	- textstatus代表请求状态，其值可能是
		1. succuss
		2. error
		3. notmodify
		4. timeout
- $.get()和$.post()方法是jQuery中的全局函数，而find()等方法都是对jQuery对象进行操作的方法

```javascript
var url = this.href;
var args= {"time" : new Date()};
$.post(url, args, function(data){
	var name = $(data).find("name").text();
	var email = $(data).find("email").text();
	var website = $(data).find("website").text();
}, "JSON");

$.getJSON(url, args, function(data){ // 这里直接通过getJSON 将 data 转为JSON格式
	var name = data.person.name;
	var email = data.person.email;
	var website = data.person.website;
});
```

### Ajax的全局事件

- 所谓全局事件，就是在所有ajax调用的时候，都会执行的事件
	- 例如：我有一个请求开始的动画，我整个页面写了100个Ajax
	- 有一天 我想把所有的动画全部改了 我要改100个
	- 全局事件就是用在这个地方的

- .ajaxComplete()
	- 当Ajax请求完成后注册一个回调函数。这是一个 AjaxEvent。
	- Ajax > 全局 Ajax 事件处理器

- .ajaxError()
	- Ajax请求出错时注册一个回调处理函数，这是一个 Ajax Event。
	- Ajax > 全局 Ajax 事件处理器

- .ajaxSend()
	- 在Ajax请求发送之前绑定一个要执行的函数，这是一个 Ajax Event.
	- Ajax > 全局 Ajax 事件处理器

- .ajaxStart()
	- 在AJAX 请求刚开始时执行一个处理函数。 这是一个 Ajax Event.
	- Ajax > 全局 Ajax 事件处理器

- .ajaxStop()
	- 在AJAX 请求完成时执行一个处理函数。 这是一个 Ajax Event。
	- Ajax > 全局 Ajax 事件处理器

- .ajaxSuccess()
	- 绑定一个函数当 Ajax 请求成功完成时执行。 这是一个Ajax Event.

```JavaScript
$(document).ajaxComplete(function() {
 $( ".log" ).text( "Triggered ajaxComplete handler." );
});

```

### jQuery + Servlet实现 验证用户名是否存在

- HTML 写法

```html
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>检查用户名是否注册</title>
<script type="text/javascript" src="${pageContext.request.contextPath}/JS/jquery-1.12.4.min.js"></script>
<script type="text/javascript">
	$(function(){
		$("#usernmae").change(function(){//当value值改变时触发函数
			var val = $(this).val();//获取值
			val = $.trim(val);//去除前后的空格
			if(val != ""){
				var url = "${pageContext.request.contextPath}/Exist";
				var args = {"username" : val, "time":new Date()};
				$.post(url, args, function(data){
					$("#message").html(data);
				});
			}
		});
	});
</script>
<link >
</head>
<body>
	<form action="" method="post">
		UserName:<input type="text" id="usernmae" /><span id="message" style="color:red;"></span>
		<br/><input type="submit" value="submit" /> 
	</form>
</body>
</html>
```

- Servlet写法

```
package com.ajax.test;

import java.io.IOException;
import java.util.Arrays;
import java.util.List;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;


/**
 * Servlet implementation class Exist
 */
@WebServlet("/Exist")
public class Exist extends HttpServlet {
	private static final long serialVersionUID = 1L;
       
    /**
     * @see HttpServlet#HttpServlet()
     */
    public Exist() {
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
		System.out.println("post");
		String username = request.getParameter("username");
		List<String> 	userNames = Arrays.asList("AAA","BBB","CCC");
		response.setCharacterEncoding("utf-8");
		response.setContentType("text/html;charaset=utf-8");
		if (userNames.contains(username)) {
			response.getWriter().print("改用户名以存在");
		} else {
			response.getWriter().print("");
		}
		System.out.println("请求已发送");
	}

}
```

## 使用jackson包去生成json
1. 导入jar包
2. 创建ObjectMappter 对象
	- ObjectMapper mapper = new ObjectMapper();
3. 调用 mapper 的 writerValueAsString() 方法 把一个对象转为一个 Json 字符串

### 先写好一个class

```java
public class Customer{
	private String name;
	private String id;
	public String getName(){
		return name;
	}
	public String getId(){
		return id;
	}
	public void setName(String name){
		this.name = name;
	}
	public void setId(String id){
		this.id = id;
	}
	public Customer(String name, Stirng id){
		this.name = name;
		this.id = id;
	}
	public String getBrithday(){
		return "2018.12.01";
	}
	public String getAddress(){
		return "hubei-wuhan";
	}
} 
```

### 写一个main类去调用上述Customer

```java
public static void main(String[] args) throws JsonGenerationException, JsonMappingException, IOE......{
	ObjectMapper mapper = new ObjectMapper();
	
	Customer customer = new Customer("Name", "1001");
	String jsonStr = mapper.writeValueAsStirng(customer);
	System.out.println(jsonStr);
}
```

- `注意`
	- JackSon 使用 getter 方法来定位Json 对象的属性
	- 自行尝试上述的代码，你会发现 没有定义为 string 的 address 和 birthday 也会出现在最后的json中
	- 因为 addrss 和 birthday 都 定义了 get 方法
	- 即 只要是定义了 get 方法的，其返回值都会被放入json对象中
	- 如果 getName() 修改 为 getCustName()，那么最后放入json的键的名字就是 "csunstName"
	
- 可以通过在CLASS中添加注解来使某些get方法不放入json对象中
	- @JsonIgnore 放在 get 函数前面
	
## jQuery block ui
jQuery BlockUI 插件可以在不同锁定浏览器的同时，模拟同步模式下发起Ajax请求的行为
该插件激活时，会阻止用户在页面进行的操作，直到插件被关闭
BlockUI通过向DOM中添加元素实现其外观和组织用户交互的行为。

```html
<script type="text/javascript" src="http://malsup.github.io/min/jquery.blockUI.min.js"></script>
```

### 阻止页面交互

```
$.blockUI();
```

### 自定义消息阻塞UI

```
$.blockUI({message:'<h1><img src="busy.gif" />Just a moment...</h1>'});
```

### 自定义样式阻塞UI

```
$.blockUI({css:{backgroundColor: 'red'; color:'#fff'}});
```

### 解除对页面的遮罩

```
$.unblockUI();
```
### 使用缺省设置对所有的ajax请求都使用UI遮罩

```
$(document).ajaxStart($.blockUI).ajaxStop($.unblockUI);
```

### 学习学习

[http://bookshadow.com/weblog/2014/09/26/jquery-blockui-js-introduction/](好东西) 

#### 全局覆盖

```
// change message border
$.blockUI.defaults.css.border = '5px solid red';

// make fadeOut effect shorter
$.blockUI.defaults.fadeOut = 200;
```

#### 局部覆盖

```
// change message border
$.blockUI({ css: { border = '5px solid red'} });

...

// make fadeOut effect shorter
$.unblockUI({ fadeOut: 200 });

...

// use a different message
$.blockUI({ message: 'Hold on!' });

...

// use a different message
$('#myDiv').block({ message: 'Processing...' });
```

## 补充

- xmlHttp.response 和 xmlHttp.responseText 都是获取响应
	- responseText 获取的永远是以文本格式，字符串形式的响应体
	- response 会 根据 responseType的变化而变化
		- xmlHttp.responseType = "json" 则 response 则为 json 格式
		- 通过代码告诉请求代理对象服务器端响应的是JSON对象 

### 模板引擎的使用（这里用的是art-template）

- 首先我们要选择模板引擎
	- 市面上的模板引擎很多
		- art-template（国产）
		- Handlebars（最火）
		- ejs
		- doT
		- swig（不维护了）
		- ……
- 下载模板引擎JS文件
- 引入到页面中
	- &lt;script src="js/template-web.js">&lt;/script>
- 准备一个模板

```javascript

<script id = "tmple" type="text/javascript"></script>
// 如果 type 不为 text/javascript 那么 标签内部的内容不会作为 js语句 执行
````

- 准备一个数据
- 通过模板引擎的JS文件提供的一个函数/方法 将模板和数据整合的到渲染结果HTML
- 将渲染结果的HTML设置到某个元素的innderHTML中


## 跨域
- 跨域可以说Ajax没有一点关系，也可以说与Ajax有着绝对的联系

### 同源策略
	同源策略是浏览器的一种安全策略
	所谓同源是指：域名，协议，端口 完全相同
	只有同源的地址才可以通过Ajax的方式请求
	不同源地址之间，默认不能相互进行Ajax请求
	不同源地址之间的请求我们称之为跨域请求
	
不同源则报错：<font style="color:red">No 'Access-Control-Allow-Origin' header is present on the requested resource</font>
- 翻译过来就是 目标地址 不允许不同源的地址对其进行Ajax操作
### 解决方案





















