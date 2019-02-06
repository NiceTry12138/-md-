---
title: 从0开始的JavaWeb---H5篇
date: 2018-09-29 20:37:38
tags:
---
## Html  
### 什么是Html？
	HyperText Markup Language：超文本标记语言
	** 超文本：超出文本的范畴，使用html可以轻松实现
	** 标记：html所有的操作都是通过标记实现的。标记，就是标签  
	** 网页语言：超文本标记语言
### 第一个html程序：
	例如：创建Java文件 后缀名为.java
	**先编译，后运行（jvm）
	同理：html文件后缀是.html
	**直接通过浏览器就可以运行
### html规范：
	1. 一个html文件开始标签和结束的标签<html></html>
	2. html包含两个部分内容：
		<head></head> 
		<body></body> 
	3. html的标签有开始标签，也要有结束标签 
	4. html的代码不区分大小写<font> == <FONT> 
	5. 部分标签没有结束标签：
		例如：<br />//内部加个"/"，标签内结束

### *html的操作思想：  
	网页中有很多的数据，不同的数据可能需要不同的显示效果，这个时候需要使用标签把要操作的数据封装起来，通过修改标签的属性值实现标签内数据样式的变化。
	一个标签就像等于一个容器，想要修改容器内数据的样式，只需要改变容器的属性值，就可以实现容器内的数据样式的变化。

### html中常用的标签
#### 文字标签和注释标签
##### *文字标签：修改文字的样式
			例如：<font> </font>
			属性：color : 文字颜色(颜色的英文单词，或者十六进制rgb)
			     size : 文字大小（1~7）
##### 注释标签
		Java的注释有三种："//" , "/* */" "/*****/"
		html的注释: <!--  注释内容 -->(源文件可以查看的注释)

#### 标题标签，水平线标签和特殊字符
##### 标题标签
	<h1></h1><h2></h2> ~~~~  <h6></h6>
	文字大小 从h1 到 h6 以此变小，并且每个标签都会自动换行
##### 水平线标签
	<hr /> 标签内结束
	属性：
		**size：水平线的粗细
		**color：水平线的颜色
