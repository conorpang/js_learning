【BOM】

- [BOM概述](#bom概述)
	- [BOM是什么](#bom是什么)
	- [DOM/BOM对比](#dombom对比)
- [window对象的常见事件](#window对象的常见事件)
	- [页面加载事件](#页面加载事件)
	- [调整窗口大小事件](#调整窗口大小事件)
- [定时器](#定时器)
	- [设置定时器 setTimeout()](#设置定时器-settimeout)
	- [案例：5秒后关闭广告](#案例5秒后关闭广告)
	- [停止定时器 clearTimeout()](#停止定时器-cleartimeout)
	- [设置 setInterval() 定时器](#设置-setinterval-定时器)
	- [案例：京东秒杀倒计时](#案例京东秒杀倒计时)
	- [停止 setInterval() 定时器](#停止-setinterval-定时器)
	- [案例：发送短信](#案例发送短信)
	- [this 的指向问题](#this-的指向问题)
- [JS执行队列](#js执行队列)
- [location对象](#location对象)
	- [location对象的属性](#location对象的属性)
	- [案例：5秒后跳转页面](#案例5秒后跳转页面)
	- [案例：获取URL的参数数据](#案例获取url的参数数据)
	- [location对象的方法](#location对象的方法)
- [naviagator对象](#naviagator对象)
- [history对象](#history对象)
	- [案例：前进后退页面](#案例前进后退页面)

# BOM概述

回顾JS的三个部分: JS / DOM / BOM

## BOM是什么

- BOM是浏览器对象模型，独立于内容于浏览器窗口进行交互的对象，核心对象是window
- BOM由一系列相关对象构成，含多种属性和方法
- BOM缺乏标准，兼容性较差，JS语法的标准化组织是ECMA，DOM的标准化组织是W3C，BOM最初是Netscape浏览器标准的一部分

## DOM/BOM对比

DOM
- 文档对象模型
- DOM 就是把文档当作对象来看
- DOM 的顶级对象是document
- DOM 主要学习的是操作页面元素
- DOM 是W3C的标准规范

BOM
- 浏览器对象模型
- 把浏览器当作对象来看
- BOM 的顶级对象是window
- BOM 学习的是浏览器窗口交互的一些对象
- BOM 是浏览器厂商在各自浏览器上定义的，兼容性较差

> BOM 比 DOM 更大，包含 DOM

window
- document
- location
- navigation
- screen
- history

window对象是浏览器的顶级对象，有双重角色
- JS 访问浏览器窗口的一个接口
- 是全局对象，定义在全局作用域中的变量，函数都会变成window对象的属性和方法

> 注意：调用时可以省略window,如 alert(), prompt()
```js
window.alert()
window.prompt()
```

```js
	window.document.querySelector();
	var num = 0; //num为全局对象,自动变成windows的属性
	console.log(window.num);

	function fn() {
		console.log(11);
	}
	fn();
	window.fn(); //fn() 为全局作用域下的函数

	console.dir(window);
	console.dir(window.name); //name本身有意义，不要随便命名变量为name
```

# window对象的常见事件

## 页面加载事件

```html
<button>点击</button>
<script>
	var btn = document.querySelector('button');
	btn.addEventListener('click', function () {
		alert('click me');
	})
	//问题来了：把JS写到button上方就无效了，如何解决？
</script>
```

- window.onload 是窗口加载事件，当文档内容完全加载完成（包括图片、脚本文件、CSS文件等）会触发该事件，然后调用处理函数
- window.onload 传统注册方式只能写一次，如果有多个，会以最后一个 window.onload 为准
- 若使用addEventListener则没有限制

```js
//窗口加载事件
// 传统方式
window.onload = function () { }
// addEventListener方式
window.addEventListener('load', function () { })

//还有一个类似的，DOMContentLoaded事件触发是，仅当DOM加载完成，不包括样式表、图片、flash等，IE9+支持
document.addEventListener('DOMContentLoaded', function () { })

//如果页面的图片很多，从用户访问到onload触发可能需要较长时间，交互效果就不能实现，必然影响用户体验，此时用DOMContentLoaded比较合适
```

```js
window.onload = function () {  //这样就可以把JS放在页面任意位置
	var btn = document.querySelector('button');
	btn.addEventListener('click', function () {
		alert('click me');
	})
}

window.onload = function () {
	alert('22');       //传统方式只能注册一次，第二次会覆盖第一次
}

window.addEventListener('load', function () {
	var btn = document.querySelector('button');
	btn.addEventListener('click', function () {
		alert('click me');
	})
})

window.addEventListener('load', function () {
	alert('22');   //addEventListener方式无限制
})

document.addEventListener('DOMCintentLoaded', function () {
	alert('33');  //DOMCintentLoaded比load加载更快，先弹33
})
```

## 调整窗口大小事件

```html
<script>
	window.onresize = function () { }
	window.addEventListener('resize', function () { })
</script>
```

window.onresize 是调整窗口大小的加载事件，当触发时就会调用处理函数
- window.innerWidth 当前屏幕宽度
- window.innerHeight 当前屏幕高度

注意
1. 只要窗口发生像素变化，就会触发该事件
2. 常利用该事件完成响应式布局

```html
<style>
	div {
		width: 200px;
		height: 200px;
		background-color: pink;
	}
</style>

<script>
	window.addEventListener('load', function () {
		var div = document.querySelector('div');
		window.addEventListener('resize', function () {
			console.log('changed');
			if (window.innerWidth <= 800) {
				div.style.display = 'none';
			} else {
				div.style.display = 'block';
			}
		})
	})
</script>
<div>123</div>
```

# 定时器

window对象提供了2种好用的方法：定时器
- setTimeout()
- setInterval()

## 设置定时器 setTimeout()

```html
<script>
	window.setTimeout(function () { }, [delayedTimeInMM]);

	// setTimeout() 用于设置一个定时器，在定时器到期后执行函数
	// window可省,延时时间为毫秒，可省，默认为0
	// 调用函数可以写函数，也可以写函数名 还可以写 'function()'
	// 多个定时器加标识符
</script>
```

```html
<script>

	// 方式1：直接写函数
	setTimeout(function () {
		console.log('Time out!');
	})


	// 方式2：函数名调用
	function callback() {
		console.log('boom!');
	}
	var time1 = setTimeout(callback, 3000); //这里调用了callback函数
	var time2 = setTimeout('callback()', 5000); //这种写法也能实现功能，但是不提倡

</script>
```

setTimeout()这个函数我们也称为*回调函数 callback*

普通函数按照代码顺序直接调用，而这个函数需要等待时间，时间到了才去调用函数，因此称为回调函数

以前所讲的

- element.onclick = function(){}
- element.addEventListener('click',function(){})

里面的函数都是回调函数


## 案例：5秒后关闭广告

- 5秒后，隐藏广告
- 用定时器，setTimeout()

```html
<img src="images/open.png" alt="">
<script>
	var ad = document.querySelector('.ad');
	setTimeout(function () {
		ad.style.display = 'none';
	}, 5000);  //5秒后隐藏
</script>
```

## 停止定时器 clearTimeout()

```html
<script>
	window.clearTimeout(timeoutID);

	// window可以省略
	// 括号里的参数是定时器的标识符
</script>

<button>stop timeout</button>
<script>
	var btn = document.querySelector('button');
	var timeout007 = setTimeout(function () {
		console.log('boom');
	}, 2000);

	btn.addEventListener('click', function () {
		clearTimeout(timeout007);
	})
</script>
```

## 设置 setInterval() 定时器

```html
<script>
	window.setInterval(回调函数, [间隔的毫秒数]);

	// 该方法重复调用一个函数，每隔这个时间，就去调用一次回调函数

	// window可以省略
	// 调用函数可以直接写函数、写函数名、字符串'函数名()'三种形式
	// 间隔的毫秒数省略默认是0，如果写必须是毫秒，表示间隔多少毫秒就自动调用这个函数
	// 建议给定时器赋值一个标识符
</script>
```

```html
<script>
	setInterval(function () {
		console.log('something');
	}, 1000);

	// setTimeout 延时时间到了，就去调用这个函数，只调用一次，然后结束该定时器
	// setInterval 每隔一段时间，就去调用这个函数，会调用很多次，重复调用这个函数
</script>
```

## 案例：京东秒杀倒计时

分析
- 倒计时是不断变化的，因此需要定时器来自动变化 setInterval
- 三个黑色盒子存放时分秒
- 三个盒子的innerHTML放入计算的时、分、秒数
- 首次执行的时候也有间隔毫秒数，因此刷新页面会有空白
- 最好采取封装函数的形式，这样可以先调用一次这个函数，防止刚开始刷新页面时有空白这一问题

```html
<div>
	<span class="hour">1</span>
	<span class="minute">2</span>
	<span class="second">3</span>
</div>

<script>
	var hour = document.querySelector('.hour');
	var minute = document.querySelector('.minute');
	var second = document.querySelector('.second');
	var inputTime = +new Date('2020-01-01 18:00:00');

	countDown(); //先调用一次，防止刷新出现空白
	setInterval(countDown, 1000);//开启定时器

	function countDown() {
		var nowTime = +new Date();
		var times = (inputTime - nowTime) / 1000;

		h = parseInt(times / 60 / 60 % 24);
		m = parseInt(times / 60 % 60);
		s = parseInt(times % 60);

		h = h < 10 ? '0' + h : h;
		m = m < 10 ? '0' + m : m;
		s = s < 10 ? '0' + s : s;

		hour.innerHTML = h;
		minute.innerHTML = m;
		second.innerHTML = s;
	}
</script>
```

## 停止 setInterval() 定时器

```html
<script>
	window.clearInterval(intervalID);

	// window可以省略
	// 里面的参数就是定时器的标识符
</script>
```

```html
<button class="begin">turn on timer</button>
<button class="stop">turn off timer</button>

<script>
	var begin = document.querySelector('.begin');
	var stop = document.querySelector('.stop');

	var timer = null; //全局变量，null为一个空对象，一定要赋一个值，否则为undefined

	begin.addEventListener('click', function () {
		timer = setInterval(function () {
			// 这里不要用var timer=... 因为只是声明了函数内的局部变量，stop的事件函数无法访问	
			//函数里没有声明的变量当全局变量使用
			console.log('hello');
		}, 1000)
	})

	stop.addEventListener('click', function () {
		clearInterval(timer);
	})

</script>
```

## 案例：发送短信

点击按钮后，该按钮60秒内不能再次点击，防止重复发送短信

[文本输入框]【按钮】

- 点击按钮后，禁用disabled为true
- 同时按钮内容发生变化，注意button里面的内容通过innerHTML修改
- 秒数发生变化，需要定时器
- 定义一个变量，在定时器里面不断递减
- 如果变量为0，说明到了时间，停止定时器，并且复原初始状态

```html
手机号码：<input type="text">
<button>发送</button>

<script>
	var btn = document.querySelector('button');
	var seconds = 3;  //定义剩下的秒数
	btn.addEventListener('click', function () {
		btn.disabled = true;
		var timer = setInterval(function () {
			if (seconds == 0) {
				// 清楚定时器、复原按钮
				clearInterval(timer);
				btn.disabled = false;
				btn.innerHTML = '发送';
				seconds = 3;  //这里一定要恢复初始值
			} else {
				btn.innerHTML = '还剩' + seconds + '秒再次点击';
				seconds--;
			}
		}, 1000)
	})
</script>
```

## this 的指向问题

this的指向在函数定义的时候无法确定，只有函数执行的时候才能确定this到底指向谁，一般情况下this的最终指向的是那个**调用它的对象**

- 全局作用域下或者普通函数中this指向的都是window，定时器里的this指向的也是window
- 方法中的this指向的是调用它的对象
- 构造函数中的this指向的是构造函数的实例

```html
<button>点击</button>
<script>

	// 全局作用域下或者普通函数中this指向的都是window，定时器里的this指向的也是window

	console.log(this); // 指向的是window
	function fn() {
		console.log(this); // 指向的是window
	}
	fn();

	setTimeout(function () {
		console.log(this); // 定时器里面的this指向的也是window 
	}, 1000)

	// 方法中的this指向的是调用它的对象

	var o = {
		sayHi: function () {
			console.log(this); //this指向的是o对象
		}
	}
	o.sayHi();

	var btn = document.querySelector('button');
	btn.onclick = function () {
		console.log(this); // this指向的是button
	}
	btn.addEventListener('click', function () {
		console.log(this); // this指向的是button
	})

	// 构造函数中的this指向的是构造函数的实例

	function Fun() {
		console.log(this);
	}
	var fun = new Fun(); // this指向的是fun实例
</script>
```

# JS执行队列

JS是**单线程语言**，同一时间只能做一件事，JS为交互而生
单线程意味着所有任务需要排队，可能造成页面渲染不连贯

```html
<script>
	console.log(1);
	setTimeout(function () {
		console.log(3);  // 单线程执行的话，该任务加载需要等待时间，会影响下一个输出任务
	}, 1000)
	console.log(2);
</script>
```

为了解决排队问题，HTML5提出web worker标准，允许JS创建多个线程，于是JS中出现了**同步**和**异步**

- 同步：前一个任务结束后再执行下一个任务，程序的执行顺序与任务的排列顺序是一致的
- 异步：做一件事情的同时，还可以处理其他事情（多线程）
> 二者的本质区别：流水线上各个流程的执行顺序不同

```html
<script>
	console.log(1);
	setTimeout(function () {  //回调函数属于异步任务
		console.log(3);
	}, 0) //延时时间为0
	console.log(2);
	// 最后结果输出的是 1，2，3
</script>
```

任务分类
- 同步任务：位于主线程执行栈
- 异步任务：位于任务队列（消息队列），回调函数属于异步任务

常见的异步任务有以下三类
- 普通事件：click, resize 等
- 资源加载：load, error 等
- 定时器：setInterval, setTimeout 等

★JS执行机制
- 先执行执行栈中的同步任务
- 异步任务放到任务队列中
- 一旦执行栈中的同步任务执行完毕，系统就会按次序读取任务队列中的异步任务，于是被读取的异步任务结束等待状态，进入执行栈，开始执行

```js
console.log(1); // 同步任务1
document.onclick = function () {
	console.log('click'); //异步任务1
}
console.log(2); // 同步任务2
setTimeout(function () {
	console.log(3); //异步任务2
}, 3000)
```

执行过程
- 当有异步任务时，执行栈提交给对应的异步进程处理
- 异步API包括（AJAX-网络模块，DOM事件-DOM模块，setTimeout，setInterval等timer模块）
- 异步任务完毕，推入任务队列中
- 任务队列包括（onload onclick事件等，setTimeout等，网络请求AJAX等）
- 主线程执行完毕，查询任务队列，取出一个任务，推入主线程处理，重复该动作
- 由于主线程不断的重复获得任务、执行任务、再获取任务、再执行，这种机制被称为**事件循环（event loop）**

# location对象

window对象提供了一个location属性用于获取或设置窗体的URL，并且可以用于解析URL，因为这个属性返回的是一个对象，所以我们将这个属性也称为location对象

URL是什么？
- 统一资源定位符：互联网上标准资源的地址
- 语法格式
- protocol://host[:port]/path/[?query]$fragment

说明
- protocol 通信协议
- host 主机/域名
- port 端口号 http默认为80
- path 路径 由0到多个 / 符号隔开的字符串，一般表示主机上的一个目录或者文件地址
- query 参数 以键值对的形式出现 通常用 & 隔开
- fragment 片段 # 常见于来链接和锚点

## location对象的属性

- **location.href** 获取或设置整个URL
- location.host 返回主机/域名
- location.port 返回端口号 如果未写 返回空字符串
- location.pathname 返回路径
- **location.search** 返回参数
- location.hash 返回片段

> 重点记忆 href 和 search

举个例子


- https://www.bilibili.com/video/BV1dV411d72A?from=search&seid=16034263370898888134#dasdasdasd 整个URL
- www.bilibili.com 域名
- /video/BV1dV411d72A 路径
- ?from=search&seid=16034263370898888134 参数
- #dasdasdasd 片段

页面跳转功能

```html
<button>点击</button>
	<script>
		var btn = document.querySelector('button');
		btn.addEventListener('click', function () {
			// console.log(location.href);  // 获得当前页面的URL
			location.href = 'http://www.baidu.com'
		})
	</script>
```

## 案例：5秒后跳转页面

```html
<div></div>
<script>
	var div = document.querySelector('div');
	var time = 5;

	jump(); // 先运行一次函数，防止出现空白页
	setInterval(jump, 1000);

	function jump() {
		if (time == 0) {
			location.href = 'http://www.baidu.com';
		} else {
			div.innerHTML = '你将在' + time + '秒钟后跳转到首页';
			time--;
		}
	}
</script>
```
## 案例：获取URL的参数数据

- 登录页面，包含提交表单，action提交到 index.html 页面
- index页面，，可以使用第一个页面的参数，可以实现数据在不同页面的传递效果
- index页面之所以可以使用第一个页面的数据，是利用了URL里面的location.search参数
- index页面拿到参数后还需要提取参数
- 第一步去掉? 用substr
- 第二步利用等号(=)分割键值对 split('=')

最后写好的代码如下：


login.html
```html
<form action="index.html">
		<!-- 默认是用的get提交 -->
		用户名：<input type="text" name="uname">
		<input type="submit" value="login">
</form>
```

index.html
```html
<div></div>
<script>
	var para = location.search.substr(1); //去掉问号
	var uname_arr = para.split('='); //获取键值对
	var uname = uname_arr[1]; //获取值，即uname

	var div = document.querySelector('div');
	div.innerHTML = '你好，' + uname;
</script>
```


## location对象的方法

- location.assign() 跟hrer一样,可以跳转页面,也称为重定向页面
- location.replace() 替换当前页面,因为不记录历史,所以不能后推页面
- location.reload() 重新加载页面,相当于刷新按钮或者F5, 如果参数为true,强制刷新ctrl+F5

```html
	<button class="button1">click1</button>
	<button class="button2">click2</button>
	<button class="button3">click3</button>
	<script>
		var btn1 = document.querySelector('.button1');
		btn1.addEventListener('click', function () {
			location.assign('http://www.douban.com');  //跳转页面
			//有记录页面历史,因此可以实现后退功能
		})

		var btn2 = document.querySelector('.button2');
		btn2.addEventListener('click', function () {
			location.replace('http://www.douban.com');  //跳转页面
			//无记录页面历史,无法后退
		})

		var btn3 = document.querySelector('.button3');
		btn3.addEventListener('click', function () {
			location.reload();
			//括号参数为true, 强制刷新当前页面
		})
	</script>
```

# naviagator对象

navigator对象包含有关浏览器的信息, 它有很多属性,最常用的是 userAgent, 该属性可以返回由客户机发送服务器的user-agent头部的值

可以通过navigator.userAgent属性作为判断条件,给电脑端和移动端跳转不同页面

# history对象

history对象用于与历史记录交互,该对象包含用户(在浏览器窗口中)访问过的URL

history对象一般在实际开发中比较少用,但是会在一些OA办公系统中见到


history方法
- back() 后退功能
- forward() 前进功能
- go(para) 前进/后退均可, 参数为1 前进1个页面, 参数为-1 后退一个页面

## 案例：前进后退页面

index.html

```html
	<p>这是index页面</p>
	<a href="list.html">go to list page</a>
	<button>back</button>

	<script>
		var btn = document.querySelector('button');
		btn.addEventListener('click', function () {
			// history.back();
			history.go(-1);
		})
	</script>
```

list.html
```html
<p>这是list页面</p>
	<a href="index.html">go to index page</a>
	<button>forward</button>

	<script>
		var btn = document.querySelector('button');
		btn.addEventListener('click', function () {
			history.forward();
		})
	</script>
```
