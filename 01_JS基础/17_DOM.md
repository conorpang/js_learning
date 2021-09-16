# DOM

- [DOM](#dom)
- [DOM简介](#dom简介)
- [获取元素](#获取元素)
	- [ID获取元素](#id获取元素)
	- [Tag获取元素](#tag获取元素)
	- [H5新增方法获取元素](#h5新增方法获取元素)
	- [获取特殊元素（body和html）](#获取特殊元素body和html)
- [事件基础](#事件基础)
	- [事件三要素](#事件三要素)
	- [执行事件的步骤](#执行事件的步骤)
- [操作元素](#操作元素)
	- [改变元素内容](#改变元素内容)
	- [innerText和innerHTML的区别](#innertext和innerhtml的区别)
	- [修改元素属性](#修改元素属性)
	- [案例：分时显示不同图片，不同问候语](#案例分时显示不同图片不同问候语)
	- [修改表单属性](#修改表单属性)
	- [案例：模仿京东登陆页面显示明文密码](#案例模仿京东登陆页面显示明文密码)
	- [修改元素的样式属性](#修改元素的样式属性)
	- [案例：淘宝点击关闭二维码](#案例淘宝点击关闭二维码)
	- [案例：循环精灵图背景](#案例循环精灵图背景)
	- [案例：显示隐藏文本框](#案例显示隐藏文本框)
	- [使用ClassName修改样式属性](#使用classname修改样式属性)
	- [案例：密码框格式提示错误信息](#案例密码框格式提示错误信息)
	- [操作元素总结](#操作元素总结)
	- [排他思想（算法）](#排他思想算法)
	- [案例：百度换肤效果](#案例百度换肤效果)
	- [案例：表格悬浮经过变色](#案例表格悬浮经过变色)
	- [案例：表单全选取消](#案例表单全选取消)
	- [自定义属性的操作](#自定义属性的操作)
	- [案例：tab栏切换（重点★）](#案例tab栏切换重点)
	- [H5自定义属性](#h5自定义属性)
- [节点操作](#节点操作)
	- [获取元素方式](#获取元素方式)
	- [节点概述](#节点概述)
	- [节点层级](#节点层级)
	- [获取first/last子元素](#获取firstlast子元素)
	- [案例：新浪下拉菜单](#案例新浪下拉菜单)
	- [节点操作：兄弟节点](#节点操作兄弟节点)
	- [节点操作：创建/添加节点](#节点操作创建添加节点)
		- [创建节点](#创建节点)
		- [添加节点](#添加节点)
	- [案例：简单版发布留言](#案例简单版发布留言)
	- [节点操作：删除节点](#节点操作删除节点)
	- [案例：删除留言案例](#案例删除留言案例)
	- [节点操作：复制节点](#节点操作复制节点)
	- [案例：动态生成表格](#案例动态生成表格)
	- [三种动态创建元素的区别](#三种动态创建元素的区别)
	- [DOM重点核心](#dom重点核心)

# DOM简介

文档对象模型 Document Object Model
- 是W3C组织推荐的处理可扩展标记语言（HTML/XML）的标准编程接口
- 提供了一系列的DOM接口，可改变网页的内容、结构和样式

DOM树
- 文档 > 根元素 > 元素 > ... > 元素 > 属性
- 文档 document 一个页面就是一个文档
- 元素 element 页面中所有标签都是元素
- 节点 node 网页中的所有内容（标签、属性、文本、注释等）都是节点
> DOM把以上内容都看作**对象**


# 获取元素

DOM在实际开发中主要用来操作元素，获取页面元素的方法：
- ID获取
- TAG获取
- H5新增方法获取
- 特殊元素获取

## ID获取元素

getElementById(ID) 可以获取带有ID的元素对象

```html
<div id="time">2019-9-9</div>
<script>
	// 因为文档页面从上往下加载，所以先有标签，再有JS
	// getElementById() 注意是驼峰命名法
	// 参数 id 是字符串，大小写敏感
	// 返回的是一个元素对象

	var time = document.getElementById('time');
	console.log(time); //<div id="time">2019-9-9</div>
	console.log(typeof time); //object

	// console.dir 打印返回的元素对象,更好的查看里面的属性和方法
	console.dir(time);

	// 输出结果为:
	// div#time
	// accessKey: ""
	// align: ""
	// ariaAtomic: null
	// ariaAutoComplete: null
	// ariaBusy: null
	// ariaChecked: null
	// ariaColCount: null
	// ariaColIndex: null
	// ariaColSpan: null
	// ariaCurrent: null
	// ariaDescription: null
	// ariaDisabled: null
	// ariaExpanded: null
	// ariaHasPopup: null
	// ...反正很长很多
</script>
```

## Tag获取元素

getElementsByTagName() 返回带有指定标签名的对象集合

注意:
1. 因为得到的是一个对象的集合,所以想要操作就要遍历
2. 得到的元素对象是动态的

```html
<ul>
	<li>text</li>
	<li>text</li>
	<li>text</li>
	<li>text</li>
	<li>text</li>
</ul>

<script>

	// 返回的是：获取过来的元素对象的集合,以伪数组的形式存储
	var lis = document.getElementsByTagName('li');
	console.log(lis);

	// HTMLCollection(5)
	// 0: li
	// 1: li
	// 2: li
	// 3: li
	// 4: li
	// length: 5
	// __proto__: HTMLCollection

	console.log(lis[0]); //<li>text</li>

	// 想要依次打印里面的元素可以采取遍历的方式
	for (var i = 0; i < lis.length; i++) {
		console.log(lis[i]);
	}

	// 如果页面中只有一个li,返回的还是伪数组
	// 如果页面中没有这个元素,返回的是空的伪数组

</script>
```

还可以获取某个元素(父元素)内部的所有指定标签名的子元素

element.getElementsByTagName('tagName')

父元素必须是指定的单个对象,获取的时候不包括父元素自己

```html
<ul>
	<li>text</li>
	<li>text</li>
	<li>text</li>
	<li>text</li>
	<li>text</li>
</ul>
<ol id="ol">
	<li>another</li>
	<li>another</li>
	<li>another</li>
	<li>another</li>
	<li>another</li>
</ol>

<script>
	var ol = document.getElementsByTagName('ol');
	console.log(ol[0].getElementsByTagName('li'));
	//父元素必须是指定的单个对象
	//这里用的是ol[0],而不是[ol]


	//换一种思路，用ID获取ol，用TAG获取li
	var ol = document.getElementById('ol');
	console.log(ol.getElementsByTagName('li'));

</script>
```


## H5新增方法获取元素

document.getElementsByClassName('class')
// 根据类名返回元素对象集合

document.querySelector('selector')
// 根据指定选择器返回第一个元素对象

document.querySelectorAll('selector')
// 根据指定选择器返回所有元素


```html
<div class="box">盒子</div>
<div class="box">盒子</div>
<div id="nav">
	<ul>
		<li>首页</li>
		<li>产品</li>
	</ul>
</div>

<script>
	// 根据类名获取某些元素集合
	var boxes = document.getElementsByClassName('box');
	console.log(boxes);

	// HTMLCollection(2)
	// 0: div.box
	// 1: div.box
	// length: 2
	// __proto__: HTMLCollection

	// querySelector() 返回指定选择器的第一个元素对象，切记里面的选择器需要添加符号 .box #nav

	var firstBox = document.querySelector('.box');
	console.log(firstBox); //<div class="box">盒子</div>

	var nav = document.querySelector('#nav');
	console.log(nav);

	var li = document.querySelector('li');
	console.log(li);


	// querySelectorAll() 返回指定选择器的所有元素对象集合

	var allBox = document.querySelectorAll('.box');
	console.log(allBox);

</script>
```

## 获取特殊元素（body和html）

```html
<!DOCTYPE html>
<html lang="en">

<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Document</title>
</head>

<body>
	<script>
		// 获取body元素
		var bodyEle = document.body;
		console.log(bodyEle);
		console.dir(bodyEle);

		// 获取html元素
		var htmlEle = document.html;
		console.log(htmlEle);  //undefined

		var htmlEle = document.documentElement;   //正确写法
		console.log(htmlEle);

	</script>
</body>
</html>
```