##### 特殊字符
	想在网页中显示 "<html>是一个特殊标签"
	如果直接写 "<html>是一个特殊标签"，则只会显示 "是一个特殊标签"
	需要转义"<html>"：
		&lt;   	--->     "<"   小于符号
		&gt;  	--->     ">"   大于符号
		&amp;  	--->     "&"   and符号 &
		&apos;	--->     "'"   英文单引号
		&quot;	--->     """   英文双引号
		&nbsp;  --->     " "   空格转义
	
#### 列表标签
	如果想在网页显示 列表的效果。
##### &lt;dl&gt;&lt;/dl&gt;：表示列表的范围
		在<dl>里面  <dt></dt>：上层内容
		在<dl>里面  <dd></dd>：下层内容
	例如：
		<dl>
			<dt>学习内容</dt>
				<dd>java</dd>
				<dd>C++</dd>
				<dd>Python</dd>
			<dt>学习进度</dt>
				<dd>没学</dd>
				<dd>没学</dd>
				<dd>没学</dd>
		</dl>

<dl>
<dt>学习内容</dt>
<dd>java</dd>
<dd>C++</dd>
<dd>Python</dd>
<dt>学习进度</dt>
<dd>没学</dd>
<dd>没学</dd>
<dd>没学</dd>
</dl>

##### &lt;ol&gt;&lt;ol&gt;：有序列表的范围
		在<ol></ol>标签内部：<li>
		属性：
			type：这是排序方式 默认（缺省）为 1. 2. 3....
				type = "a"
				type = "i"
			
	例如：
		<ol type="a">
		<li>java</li>
		<li>C++</li>
		<li>Python</li>
		</ol>
<ol type="a">
<li>java</li>
<li>C++</li>
<li>Python</li>
</ol>

##### &lt;ul&gt;&lt;/ul&gt;：无序列表的范围
	属性：
		type：
			circle	空心圆	
			disc	实心圆（默认）
			square	实心方块
	<ol type="a">
	<li>java</li>
	<li>C++</li>
	<li>Python</li>
	</ol>

<ul type="circle">
<li>java</li>
<li>C++</li>
<li>Python</li>
</yl>


#### &lt;img&gt;图像标签（重点）
	<img src="a.jpg" width="宽像素" height="高像素" alt="显示的文字"/>
	--src：图片的路径
	--width：图片的宽度
	--height：图片的高度
	--alt：图片上显示的文字，把鼠标移动到图片上面，停留片刻显示内容

#### 路径的介绍
##### 第一类：绝对路径
		D:\blog\lc_love_hehe\source\_posts\p.jpg
		http://www.baidu.com/b.jag
##### 第二类：相对路径
		一个文件相对于另外一个文件的位置
		三种写法：
			当图片与html在同一个文件夹内，直接使用 b.jpg
			当图片在html的同级文件夹img中，使用img/b.jpg
			当图片在html的上级文件夹中，../b.jpg
			
#### 超链接
##### 连接资源
	<a href="连接到资源的路径">显示在页面上的内容</a>
		href：连接的资源的地址
		target：设置打开的方式，默认是当前页打开。
			_blank：在新窗口打开
			_self：当前页打开
		当超链接不需要到任何地址的时候，href="#"
	<a href="https://usuiforhe.github.io/" target="_blank">test</a>
##### 定位资源
	<a name="top">顶部</a>//定义顶部的位置
	<a name="#top">回到顶部</a>//定位到网页中name为top的位置，记得加上#

	<pre>原样输出
	例如：
	public static void main(String[] args){
		Syste.out.println("hello world");
	}
	&lt;pre&gt;
	public static void main(String[] args){
		Syste.out.println("hello world");
	}
	&lt;/pre&gt;
public static void main(String[] args){	Syste.out.println("hello world");}
<pre>
public static void main(String[] args){
	Syste.out.println("hello world");
}
</pre>
`加上了 <pre> 标签后，原本一行的代码，变成了我们要的换行的效果`

#### 表格标签
	可以对数据进行格式化，使数据显示更加清晰
	<table></table>:表示表格的范围
	在<table>里面： <caption>表格标题
	在<table>里面： <tr>
	在<tr>里面：<td>
	
	画图分析表格的写法：
		首先定义一个表格的范围使用table
			定义一行使用 tr
			定义一个单元格使用 td
		操作技巧：
			首先数有多少行，数每行里有多少个单元格
		例如：
			<table>
				<tr>
					<td>学科</td>
					<td>学习进度</td>
					<td>梦想</td>
				</tr>
				<tr>
					<td>python</td>
					<td>没学</td>
					<td rowspan="3">想学</td>
				</tr>
				<tr>
					<td>C++</td>
					<td>没学</td>
				</tr>
				<tr>
					<td>Java</td>
					<td>没学</td>
				</tr>
			</table>
		属性：
		<table>中：
			border：表格线的粗细
			bordercolor：表格线的颜色
			cellspacing：表格之间的距离
			align：left center right  框中文字的位置
		<td>中：
			colspan：0~无穷大，跨列
			rowspan：0~无穷大，跨行
<table>
	<tr>
		<td>学科</td>
		<td>学习进度</td>
		<td>梦想</td>
	</tr>
	<tr>
		<td>python</td>
		<td>没学</td>
		<td rowspan="3">想学</td>
	</tr>
	<tr>
		<td>C++</td>
		<td>没学</td>
	</tr>
	<tr>
		<td>Java</td>
		<td>没学</td>
	</tr>
</table>

#### 表单标签
`可以提交数据到服务器的标签，这个过程可以使用表单标签实现`  

> &lt;form&gt;&lt;/form&gt;：定义表单范围  
输入项：可以输入内容或者选择内容的部分  
	大部分的输入项 使用 &lt;input type = "输入类型" /&gt;  

	Input  类型：type = "email/url/number/range/date picker/search/color/tel"  	
	<input type="password">密码框
	<input type="radio" name="sex"/>女<input type="radio" name="sex"/>男  单选框
	<input type="checkbox" name="love"/>苹果<input type="checkbox" name="love"/>香蕉<input type="checkbox" name="love"/>栗子  多选框
	<input type = "url" name = "url">	手机端弹出字母键盘，电脑端无差别  
	<input type = "email" name = "email">	手机端弹出字母键盘，电脑端无差别  
	<input type = "tel" name = "tel">	手机端弹出数字键盘，电脑端无差别  
	<input type = "number" name = "number">	手机端弹出数字键盘，电脑端右边多处两个按钮控制加减，只能输入参与运算的内容“+ - . 1 2 3 4 5 6 7 9 e”  
	data picker input类型:  
		date —— 选取 日， 月， 年  
		month —— 选取月，年  
		week ——	选取 周和年  
		time —— 	选取时间（小时和分钟）	  
		datetime	—— 选取时间，日，月，年（utc时间）  
		datetime-local —— 选取时间，日，月， 年（本地时间）  使用方法一样 
	<input type = "date" name = "date" > 手机端显示的是 日期键盘  
	<input type = "range" name = "range" min = "最小值" max = "最大值">  
	<input type = "image" src="a.jpg"/>设置按钮为图片，作用是提交
	<input type = "search" name = "search" >  
	<input type = "color" name = "color">弹出颜色选择  
	<input type = "hidden"/> 	隐藏项，不会显示在页面中的
	<input type = "button" />	普通按钮
	<input type = "submit" /> 	提交按钮
	<input type = "reset" value="你想显示的文字"/>	重置按钮
	<selsect>
		<option>1</option>
		<option>2</option>
		<option>3</option>
	</select>下拉选项
	<textarea cols="列数" rows="行数"></textarea> 文本域

`最好每个输入项都有个name属性，方便后台提取数据。后台通过name属性获取对应输入的值`

	表单属性：  
	autocomplete/autofocus/multiple/placeholder/required/action/method  
	action	是提交数据到的那个页面
	method	常用的就两种“get”“post”，默认get
	enctype	关于文件上传的属性
	<form autocomplete = "on"（#自动完成功能，存下之前提交过的字段#）action = "****"    ausofocous = "">  
		<input type = "text" name = "text"  autofocus = "autofocus">(#不写  autocomplete 默认开启存储  autofocus 光标自动确定该input#)  
		<input type = "email" name = "email" autocomplete = "off">（#关闭自动存储#）  
		<input type = "file" multiple = "muliple" / >(#muliple 是乘法，代表多个的意思，同时上传多个文件#)  
		ps. multiple 在类型为type的时候，也可以用，多个邮箱之间用 分号 隔开。 如果没有multiple ，email类型也可以传多个email，但是用了multiple 的 input，会传出一个数组到后台，而没有用的则会传出一整个字符串，难以操作。  
		<input type = "text" placeholder = "用户名" />(#提示输入用户名，开始输入时提示消失#)  
		ps. placeholder 适用于： text, search, url, tel, email, password。  
		<input type = "text" required = "required" /> （#required 规定必须在提交之前填写输入域（不能为空）#）  
		<input type = "submit">  
	</form>`
#### 其他标签
	<b>		加粗
	<s>		删除线
	<u>		下划线
	<i>		斜体
	<pre>	原样输出
	<sub>	下标
	<sup>	上标
	<div>	盒子，自带换行
	<span>	盒子，不带换行

#### html的头标签
	html由两部分组成 head 和 body
	在head里面的标签就是头标签
		title：显示在标签上显示的内容
		base：为页面上的所有链接规标题栏显示的内容定默认地址或默认目标（target属性）
		例如：
			<base target="_blank">
			//这是所有的超链接都是新窗口打开
		meta：可以提供有关页面的基本信息
		例如：
			<meta http-equiv="refresh" content="3;url=01-hello.html">
			// refresh 模拟页面请求， 3 3秒后， url 跳转的目标页面
		link：定义文档与外部资源的关系

#### 框架标签（过时）
	<frameset>
		属性：
			rows：按行进行划分
			cols：按列进行划分
		<frameset rows="80,*">划分为两行，第一行高80		
	<frame>
		具体显示的页面
		<frame name = "lower_left" src="b.html">
	使用框架标签时候，不能写在body里面，需要把body去掉。

### HTML样例
	<body>
	    <header>
	        <div>logo</div>
	        <nav>
	            <a href="test.html">首页</a>
	            <a href="#">介绍</a>
	            <a href="#">案例</a>
	            <a href="#">链接</a>
	            <a href="#">关于</a>
	        </nav>
	    </header>
	    <section>
	        <aside>
	            <a href="#se1">setcion1</a>
	            <a href="#se2">section2</a>
	            <a href="#se3">section3</a>
	        </aside>
	        <article>
	            Today, Rikka is going to learn how to use BIT to solve some simple data structure tasks. While studying,
	            She finds there is a magic expression x&(−x) in the template of BIT. After searching for some literature,
	            Rikka realizes it is the implementation of the function lowbit(x).
	            lowbit(x) is defined on all positive integers. Let a1...am be the binary representation of x while a1 is the
	            least significant digit, k be the smallest index which satisfies ak = 1. The value of lowbit(x) is equal to
	            2
	            k−1
	            .
	            After getting some interesting properties of lowbit(x), Rikka sets a simple data structure task for you:
	            At first, Rikka defines an operator f(x), it takes a non-negative integer x. If x is equal to 0, it will return
	            0. Otherwise it will return x − lowbit(x) or x + lowbit(x), each with the probability of 1
	            2
	            .
	            Then, Rikka shows a positive integer array A of length n, and she makes m operations on it.
	            There are two types of operations:
	            • 1 L R, for each index i ∈ [L, R], change Ai to f(Ai).
	            • 2 L R, query for the expectation value of ∑R
	            i=L Ai
	            . (You may assume that each time Rikka calls f,
	            the random variable used by f is independent with others.)
	            Input
	            The first line contains a single integer t(1 ≤ t ≤ 3), the number of the testcases.
	            The first line of each testcase contains two integers n, m(1 ≤ n, m ≤ 105
	            ). The second line contains n
	            integers Ai(1 ≤ Ai ≤ 108
	            ).
	            And then m lines follow, each line contains three integers t, L, R(t ∈ {1, 2}, 1 ≤ L ≤ R ≤ n).
	            Output
	            For each query, let w be the expectation value of the interval sum, you need to output (w × 2
	            nm)
	            mod 998244353.
	            It is easy to find that w × 2
	            nm must be an integer.
	
	        </article>
	    </section>
	    
	    <input placeholder="选择手机品牌" list="phtonlist" /><!--input的list 必须和datalist的id相同-->
	    <datalist id="phtonlist">
	        <option value="1">1</option>
	        <option value="2">2</option>
	        <option value="3">3</option>
	        <option value="4">4</option>
	    </datalist>
	    <meter value="220" min="20" max="380" low="200" high="240" optimum="220"></meter><!-- 当前值为220 最低为20 最高为380 标准在200~240之间 最好的取值为220-->
	    <meter value="180" min="20" max="380" low="200" high="240" optimum="220"></meter>
	    <meter value="260" min="20" max="380" low="200" high="240" optimum="220"></meter>
	    <meter value="0.75">75%</meter>
	    <progress value="30" max="100"></progress>
	    <progress max="100"></progress>
	    <details>
	        <summary>你要显示的标题</summary>
	        内容：。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。。
	    </details>
	    <menu type="toolbar">
	        <li>
	            <menu aria-label="File">
	                <button type="button">new1</button>
	                <button type="button">new2</button>
	                <button type="button">new3</button>
	            </menu>
	        </li>
	        <li>
	
	            <button type="button">new4</button>
	            <button type="button">new5</button>
	            <button type="button">new6</button>
	        </li>
	    </menu>
	    <footer>
	        copyright......
	    </footer>
	    <p>我们来<ruby>聊<rt>liao</rt></ruby>天</p>
	</body>
## CSS-层叠样式表

### 解释	
#### 层叠
	一层一层的，与优先级有关
#### 样式表
	有很多的属性和属性值，改变标签的属性值，是标签变换
#### 作用
	CSS将网页内容和显示样式进行分离，提高了显示功能，解决了html代码对样式定义的重复，提高了后期样式代码的可维护性。

### CSS和Html的结合方式
	1. 在每个html标签上都有一个style属性。通过style属性修改标签样式
		<span style="background-color:red; color=green;">测试</span>
	2. 使用html的一个标签实现 <style> 标签，写在head里面
		<style type="text/css">
			div{
				background-color:red;
				color = green
			}//所有div的样式都这样
		</style>
	3. 在<style>标签中使用语句 @import url (css文件的路径)
		<style type="text/css">
			@import url(div.css)
		</style>
	4. 使用头标签<link>,引入外部css文件
		<link rel="srtlesheet" type="text/css" href="css_3.css" />
	Ps.第三种结合方式，缺点：在某些浏览器下不支持。一般来说，是用第四种结合方式。

### CSS的优先级
	从上到下，从外到内，CSS的优先级从低到高。后加载的优先级高。

### CSS书写规范
	1. 选择器名称{
		属性名：属性值；
		属性名：属性值；
	}
	2. 属性与属性之间用分号隔开
	3. 属性与属性值之间用冒号链接
	4. 如果一个属性有多个属性值的话，那么多个值用空格隔开

### 选择器
#### id选择器
	<标签 id="test">文字内容</标签>
	在CSS文件中：
		通过 #test{
			background-color: red;
		}来选择 id 为test的标签。也就是说 id 前面加上 " # "
#### 类选择器
	<标签 class="test">文字内容</标签>
	在CSS文件中：
		通过 .test{
			background-color:red;
		}来选择 class 为test的标签。也就是说 class 前面加上 " . "
#### 标签选择器
	<标签>文字内容</标签>
	在CSS文件中：
		通过 标签{
			background-color:red;
		}来选择 标签

`class 选择器的优先级 > 标签选择器的优先级`
`id选择器的优先级 > class选择器的优先级`
`标签内部的style属性的优先级 > id 选择器的优先级`

#### 关联选择器
	<div><p>test</p></div>
	要选中 p 标签 那么CSS这样写
		div p{
			background-color:red;
		}两个中间一个空格，这样就选中 div 子标签中的 p 标签

#### 组合选择器
	<div>test111</div>
	<p>test222</p>
	想把div和p设置成一样的样式，那么CSS中这么写
		div,p{
			background-color:red;
		}中间用逗号连接，表示两个都选中

#### 伪类元素选择器
	CSS里面提供了一些定义好的样式，可以拿过来使用
	原始状态		鼠标放上去的状态		点击		 	点击之后
	：link		：hover				：active		visited
	例如CSS文件中：
		a:link{
			background-color: red;
		}
		a:hover{
			background-color: blue;
		}
		a:active{
			background-color: black;
		}
	第一个字符		第一行			在文字标签前面加上
	:first-letter	:first-line		：before
	例如CSS文件中：
		p:before
		{
			content:"台词：";
		}那么 所有的 p 标签前面 都会加上 "台词" 这两个字

<table>
<tr> <td>选择符类型</td> <td>表达式</td> <td>描述</td></tr>
<tr><td>子串匹配的属性选择符</td><td> E[att^="val"] </td><td>匹配具有att属性、且值以val开头的E元素 </td> </tr>
<tr> <td>子串匹配的属性选择符</td> <td>E[att$="val"]</td> <td>匹配具有att属性、且值以val结尾的E元素 </td> </tr>
<tr> <td>子串匹配的属性选择符</td> <td>E[att*="val"]</td> <td>匹配具有att属性、且值中含有val的E元素 </td> </tr>
<tr> <td>结构性伪类</td> <td> E:root</td> <td> 匹配文档的根元素。在HTML中，根元素永远是HTML </td> </tr>
<tr> <td>结构性伪类</td> <td> E:nth-child(n)</td> <td> 匹配父元素中的第n个子元素E </td> </tr>
<tr> <td>结构性伪类</td> <td> E:nth-last-child(n)</td> <td> 匹配父元素中的倒数第n个结构子元素E</td> </tr>
<tr> <td>结构性伪类 </td> <td>E:nth-of-type(n)</td> <td> 匹配同类型中的第n个同级兄弟元素E   
<tr> <td>结构性伪类</td> <td> E:nth-last-of-type(n)</td> <td> 匹配同类型中的倒数第n个同级兄弟元素E </td> </tr>
<tr> <td>结构性伪类</td> <td> E:last-child</td> <td> 匹配父元素中最后一个E元素</td> </tr>
<tr> <td>结构性伪类 </td> <td>E:first-of-type </td> <td>匹配同级兄弟元素中的第一个E元素 </td> </tr>
<tr> <td>结构性伪类 </td> <td>E:only-child </td> <td>匹配属于父元素中唯一子元素的E</td> </tr>
<tr> <td>结构性伪类 </td> <td>E:only-of-type </td> <td>匹配属于同类型中唯一兄弟元素的E</td> </tr>
<tr> <td>结构性伪类</td> <td> E:empty</td> <td> 匹配没有任何子元素（包括text节点）的元素E</td> </tr>
<tr> <td>目标伪类</td> <td> :target</td> <td> 匹配相关URL指向的E元素</td> </tr>
<tr> <td>UI元素状态伪类</td> <td> E:enabled</td> <td> 匹配所有用户界面（form表单）中处于可用状态的E元素 </td> </tr>
<tr> <td>UI元素状态伪类 </td> <td>E:disabled </td> <td>匹配所有用户界面（form表单）中处于不可用状态的E元素 </td> </tr>
<tr> <td>UI元素状态伪类</td> <td> E:checked</td> <td> 匹配所有用户界面（form表单）中处于选中状态的元素E </td> </tr>
<tr> <td>UI元素状态伪类</td> <td> E::selection</td> <td> 匹配E元素中被用户选中或处于高亮状态的部分</td> </tr>
<tr> <td>否定伪类</td> <td> E:not(s)</td> <td> 匹配所有不匹配简单选择符s的元素E</td> </tr>
<tr><td>通用兄弟元素选择器</td> <td> E ~ F </td> <td>匹配E元素之后的F元素 </td> </tr>
</table>

### 盒子模型
	div+CSS，给div一个样式，设置它的位置以及外观。又因为这div就像一个盒子一样，所以也叫做盒子模型。
`在进行布局前需要把数据封装到一块一块的区域内`
#### 边框
	属性：
		border：统一设置
			none | hidden | dotted | dashed | solid | double | groove | ridge | inset | outset
			无边框| 隐藏边框|点线或实线|虚线或实线| 实线 |双线边框  | 3D凹槽 | 3D凸槽 |3D凹边 |3D凸边
		border-top：上边框
		border-bottom：下边框
		border-left：左边框
		border-right：右边框
		border: 粗细（px） 样式（上述）颜色；
#### 内边距
	padding：length（px）//统一设置
	padding-bottom	:	文字内容距离下边框的距离
	padding-left	:	文字内容距离左边框的距离
	padding-right	:	文字内容距离有边框的距离
	padding-top		:	文字内容距离上边框的距离
#### 外边距
	margin：外边距，边框距离外边框的距离
	margin：length（px）//统一设置
	margin-top		:	边框距离上外边框的距离
	margin-bottom	:	边框距离下外边框的距离
	margin-right	:	边框距离右外边框的距离
	margin-left		:	边框距离左外边框的距离

### CSS的布局的漂浮
	float：none | left | right
	none	：默认值。对象不漂浮
	left	：文本流向对象的右边
	right	：文本流向对象的左边

### CSS的布局的定位
	Position	属性：
		static:默认值。无特殊定位，对象遵循HTML定位规则
		absolute：将对象从文档流中脱出，使用left,right,top,bottom等属性相对于其进行绝对定位
		——————即，这个盒子独立出来，不由html自动按文档流分配位置，后面的盒子自动补齐该和自动空位
		relative：对象不可层叠，但将依据left,right,top,bottom等属性在正常文档流中偏移位置。
		——————即，这个盒子没有从文档流中拖出，位置还在，但是可以移动而不影响其他的盒子的原有位置

## Javascript
### JavaScript简介
	JavaScript是基于对象和时间驱动的脚本语言，主要应用在客户端
#### 基于对象
	提供好了很多对象，可以直接拿过来使用
#### 事件驱动
	html做网站是静态效果，加入了js后就可以完成动态的效果
#### 特点
	1. 交互性（信息的动态交互）
	2. 安全性（不可以直接访问本地磁盘）
	3. 跨平台性（只要是可以解析js的浏览器都可以执行，与平台无关）
### JavaScript的组成
	三部分：
	1. ECMAScript
		ECMA：欧洲计算机协会
		由ECMA组织指定的js语法，语句......
	2. BOM
		broswer object model：浏览器对象模型
	3. DOM
		document object model：文档对象模型

### JavaScript与HTML的结合
	1. 使用一个标签
		<script type="text/javascript">JavaScript代码</script>
	2. 使用script引入外部标签文件
		创建一个js文件，写js代码
			<script type="text/javascript" src="a.js"></script> 这样写的话 <script></script>中间的代码不会执行

### JavaScript基本语法
#### js的原始类型和声明变量
	1. string：字符串
		var str="abc";
	2. number：数字类型
		var m = 123;
	3. boolean：数字类型
		var flag=true;
	4. null:对象引用为空
	5. undifined：定义了一个变量，但是这个变量没有赋值
		var aa；
	用typeof（变量名）；查看当前变量的数据类型
#### js的语句
	1.判断语句：
	 	1. if语句
		if(a == 5){
			alert("5");
		}else{
			alert("不是5")	
		}
		2. switch语句（支持所有的数据类型）
		switch(变量){
			case 5:操作;break;
			case 6:操作;break;
			case 7:操作;breal;
			default:操作;break;
		}
	2. 循环语句
		1. for循环
			for(var i=0; i<10; i++){
				alert(i);
			}
		2. whilt循环
			var i=4;
			whilt(i--){
				alert(i);
			}
#### js的运算符
	1. -
	2. +
	3. *
	4. /
	5. &
	6. ++
	7. --
	8. +=
	9. -=
##### 字符串加减
		j=123
		alert(j/1000*1000)
		java中输出的 0； 但是JavaScript中输出的 123；
		js中不区分整形浮型点
		var str = "457"
		alert(str+1);
		Java和JavaScript中输出的都是4571; 加法做的是字符串相见
		alert(str-1);
		JavaScript输出的是 456，即进行了减法运算
		alert("abc"-1);
		JavaScript输出NAN，提示错误，不是一个数字。 
		
##### Boolean的操作
	var flag=true;
	alert(flag+1);
	JavaScript中输出的是 2。也就是说 true = 1；
	反之，flase = 0。

##### === 和 == 的区别
	JavaScript中， == 用于判断两个参数的值是否相等 === 用于判断两个参数 类型和值是否都相等
		例如：
			var x = "5", y = 5;
			x == y 则为 true
			x === y 则为false
#### 引入知识
	直接向页面输出的语句（可以直接把内容显示在页面上）
	document.write("aaa");
	document.write("<hr />");
	可以直接写入数据，也可以写入html代码，当然也可以混合都写

### js的数组
	js数组中，写什么都可以,可以是数据的混合，可以同时包括int，string或者其他类型
#### 定义数组的三种方式
	1. var arr=[1,2,"34"];
	2. 使用内置的对象 Array对象
		var arr = new Array(5);//定义一个数组，数组长度是5
	3. 使用内置对象 Array对象
		var arr2 = new Array(3,4,5);//定义一个数组，数组里面的元素为 3，4，5
#### 数组的属性
	length：表示数组的长度
		var len = arr.length;
	数组的长度是可以变的
	数组可以存放不同的数据类型的数据

### js的函数
#### 在js里面定义函数有三种定义方式
	1. 关键字：function
		funciton 方法名（参数列表）{
			方法体；
			返回值；（返回值可有可无）
		}
	2. 匿名函数：function
		var func = funtion （参数列表）{
			方法体和返回值；
		}
		调用直接  func();
	3. 内部对象：Function（用的少，了解就行）`动态函数`
		var func = new Function("参数列表"，“方法体和返回值”);
		var test = new Function("x,y","var sum;sum=x+y;return sum;");
### js的全局变量和局部变量
#### 全局变量
	在script标签内部顶一个变量，这个变量在页面中js部分都可以使用
#### 局部变量
	在方法内部定义一个变量，只能在方法内部使用

#### 测试
	全局变量：
		<script>
			var a = 10;
			function func(){
				alert(a);
			}
			func();
		</script>
		<script>
			alert(a);
		</script>
		可以跨script标签使用的变量。称之为全局变量
	局部变量：
		<script>
			function func(){
				var a = 10;
				alert(a);
			}
			func();
			alert(a);//报错
		</script>
		局部变量只能在方法内部使用

### script应该放的位置
#### 位置差别
	<script>原则上放任意位置都可以执行，但是还是要注意位置
	html文档是从上到下解析的，如果用js去获得html的标签，一定要在获取标签的后面，不然会得到一个 null 的变量，导致错误。
#### 建议
	把script标签放到</body>后面，</html>前面

#### js的重载
	function add1(a, b){ return a+b }
	function add1(a, b, c){ return a+b+c }
	function add1(a, b, c, d){ return a+b+c+d }
	add1(2,3)	add(2,2,3)	add(2,2,3,3)
	第一个得出结果NAN，第二个得出结果NAN，第三个得出正确结果
##### 为什么呢？

### JavaScript基础DOM

#### js的String对象
##### 方法属性
###### 属性	
	只有一个需要注意：length  字符串的长度
###### 方法
####### 与html相关的方法
	设置数据样式的方法
	1. bold() 使用粗体显示字符串  document.write(str.bold());
	2. fontcolor() 使用指定的颜色来显示字符串  document.write(str.fontcolor("red"));
	3. fontsize() 使用指定的尺寸来显示字符串  document.wirte(str.fontsize(1));//参数值为1~7
	4. link() 将字符串显示为链接  document.write(str.link(www.baidu.com));//即字符串成为一个超链接
	5. big() 用大号字体显示字符串  document.write(str.big());
	6. blink() 显示闪动字符串  document.write(str.blink());
	7. sup() 把字符串显示为上标  
	8. sub() 把字符串显示为下标  
	9. small() 使用小字号来显示字符串 
	10. strike() 使用删除线来显示字符串  
####### 与Java相似的方法
	对数据进行操作的方法
	1. split() 把字符串分割为字符串数组  
	2. charAt() 返回在指定位置的字符  str.cjarAt(1);
	3. concat() 连接字符串  str.concat(str2);
	4. indexOf() 检索字符串  str.indexof("as");//不存在返回-1
	5. charCodeAt() 返回在指定的位置的字符的 Unicode 编码   
	6. fixed() 以打字机文本显示字符串  
	7. fromCharCode() 从字符编码创建一个字符串  
	8. italics() 使用斜体显示字符串  
	9. lastIndexOf() 从后向前搜索字符串  
	10. localeCompare() 用本地特定的顺序来比较两个字符串  
	11. match() 找到一个或多个正则表达式的匹配  
	12. replace() 替换与正则表达式匹配的子串  str.replace("a", "c");//把a替换成c
	13. search() 检索与正则表达式相匹配的值  
	14. slice() 提取字符串的片断，并在新的字符串中返回被提取的部分   
	15. substr() 从起始索引号提取字符串中指定数目的字符  str.substr(start, length);截取从start开始长度为length的字符串
	16. substring() 提取字符串中两个指定的索引号之间的字符  str.substring(start, end);截取从start开始 end 截至的字符串
	17. toLocaleLowerCase() 把字符串转换为小写  
	18. toLocaleUpperCase() 把字符串转换为大写  
	19. toLowerCase() 把字符串转换为小写  
	20. toUpperCase() 把字符串转换为大写  
	21.	toSource() 代表对象的源代码  
	22. toString() 返回字符串   
	23. valueOf() 返回某个字符串对象的原始值  

### js的Date对象
	js获取当前事件
		var date = new Date();
#### Date对象的方法
	1. toLocaleString() 根据本地时间格式，把 Date 对象转换为字符串 date.toLocaleString();
	2. toLocaleTimeString() 根据本地时间格式，把 Date 对象的时间部分转换为字符串
	3. toLocaleDateString() 根据本地时间格式，把 Date 对象的日期部分转换为字符串
	4. setFullYear() 设置 Date 对象中的年份（四位数字）
	5. setMonth() 设置 Date 对象中月份 (0 ~ 11) 注意是 0~11，而不是1~12 ！！！！
	6. setHours() 设置 Date 对象中的小时 (0 ~ 23)
	7. setMinutes() 设置 Date 对象中的分钟 (0 ~ 59)
	8. setSeconds() 设置 Date 对象中的秒钟 (0 ~ 59)
	9. setMilliseconds() 设置 Date 对象中的毫秒 (0 ~ 999)
	10. getFullYear() 从 Date 对象以四位数字返回年份
	11. getMonth() 返回 Date 对象的月份 (0~11)  setMonth() 设置 Date 对象中月份 (0 ~ 11)。 
	12. getHours() 返回 Date 对象的小时 (0 ~ 23)
	13. getMinutes() 返回 Date 对象的分钟 (0 ~ 59) 
	14. getSeconds() 返回 Date 对象的秒数 (0 ~ 59)
	15. getMilliseconds() 返回 Date 对象的毫秒(0 ~ 999)
	16. getTime() 返回 1970 年 1 月 1 日至今的毫秒数。 

### js的Math对象
	全都是静态方法，调用函数时直接	Math.方法名（参数）
#### Math对象的方法
	1. abs(x) 返回数的绝对值
	2. acos(x) 返回数的反余弦值
	3. asin(x) 返回数的反正弦值
	4. atan(x) 以介于 -PI/2 与 PI/2 弧度之间的数值来返回 x 的反正切值
	5. atan2(y,x) 返回从 x 轴到点 (x,y) 的角度（介于 -PI/2 与 PI/2 弧度之间）
	6. ceil(x) 对数进行上舍入
	7. cos(x) 返回数的余弦
	8. exp(x) 返回 e 的指数
	9. floor(x) 对数进行下舍入
	10. log(x) 返回数的自然对数（底为e）
	11. max(x,y) 返回 x 和 y 中的最高值
	12. min(x,y) 返回 x 和 y 中的最低值
	13. pow(x,y) 返回 x 的 y 次幂
	14. random() 返回 0 ~ 1 之间的随机数
	15. round(x) 把数四舍五入为最接近的整数 
	16. sin(x) 返回数的正弦
	17. sqrt(x) 返回数的平方根
	18. tan(x) 返回角的正切
	19. toSource() 返回该对象的源代码
	20. valueOf() 返回 Math 对象的原始值 
#### Math对象的属性
	1. E 返回算术常量 e，即自然对数的底数（约等于2.718）
	2. LN2 返回 2 的自然对数（约等于0.693）
	3. LN10 返回 10 的自然对数（约等于2.302）
	4. LOG2E 返回以 2 为底的 e 的对数（约等于 1.414）
	5. LOG10E 返回以 10 为底的 e 的对数（约等于0.434）
	6. PI 返回圆周率（约等于3.14159）
	7. SQRT1_2 返回返回 2 的平方根的倒数（约等于 0.707）
	8. SQRT2 返回 2 的平方根（约等于 1.414）

### js的全局函数
	由于不属于任何一个对象，直接名称使用
	1. decodeURI()	解码某个编码的URI
	2. decodeURIComponent()		解码一个编码的URI组件
	3. encodeURI()	把字符串编码为URI
	4. encodeURIComponent()		把字符串编码为URI组件
	5. escape()		对字符串进行编码
	6. eval()		计算JavaScript字符串，并把它作为脚本代码来执行
	7. getClass()	返回一个javaObject的JavaClass
	8. isFinite()	检查某个值是否为有穷大的数
	9. isNaN（）		检查某个值是否是数字
	10. parseFloat()	解析一个字符串并返回一个浮点数
	11. parseInt()		解析一个字符串并返回一个整数
	12. unescape()		对由escape()编码的字符串进行解码
## js函数的重载
### js的重载是否存在？
	不存在重载。函数名相同的以后定义的为准。也就是说方法名相同的情况下，后定义的会覆盖掉先定义的方法。
### js可以通过其他的方式去模拟重载
	在js的函数中，传入的参数列表，可以通过一个js自带的 aruguments[]数组去访问传入的参数。
	例如：
		function add(a, b, c){
			arguments[0] == a;
			arguments[1] == b;
			arguments[2] == c;
		}
	js的函数你可以传入多个参数，例如 add(1,2,3,4,5,6)，虽然定义的 add函数只有三个参数，
	但是通过arguments可以获得 传入的所有参数 1,2,3,4,5,6 只是 a=1,b=2,c=3 罢了
	通过arguments.length 判断传入参数大小，以此来手动进行重载

## js的bom对象
	bom：broswer object model 浏览器对象模型
	通过bom对象，可以直接对浏览器进行操作。
### 有哪些对象
#### navigator
	Navigator 对象包含有关浏览器的信息。
##### 对象属性
	1. appCodeName 返回浏览器的代码名 
	2. appMinorVersion 返回浏览器的次级版本
	3. appName 返回浏览器的名称	alert(navigator.appName);
	4. appVersion 返回浏览器的平台和版本信息
	5. browserLanguage 返回当前浏览器的语言
	6. cookieEnabled 返回指明浏览器中是否启用 cookie 的布尔值
	7. cpuClass 返回浏览器系统的 CPU 等级
	8. onLine 返回指明系统是否处于脱机模式的布尔值
	9. platform 返回运行浏览器的操作系统平台
	10. systemLanguage 返回 OS 使用的默认语言
	11. userAgent 返回由客户机发送服务器的 user-agent 头部的值
	12. userLanguage 返回 OS 的自然语言设置 

##### 对象方法
	1. javaEnabled() 规定浏览器是否启用 Java
	2. taintEnabled() 规定浏览器是否启用数据污点 (data tainting)

#### screen（屏幕对象）
	Screen 对象包含有关客户端显示屏幕的信息。
##### 对象属性
	1. availHeight 返回显示屏幕的高度 (除 Windows 任务栏之外)
	2. availWidth 返回显示屏幕的宽度 (除 Windows 任务栏之外)
	3. bufferDepth 设置或返回调色板的比特深度
	4. colorDepth 返回目标设备或缓冲器上的调色板的比特深度
	5. deviceXDPI 返回显示屏幕的每英寸水平点数
	6. deviceYDPI 返回显示屏幕的每英寸垂直点数
	7. fontSmoothingEnabled 返回用户是否在显示控制面板中启用了字体平滑 
	8. height 返回显示屏幕的高度
	9. logicalXDPI 返回显示屏幕每英寸的水平方向的常规点数
	10. logicalYDPI 返回显示屏幕每英寸的垂直方向的常规点数
	11. pixelDepth 返回显示屏幕的颜色分辨率（比特每像素）9 
	12. updateInterval 设置或返回屏幕的刷新率
	13. width 返回显示器屏幕的宽度。 

#### location
	对象包含有关当前 URL 的信息。
##### 对象属性
	1. ash 设置或返回从井号 (#) 开始的 URL（锚）
	2. host 设置或返回主机名和当前 URL 的端口号
	3. hostname 设置或返回当前 URL 的主机名
	4. href 设置或返回完整的 URL`(重点)` 
		1. location.href;//得到当前请求的url地址。
		2. location.href="你要跳转的地址,例如：www.baidu.com"这样就会跳转页面
	5. pathname 设置或返回当前 URL 的路径部分
	6. port 设置或返回当前 URL 的端口号
	7. protocol 设置或返回当前 URL 的协议
	8. search 设置或返回从问号 (?) 开始的 URL（查询部分）
	
##### 对象方法
	1. assign() 加载新的文档
	2. reload() 重新加载当前文档
	3. replace() 用新的文档替换当前文档。 


#### history（历史）
	请求的url的历史记录

##### 对象属性
	1. length 返回浏览器历史列表中的 URL 数量
##### 对象方法
	1. back() 加载 history 列表中的前一个 URL  history.back()
	2. forward() 加载 history 列表中的下一个 URL	history.forward()
	3. go() 加载 history 列表中的某个具体页面

#### window
	Window 对象表示浏览器中打开的窗口。包含location,navicator,history,screen对象
	它是一个顶层对象
#### 属性
	opener 获得创建窗口的窗口 即用a.html打开b.html，在b.html中通过window.opener获得a.html的窗口对象

##### 对象方法（都要记住）
	1. alert() 显示带有一段消息和一个确认按钮的警告框
	2. blur() 把键盘焦点从顶层窗口移开
	3. clearInterval() 取消由 setInterval() 设置的 timeout 
		1. window.clearInterval(id);
		2. id为 setInterval()返回的id值
	4. clearTimeout() 取消由 setTimeout() 方法设置的 timeout
		1. window.clearTimeout(id);
		2. id为 setTimeout()返回的id值
	5. close() 关闭浏览器窗口
		1. windown.close();
		2. 浏览器兼容性差
	6. confirm() 显示带有一段消息以及确认按钮和取消按钮的对话框
		1. window.confirm("传入的消息")
		2. 返回一个Boolean类型值。确定为ture，取消为false
	7. createPopup() 创建一个 pop-up 窗口
	8. focus() 把键盘焦点给予一个窗口 
	9. moveBy() 可相对窗口的当前坐标把它移动指定的像素
	10. moveTo() 把窗口的左上角移动到一个指定的坐标
	11. open() 打开一个新的浏览器窗口或查找一个已命名的窗口 
		1. window.open(URL, name, features, replace);
		2. url 要打开页面的url  name 自己定,可以不要 features 窗口特征 宽高
		3. window.open("www.baodu.com","","width=200,height=200");
	12. print() 打印当前窗口的内容 
	13. prompt() 显示可提示用户输入的对话框
		1. window.prompt("提示输入的值","默认的文本框的内容")；
		2. 现在用的少，因为不好看，还不能改样式表
	14. resizeBy() 按照指定的像素调整窗口的大小
	15. resizeTo() 把窗口的大小调整到指定的宽度和高度 
	16. scrollBy() 按照指定的像素值来滚动内容
	17. scrollTo() 把内容滚动到指定的坐标 
	18. setInterval() 按照指定的周期（以毫秒计）来调用函数或计算表达式 
		1. 一般用来做定时器,有一个返回值ID，代表这个定时器
		2. window.setInterval("js代码",毫秒数);
		3. 1s = 1000ms
		4. 例如：window.setInterval("alert('123');", 3000);
	19. setTimeout() 在指定的毫秒数后调用函数或计算表达式
		1. 一般用来做定时器，但是只会执行一次。返回一个ID值，代表这个定时器
		2. 例如：window.setTimeout("alert('123');", 4000);

## js的dom对象
### 什么是dom
	dom：document object model：文档对象模型
	文档：超文本标记文档：html，xml
	对象：提供了属性和方法
	模型：使用属性和方法操作超文本标记型文档
	可以使用js里面的dom里面提供的对象，使用这些对象的属性和方法，对标记型文档进行操作
	想要对标记型文档进行操作，首先需要 对标记型文档里面的所有内容封装成对象，需要把HTML里面的标签，属性，文本内容都封装成对象
	要想对标记型文档进行操作，解析标记型文档

### 解析过程
	根据html的层级结构，在内存中分配一个属性结构，需要把html中的每部分封装成对象
![](https://i.imgur.com/T6dN6Cg.png)

	1. 上图中，整个蓝色框住的可以当成一个document对象，表示整个HTML文档
	2. 同时一个标签/元素也是一个对象，我们成为标签对象 element
	3. 属性对象（id属性之类的）
	4. 文本对象（标签括起来的数据）
	5. Node（节点）对象是属性，文本，标签对象的父对象
### 常用方法
	nodeName	String		节点的名字：根据节点的类型定义
	nodeValue	String		节点的值：根据节点的类型而定义
	nodeType	Number		节点的类型常量值之一
	ownerDocument	Document	指向整个节点所属的文档
	firstChild	Node		指向在childNodes列表中的第一个节点
	lastChild	Node		指向在childNodes列表中的最后一个节点
	childNodes	NodeList	所有子节点的列表
	parentNode	Node		返回一个给定节点的父亲节点
	previousSibling	Node	指向前一个兄弟节点：如果这个节点就是第一个兄弟节点，那么值为null
	nextSibling	Node		指向后一个兄弟节点
	hasChildNodes()	Boolean	当childNodes包含一个或多个节点时，返回真
	attributes	NameNodeMap	包含了代表一个元素的特性的Attr对象，仅用于Element节点
	appendChild(node)	Node	将node添加到childNodes的末尾
	removeChild(node)	Node	从childNodes中删除node
	replaceChild(newnode, node)	Node	替换
	insertBefore(newnode, refnode)	Node	在ChildNodes中的refnode之前插入newnode
### DHTML
	DHTML是很多技术的简称
	DHTML=html+css+dom+javascript
	html：封装数据
	css：使用属性和属性值设置样式
	dom：操作html文档
	JavaScript：专门指的是js的语法语句

### document对象
	每个载入浏览器的HTML文档都会成为document对象
#### 属性
	1. cookie 设置或返回与当前文档有关的所有 cookie
	2. domain 返回当前文档的域名
	3. lastModified 返回文档被最后修改的日期和时间
	4. referrer 返回载入当前文档的文档的 URL
	5. title 返回当前文档的标题
	6. URL 返回当前文档的 URL
#### 方法
	1. close() 关闭用 document.open() 方法打开的输出流，并显示选定的数据
	2. getElementById() 返回对拥有指定 id 的第一个对象的引用
	3. getElementsByName() 返回带有指定名称的对象集合
	4. getElementsByTagName() 返回带有指定标签名的对象集合
	5. open() 打开一个流，以收集来自任何 document.write() 或 document.writeln() 方法的输出
	6. write() 向文档写 HTML 表达式 或 JavaScript 代码
	7. writeln() 等同于 write() 方法，不同的是在每个表达式之后写一个换行符
### 案例：在末尾添加节点
	<ul id="ulid">
		<li>111</li>
		<li>222</li>
		<li>333</li>
		<li>444</li>
	</ul>
	<input type="button" value="add" onclick="add1();" />
	<script>
		//任务是，点击按钮，添加一行 555 在 444 后面
		function add1(){
			var ul = document.getElementById("ulid");
			var text = document.createTextNode("555");
			var li = document.createElement("li");
			li.appendChild(text);
			ul.appendChild(li);
		}
	</script>
### 元素对象-element对象
	在 HTML DOM 中，Element 对象表示 HTML 元素。
	Element 对象可以拥有类型为元素节点、文本节点、注释节点的子节点。
	NodeList 对象表示节点列表，比如 HTML 元素的子节点集合。
	要操作element对象，首先必须要获取到element，使用document里面对应的方法获取
#### 操作element对象的属性
	1. 获取属性：getAttribute(name)方法
	2. 设置属性：setAttribute(name, valure)方法
		例如：input1.setAttribute("class","haha");
		这是 input1元素的class为haha
	3. 删除属性：removeAttribute(name)方法
		不能删除value属性

#### 获得element中的element对象
	<ul id="ulid">
		<li>111</li>
		<li>222</li>
		<li>333</li>
		<li>444</li>
	</ul>
	<script type="text/javascript">
		var ull = document.getElementById("ulid");
		var lis = ull.childNodes;
		alert(lis.length);
	</script>
`上面的代码在IE中输出4， 在火狐中输出9`  

	因为火狐把 回车 空格 也算作数据了

`所以直接通过childNodes直接获得准确的子类是不现实的`

	在Element对象的范围内，可以用来查找其他节点的唯一有效方法就是getElementsByTagName()方法。
	上面的例子中，直接通过 ull.getElementsByTagName("li")获得子Element对象就行了。

### Node对象
#### 属性
	1. nodeName		节点名称
	2. nodeType		节点类型
	3. nodeValue	节点的值
##### 标签节点对应的值
	nodeType	1
	nodeName	大写的标签名称 
	nodeValue	null
##### 属性节点对应的值
	获取方法 getAttributeNode("属性名称");
	nodeType	2
	nodeName	属性名称
	nodeValue	属性的值
##### 文本节点对应的值
	获取方法 element.firstChild 或者 lastChild
	nodeType	3
	nodeName	#text
	nodeValue	文本内容
#### 例子
	使用dom解析html的时候，需要html里面的标签，属性和文本都封装成对象
	<span id="spanid">呵呵呵</span>
	<script>
		//标签节点
		var span1 = document.getElementById("spanid");
		alert(span1.nodeType);	//输出	1
		alert(Span1.nodeName);	//输出	SPAN
		alert(span1.nodeValue);	//输出	null
		
		//属性节点
		var id1 = span1.getAttributeNode("id");
		alert(id1.nodeType);	//输出	2
		alert(id1.nodeName);	//输出	id
		alert(id1.nodeValue);	//输出	spanid

		//文本节点
		var text = span1.firstChild;
		alert(text.nodeType);	//输出	3
		alert(text.nodeName);	//输出	#text
		alert(text.nodeValue);	//输出	呵呵呵
	</script>

### 父节点，子节点，同辈节点
	<ul id="ulid">
		<li>111</li>
		<li>222</li>
		<li>333</li>
		<li>444</li>
	</ul>
	ul 是 li 的父节点， li 是 ul 的子节点
	li 与 li 是 同辈节点，因为他们是同一级
#### 父节点
	parentNode
#### 子节点
	childNodes的到所有的子节点，但是兼容性查
	firstChild	第一个子节点
	lastChild	最后一个子节点
#### 同辈节点
	nextSibling		下一个子节点
	previousSibling	前一个子节点

### 操作DOM树
#### appendChild方法
	添加子节点到末尾
	特点：类似于剪切粘贴的效果
##### 例子
###### CSS内容
	#div1{
		width:200px;
		height:150px;
		border:2px solid red;
	}
	#div2{
		width:250px;
		height:150px;
		border: 5px dashed green;
	}
###### HTML内容
	<div id="div1">
		<ul id="ulidll">
			<li>123</li>
			<li>456</li>
			<li>789</li>
		</ul>
	</div>
	<div id="div2">
	</div>
	<input type="button" value="add" onclick="add1()" />
###### js内容
	function add1(){
		var div2 = document.getElementById("div2");
		var ull = document.getElementById("ulidll");
		div2.appendChild(ull);
	}
	
	通过结果可以看到，ul 的内容 从 div1 移动到 div2 中。

#### insertBefore(newnode, oldNode)方法
	在oldnode节点之前插入一个新的节点
	1. 创建标签
		li2 = document.createElement("li");
	2. 创建文本
		text = document.createTextNode("啦啦啦啦");
	3. 把文本添加到标签下
		li2.appendChild(text);
	4. 获取 oldNode
		var li3=document.getElementById("li3");
	5. 插入
		var ul = document.getElementById("ul1");//获得父节点
		ul.insertBefore(li2, li3);

#### removeChilid 删除节点
	只能通过父节点删除，不能自己删自己
	1. 获取要删除标签
		var li3 = document.getElementById("li3");
	2. 获取父节点
		var par = document.getElementById("ul");
	3. 删除
		par.removeChild(li3);
#### replaceChild(newnode, oldnode)替换节点
	只能通过父节点进行替换，不能自己替换自己
	1. 创建新节点
		var li = document.createElement("li");
		var text = document.createTextNode("文本内容");
		li.appenChild(text);
	2. 获取旧节点
		var oldli = document.getElementById("oldli");
	3. 获取父标签
		var ul = document.getElementById("ul");
	4. 替换标签
		ul.replaceChild(li, oldli);
#### cloneNode(boolean) 复制节点
	//复制ul列表到另一个div中
	1. 获取ul
		var ul = document.getElementById("ul");
	2. 复制ul，放到类似于剪切板里面
		var copyul = ul.cloneNode(true);
	3. 获取新的div
		var newdiv = document.getElementById("newdiv");
	4. 复制进去
		newdiv.appendChild(copyul);		
		因为 copyul 是复制的新的，所以appendChild的剪贴方法并不会删除掉原 ul

### innerHTML属性
	1. 浏览器几乎都支持该属性，但不是DOM标准的组成部分
	2. innerHTML属性可以用来读某给定元素里的HTML内容
		var span1 = document.getElementById("span1");
		alert(span1.innerHTML);//获取文本内容
	3. innerHTML属性可以用来写给定元素里的html内容
		var div1 = document.getElementById("div1");
		div1.innerHTML += "<h1>AAA</h1>";

### 案例：动态显示时间
	1. 获取当前时间：
		var date = new Date();
		date = date.toLocaleString();
	2. 需要让页每秒执行
		setInterval()方法
	3. 用一个<span>来承接时间
		function gettime(){
			var date = new Date();
			date = date.toLocaleString();
			var div = document.getElementsById("time");
			div.innerHtml = date; 
		}
		//使用定时器，每秒写一次
		setInterval("gettime();", 1000);

### 案例：一键全选
	<input type="checkbox" name="lova" />	排球
	<input type="checkbox" name="lova" />	篮球
	<input type="checkbox" name="lova" />	足球
	<input type="checkbox" name="lova" />	羽毛球
	<input type="button" value="全选" onclick="setall();"/>
	<input type="button" value="全不选" onclick="setNo();"/>
	<script>
		// 复选框中 的 chexked = true 即为选中，反之为没选中
		function setall(){
			//获取复选框
			var loves = document.getElementsByName("love");
			//遍历 loves 数组，整体修改值
			for(var i=0; i<loves.length; i++)
			{
				var love1 = loves[i];
				love1.checked = true;
			}
		}
	</script>
### 案例：省市联动
	选择 湖北省的时候，只会显示湖北省的市，选择湖南省的时候，只会显示湖南省的市
	<select id="sheng" onchange="add1();">
		<option>湖北省</option>
		<option>湖南省</option>
		<option>山西省</option>
		<option>江西省</option>
	</select>
	<select id="shi">
		
	</select>
	// onchange 是 当 select 改变的时候执行的操作
	<script>
		//通过数据库，可以获得每个省份，有哪些城市
		var arr = [];//arr存的读取的城市
		var select = document.getElementById("shi");
		//一定要先清空 select，否则第二次选择会进行二次添加
		var chils = select.getElementsByTagName("option");
		for(var i=child.length-1; i>=0; i--){
			var op = option[i];
			select.removeChild(op);
		}
		for(int i=0; i<arr.length; i++){
			var opt = document.createElement("option");
			var text = document.createTextNode(arr[i]);
			opt.appendChild(text);
			select.appendChild(opt);
		}
	</script>

## XML文档
### 什么是xml
	eXtensible Markup Language：可扩展标记型语言
	1. 标记型语言：html也是标记型语言，通过使用标签来操作
	2. 可扩展：html里面每个标签都是固定的，有特定的含义。xml中，标签可以自定义，也可以是中文的标签
	3. xml技术是W3C组织发部分，目前遵循的是2000发布的XML1.0规范
	
### xml的用途
	html用于显示数据，xml也可以用来显示数据，但是更主要的功能和目的是同来存储数据。
	1. 用于不同系统之间传输数据
		1. 如果数据直接用 字符串 传输，接收方并不能解析数据 
			例如："120.0.0.1;2018.10.01;hello world"发送方知道这是 "ip地址，时间，内容"，但是接收方并不知道
		2.  <message>
				<ip>120.0.0.1</ip>
				<time>2018.10.01<time>
				<content>hello world</content>
			</message>
		3. 这样写接收方能懂，并且可以扩展更多标签在<message>中
	2. 同来表示生活中有关系的数据
		例如：
		<中国>
			<湖北>
				<武汉></武汉>	
				<荆州></荆州>
			</湖北>
			<湖南>
			</湖南>
		<中国>
	3. 经常用在配置文件
		1. 用于链接数据库，例如用于存储用户密码，修改密码值用修改xml中的密码、
### xml的语法
#### xml的文档声明
	创建文件，后缀名为 .xml
#####写一个文档声明，必须写在第一行第一列
	<?xml version="1.0" encoding="utf-8"?>
###### 属性
	version：xml的版本 1.0，1.1
	encoding：xml 编码  gbk utf-8 iso8859-1
	standalone：yes/no 表示xml文件是否可以独立存在


#### 声明元素（标签）
##### 标签的定义
	1. 标签定义有开始必须有结束：<person></person>
	2. 标签没有内容，也可以标签内结束：<person />
	3. 标签可以嵌套，必须要合理嵌套
	4. 一个xml文档有且必须只有一个根标签
	5. 标签的包含的空格和换行会被解析成文本内容处理：<person>   1<person> 和 <person>1</person>是不一样的
	6. xml文档区分大小写。所以，开始标签和结束标签必须绝对相同，大小写也要完全一致
	7. 标签名可以字母（包括非西欧字符），数字，下划线，中划线，冒号，点号组成，但是不能以数字，中划线和点号开头
	8. 不能包括 ‘< > , $’
	9. 标签名尽量不要出现英文冒号“:”, 除非是在使用名空间
	10. 标签名不能以字符“xml”等任意大小写组合开始
	11. 标签名不能包含空格
#### 定义属性
	html是标记型文档，所以标签有属性。同理，xml也可以用属性
	<person id1="aa"></person>
##### 属性定义的要求
	1. 一个标签上可以有多个属性
	2. 同一个标签，不能有属性名相同的属性
	3. 属性值一定要用引号，单引号，双引号都行
	4. 属性名的命名规范和标签命名规范相同
#### 注释
	写法<!-- 注释的内容 -->
	注释不能嵌套
#### 特殊字符 && CDATA区
	开始标签和结束标签之间的文本可以是任何Unicode字符，并且其间的任何字符都重视的传递给xml处理程序
	但是如果中间由 < 或者 & 字符，容易导致辨认错误。例如： <test> 1 + 1 < 3</test>， 这样用浏览器打开就会显示错误。
	解决方法：
		1. 使用实体应用（xml定义了五种实体引用）（记得后面要加分号）：
			&lt;   	--->     "<"   小于符号
			&gt;  	--->     ">"   大于符号
			&amp;  	--->     "&"   and符号 &
			&apos;	--->     "'"     英文单引号
			&quot;	--->     """     英文双引号
		2. 使用CDATA标记
		    在特殊标记CDATA下，所有的特殊字符，甚至是有效元素都将被当成简单字符处理
		    实体引用也会失去作用，变成纯文本
		    语法：
			<![CDATA[文本内容]]>

