---
title: BootStrap框架
date: 2017-10-22 19:14:38
tags:
---
## 什么是BootStrap
- bootstrap 是当下非常经典且流行的前端框架（界面工具集）很多公司的前后端项目都有继承bootstrap
- bootstrap的特点：灵活借简洁，代码优雅，美观大方，直观强悍的前端开发框架
- GitHub：https://github.com/twbs/boostrap
- 官网：
	- http://www.bootcss/com/
	- http://getbootstrap.com/

## 使用Bootstrap
- npminstall bootstrap --save  
	(通过npm进行安装，适合工程化开发，比如集成到react或者Node项目中)

- gitHub直接下载  
	(适合起步，全面学习)


### Bootstrap初始化模板
```html
<!DOCTYPE html>
<html lang="zh-CN">
	<head>
		<meta charset="utf-8">
		<meta http-equiv="X-UA-Compatible" content="IE=edge">
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
		<title>test1</title>

		<link rel="stylesheet" href="utlise/bootstrap-3.3.7-dist/css/bootstrap.min.css">
		<link href="css/index.css" rel="stylesheet">
		<!-- <script src="https://cdn.staticfile.org/jquery/2.1.1/jquery.min.js"></script> -->
		<script src="utlise/jquery-3.3.1.js" ></script>
		<script src="utlise/bootstrap-3.3.7-dist/js/bootstrap.min.js"></script>
	</head>
	<body>
		<h1>你好，世界！</h1>

		<!-- jQuery (Bootstrap 的所有 JavaScript 插件都依赖 jQuery，所以必须放在前边) -->
		<script src="https://cdn.jsdelivr.net/npm/jquery@1.12.4/dist/jquery.min.js"></script>
		<!-- 加载 Bootstrap 的所有 JavaScript 插件。你也可以根据需要只加载单个插件。 -->
		<script src="https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/js/bootstrap.min.js"></script>
	</body>
</html>
```

![](https://i.imgur.com/2Z1W4tR.png)

	自己的定义的css和js一定要在bootstrap定义的css和js之后，以免bootstrap定义的东西覆盖了我们定义的


## 使用Boosstrap
	在官网中查看信息即可
- https://v3.bootcss.com/components/#glyphicons
- https://v3.bootcss.com/css/#overview

### 例如

#### 字体图标

```html
<span class="glyphicon glyphicon-envelope" style="font-size:40px"></span>
```
这样的一个文字信息图标就出来了

#### 进图条

```html
<div class="progress">
	<div class="progress-bar" role="progressbar" aria-valuenow="60" aria-valuemin="0" aria-valuemax="100" style="width: 60%;">
		60%
	</div>
</div>
```

#### 面板 panel

```html
<div class="panel panel-default panel-success">
		<!-- 面板类似于一个栏目框，heading为标题，panel-success 只可以改变标题颜色  -->
		<div class="panel-heading">面板标题</div>
		<div class="panel-body">面板内容</div>
		<div class="panel-footer">面板脚注</div>
</div>
```

#### 模态框

```html
	<!-- Button trigger modal -->
<button type="button" class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal">
  Launch demo modal
</button>

<!-- Modal -->
<div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel">
	<div class="modal-dialog" role="document">
		<div class="modal-content">
			<div class="modal-header">
				<button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
				<h4 class="modal-title" id="myModalLabel">Modal title</h4>
			</div>
			<div class="modal-body">
				...
			</div>
			<div class="modal-footer">
				<button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
				<button type="button" class="btn btn-primary">Save changes</button>
			</div>
		</div>
	</div>
</div>
```

#### 轮播图Carousel

```html
<div id="carousel-example-generic" class="carousel slide" data-ride="carousel">
	<!-- Indicators -->
	<ol class="carousel-indicators">
		<li data-target="#carousel-example-generic" data-slide-to="0" class="active"></li>
		<li data-target="#carousel-example-generic" data-slide-to="1"></li>
		<li data-target="#carousel-example-generic" data-slide-to="2"></li>
	</ol>

	<!-- Wrapper for slides -->
	<div class="carousel-inner" role="listbox">
		<div class="item active">
			<img src="..." alt="...">
			<div class="carousel-caption">
				...
			</div>
		</div>
		<div class="item">
			<img src="..." alt="...">
			<div class="carousel-caption">
				...
			</div>
		</div>
		...
	</div>

	<!-- Controls -->
	<a class="left carousel-control" href="#carousel-example-generic" role="button" data-slide="prev">
		<span class="glyphicon glyphicon-chevron-left" aria-hidden="true"></span>
		<span class="sr-only">Previous</span>
	</a>
	<a class="right carousel-control" href="#carousel-example-generic" role="button" data-slide="next">
		<span class="glyphicon glyphicon-chevron-right" aria-hidden="true"></span>
		<span class="sr-only">Next</span>
	</a>
</div>
```

#### 其他的自行学习

## 综合案例

### 响应式页面
	因为页面不仅要跑到pc端，还要跑到手机端，所以页面要做成响应式的页面

`开启视口模式`

```html
	<meta name="viewport" content="width=decice-witdth, initial-scalse=1.0"> 
```

![](https://i.imgur.com/hkXJ8WL.png)

![](https://i.imgur.com/usYXan5.png)

#### 自己写自适应

##### css

```css

@media screen and (max-width: 768px){
	.contariner{
		width: 100%;
	}
}

@media screen and (min-width: 760) and (max-width: 992px){
	.contariner{
		width: 750px;
	}
}

@media screen and (max-width: 992) and (max-width: 1200px){
	.contariner{
		width: 970px;
	}
}

@media screen and (min-width: 1200){
	.contariner{
		width: 1170px;
	}
}

```

	这些参数值都是根据上面的 栅格参数 制定的
##### js

```javascript
window.addEventListener("load", functino(){
	//获取常量 类 和 屏幕宽高
	let contariner = document.querySelector(".container");
	let clientw = 0;	
	// 监听窗口的大小变化
	window.addEventListener("resize", function(){
		clientw = window.innerWidth;
		
		if(clientw >= 1200) {//超大屏幕
			container.styler.width = "1170px";
		} else if(client >= 992) {//大屏幕
			container.styler.width = "970px";
		} else if(client >= 760) { //小屏幕
			container.styler.width = "750px";
		} else {
			container.styler.width = "100%";
		}
	})
});
```

### 设计页面
	
	栅格布局，bootstrap 把一行分成12列，可以通过自由组合，去组成12列
![](https://i.imgur.com/pDedAyZ.png)

	bootstrap 也帮你定义好了这 12 种去实现
![](https://i.imgur.com/1BV65wQ.png)

	如果想要某些模块在小屏幕不显示 可用：
![](https://i.imgur.com/iy5kQej.png)

### 文字样式

![](https://i.imgur.com/DvEDqx3.png)

![](https://i.imgur.com/hKhXyao.png)

	之后选择下载，解压，导入到工程种

![](https://i.imgur.com/yRrzEuu.png)

	其中 icon-wifi 的 content 的值 来自于 网页demo中
	注意 content 中 " \ "的方向，切忌写反
	然后就可以直接在 <span class="icon-wifi"></span>中使用即可