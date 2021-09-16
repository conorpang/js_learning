# DOM
- [DOM](#dom)
- [DOM简介](#dom%E7%AE%80%E4%BB%8B)
- [获取元素](#%E8%8E%B7%E5%8F%96%E5%85%83%E7%B4%A0)
	- [ID获取元素](#id%E8%8E%B7%E5%8F%96%E5%85%83%E7%B4%A0)
	- [Tag获取元素](#tag%E8%8E%B7%E5%8F%96%E5%85%83%E7%B4%A0)
	- [H5新增方法获取元素](#h5%E6%96%B0%E5%A2%9E%E6%96%B9%E6%B3%95%E8%8E%B7%E5%8F%96%E5%85%83%E7%B4%A0)
	- [获取特殊元素（body和html）](#%E8%8E%B7%E5%8F%96%E7%89%B9%E6%AE%8A%E5%85%83%E7%B4%A0body%E5%92%8Chtml)

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