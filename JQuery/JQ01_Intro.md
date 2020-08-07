【jQuery 入门】

# jQuery概述

仓库：需要去找就可以

## JS库
library，是一个封装好的特定的集合（方法和函数），预先定义好了很多函数在里面，比如动画animate, hide, show, getElement等
- 本质是JS文件
- 封装了很多原生JS代码
- 可以高效获取使用
- jQuery 就是一个JS库，作用是方便操作元素，里面基本都是函数或方法

## 常见的JS库
- jQuery
- Prototype
- YUI
- Dojo
- Ext JS
- Zepto (for mobile)
> 这些库都是对原生JS的封装，内部都是用JS实现的，我们主要学习jQuery

## jQuery
- 快速简洁的JS库
- write less, do more
- j => javascript, query => to search, 把JS中的DOM操作做了封装，可以快速的查询使用里面的功能
- jQuery 封装了JS常用的功能代码，优化了DOM操作，事件处理，动画设计和ajax交互
- 学习 jQuery 就是学习调用这些函数
- jQuery 的出现加快了前端人员的开发速度，我们可以非常方便的调用和使用它
> 原生JS好比楼梯，jQuery 好比电梯

## jQuery 优点
- 轻量级，核心文件只有几十kb
- 跨浏览器兼容，基本兼容现有主流浏览器
- 链式编程，隐式迭代
- 对事件、样式、动画支持，大大简化了DOM操作
- 支持插件扩展，由丰富的第三方插件，如：树形菜单、日期控件、轮播图等
- 免费、开源

# jQuery基本使用

## jQuery 下载

- 官网 https://jquery.com/
- 版本1x 兼容IE678，不再更新
- 版本2x 不兼容IE678，不再更新
- 版本3x 不兼容IE678，是主要维护版本

下载哪个版本？
- Production 代码压缩的比较厉害 体积小
- Devlopment 代码整齐 体积稍大

## 使用步骤
- 引入
- 直接写其他的JS代码

举例
```html
<!-- 引入jquery -->
<script src="jquery.min.js"></script> 

<style>
	div {
		width: 200px;
		height: 200px;
		background-color: pink;
	}
</style>

<div></div>

<script>
	$('div').hide(); //隐藏div元素  使用
</script>
```

## jQuery 的入口函数
- 等待DOM结构渲染完毕即可执行内部代码，不必等到所有资源加载完成，jQuery帮我们完成了封装
- 相当于原生JS的DOMContentLoaded
- 不同于原生JS中的load事件是等页面文档，外部的JS文件，CSS文件，image都加载完毕了才执行代码

方式1：传统方式
```html
<script>
	$(document).ready(function () {
		$('div').hide();
	})
</script>
```

方式2：更简单的方式（推荐）

```html
<script>
	$(function () {
		$('div').hide();
	})
</script>
```

## jQuery 的顶级对象 $
- $ 是 jQuery 的别称，实际开发中通常直接使用 $
<!-- - $ 是 jQuery 的顶级对象，相当于原生JS中的window，把元素用$包装成jQuery对象，就可以调用jQuery的方法 -->

```html
<script>
	// 以下两条入口函数等同

	$(function () { })

	jQuery(function () { })

</script>
```

## jQuery 对象和 DOM 对象
- 原生JS获取的对象就是DOM对象
- jQuery 方式获取的元素就是jQuery 对象
- jQuery 对象的本质是：利用$对DOM对象包装后产生的对象（伪数组形式储存）
- jQuery 对象只能使用jQuery方法，DOM 对象只能使用原生的JS属性和方法

```html
<div></div>
<script>
	// DOM对象
	var myDiv = document.querySelector('div');

	// myDiv.hide();  
	// 这种写法是错误的!!! DOM 对象只能使用原生的JS属性和方法

	// jQuery 对象
	$('div');

	// $('div').style.display = 'none'; 
	//这种写法是错误的!!! jQuery 对象只能使用jQuery方法
	
</script>
```

## jQuery 对象和 DOM 对象互相转换
- jquery obejct / dom object 可以互相转换
- js比jquery大, 而一些原生的属性和方法jquery没有封装，我们要使用这些属性和方法就必须把jquery object转换为dom object
- dom object => jquery object：`$(div)` 直接将已获取的DOM元素再用$包装一下
- jquery object => dom object：两种方法 `$('div')[index]` 或 `$('div').get(index)`

```html
<video src="mov.mp4" muted></video>
<!-- chrome需要加muted属性 -->

<script>
	// 直接获取为jquery object
	$('video');

	// dom object => jquery object
	var myVideo = document.querySelector('video');
	$(myVideo);  //这里不需要引号，myVideo已经是一个对象了

	// jquery object => dom object, 两种方法都可以
	$('video')[0];
	$('video').get(0);
</script>
```