#### PI指令（处理指令）
	可以在xml中设置样式，其实就是外部引入css
	引入css：<?xml-stylesheet type="text/css" href="1.css"?>
	但是，对中文的标签元素不起作用，毕竟外国人定义的东西



### xml的约束
	比如定义人的信息的xml，肯定不能出现猫猫狗狗的信息，所以需要约束
	由于xml的标签是自定义，所以不加约束容易出现问题。
#### dtd约束
	创建一个后缀名为 .dtd 的dtd文件
	步骤：
	1. 查看xml中有多少个元素
		例如：
			<message>
				<ip>120.0.0.1</ip>
				<time>2018.10.01<time>
				<content>hello world</content>
			</message>
		有四个元素（标签）
	2. 有多少个元素，就在dtd文件中写多少个<!ELEMENT>
	3. 判断元素是简单元素还是复杂元素
		1. 有子元素的元素是复杂元素
			<!ELEMENT 元素名称(子元素名称逗号隔开)>
			<!ELEMENT message(ip+,time？,content*)>
`其中 + ? * 是选择性加上，代表子标签在根标签下出现的次数
	1. +	代表出现一次或多次
	2. ？	代表出现0次或1次 
	3. *	打表出现0次或多次 
	默认是只出现一次`  
`逗号连接子元素名称时，子元素必须按顺序出现`  
`用 | 隔开时，表示只能出现范围中的一个`  

		2. 没有子元素的元素是简单元素
			<!ELEMENT 元素名称 (#PCDATA)>
			<!ELEMENT ip (#PCDATA)>
			<!ELEMENT time (#PCDATA)>
			<!ELEMENT content (#PCDATA)>
	4. 在xml中引入外部dtd文件，写在<xml>标签行下
		<!DOCTYPE 根元素名称 SYSTEM "dtd文件路径">
	4. 在xml内部定义dtd
		<!DOCTYPE 根元素名称[
			<!ELEMENT 子标签 (#PCDATA)>
		]>
		例如：
			<!DOCTYPE message[
				<!ELEMENT ip (#PCDATA)>
				<!ELEMENT time (#PCDATA)>
				<!ELEMENT content (#PCDATA)>
			]>
	4. 使用外部/网络的dtd文件
		<!DOCTYPE 根元素 PUBLIC "DTD名称" "DTD文档的URL">
	用浏览器打开的时候，浏览器之校验语法，不校验约束，所以用浏览器打开不能查看是否约束上

##### 使用dtd定义属性
	语法：<!ATTLIST 元素名称 属性名称 属性类型 属性的约束>
	1. 属性类型有三种
		1. CDATA：表示属性的取值为普通的文本字符串
		2. ENUMERATED：表示枚举，只能从枚举列表中任选其一 例如：（鸡肉|鸭肉|鱼肉|牛肉）这种方法定义枚举
		3. ID：表示属性的取值不能重复，只能是字母，下划线开始
	2. 属性的约束有三种
		1. #REQUIRED：表示该属性必须出现
		2. #IMPLIED：表示该属性可有可无
		3. #FIXED：表示属性的取值为一个固定值
		4. 直接写一个值上去：表示属性的默认值为你直接协商的值
	例如：<!ATTLIST ip ID1 CDATA "wwww"> 则ID1属性的值默认为www
#### schema约束
	空

### xml解析
	xml是标记型文档
	js使用dom解析标记型文档
		根据html的层级结构，在内存中分配一个属性结构，把html的标签属性和文本封装成对象
		document对象，element对象，属性对象，文本对象，node节点对象
	xml的解析方式：dom 和 sax
#### dom方式解析
	根据 xml 的层级结构在内存中分配一个树形结构，把xml的标签，属性和文本都封装成对象
		缺点：如果文件过大，造成内存溢出
		优点：方便实现增删改操作
#### sax方式解析
	采用事件驱动方式，边读便解析，从上到下，一行一行的解析，解析到某个对象，返回对象名称
		缺点：不能实现增删改
		优点：不会造成内存溢出，方便实现查询操作
![](https://i.imgur.com/bf6pKn0.png)

#### dom和sax方式的解析器
	不同的公司和组织提供了针对dom和sax方式的解析器，通过api方式提供	
	1. sun公司提供	jaxp
	2. dom4j组织提供	dom4j（实际开发中用的比较多）
	3. jdom组织提供	jdom

#### jaxp的api的查看
	jaxp是javase的一部分
	jaxp解析器在jdk的javax.xml.parsers包里面
	DocumentBuilder			定义API，使其从xml文档获取DOM文档实例
	DocumentBuilderFactory	定义工厂API，是应用程序能够从xml文档获取生成DOM对象数的解析器
	SAXParser				定义包装XMLReader实现类的API
	SAXParserFactory		定义工厂API，是应用程序能够配置和获取基于sax的解析器以解析XML文档


