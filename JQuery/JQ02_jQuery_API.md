【jQuery常用API】

- [jquery 选择器](#jquery-选择器)
	- [基础选择器](#基础选择器)
	- [层级选择器](#层级选择器)
	- [隐式迭代](#隐式迭代)
	- [jquery 筛选选择器](#jquery-筛选选择器)
	- [jquery 筛选方法](#jquery-筛选方法)
	- [案例：新浪下拉菜单](#案例新浪下拉菜单)
	- [jquery中的排他思想](#jquery中的排他思想)
	- [案例：淘宝服饰精品](#案例淘宝服饰精品)
- [jquery 样式操作](#jquery-样式操作)
	- [案例：tab栏切换](#案例tab栏切换)
	- [类操作与className的区别](#类操作与classname的区别)
- [jquery 效果](#jquery-效果)
	- [显示隐藏效果](#显示隐藏效果)
	- [滑动效果](#滑动效果)
	- [事件切换](#事件切换)
	- [动画队列及其停止排队方法](#动画队列及其停止排队方法)
	- [淡入淡出效果](#淡入淡出效果)
	- [案例: 高亮显示案例](#案例-高亮显示案例)
	- [自定义动画 animate](#自定义动画-animate)
	- [案例:王者荣耀手风琴效果(折叠卡片)](#案例王者荣耀手风琴效果折叠卡片)
- [jquery 属性操作](#jquery-属性操作)
	- [案例:购物车模块-全选](#案例购物车模块-全选)
- [jquery 文本属性值](#jquery-文本属性值)
	- [案例: 购物车增减商品数量](#案例-购物车增减商品数量)
	- [案例: 购物车修改商品小计](#案例-购物车修改商品小计)
- [jquery 元素操作](#jquery-元素操作)
	- [遍历元素](#遍历元素)
	- [创建元素](#创建元素)
	- [添加元素](#添加元素)
	- [删除元素](#删除元素)
	- [案例: 购物车删除商品模块](#案例-购物车删除商品模块)
	- [案例：购物车案例-选中商品添加背景](#案例购物车案例-选中商品添加背景)
- [jquery 尺寸、位置操作](#jquery-尺寸位置操作)

# jquery 选择器

## 基础选择器

jquery 做了统一封装 `$('selector')` 选择器直接写css选择器即可，要加引号

- id selector: `$('#id')`
- all selector: `$('*')`
- class selector: `$('.class')`
- tag selector: `$('div')`
- union selector 并集选择器: `$(div,p,li')`
- intersection selector 交集选择器: `$('li.current')`

## 层级选择器

- 子代选择器: `$('ul>li')` 只获取亲儿子，不获取孙子
- 后代选择器: `$('ul li')` 获取所有后代


```html
<script src="jquery.min.js"></script>

<div></div>
<div class="nav"></div>
<p></p>
<ol>
	<li></li>
	<li></li>
	<li></li>
	<li></li>
</ol>
<ul>
	<li></li>
	<li></li>
	<li></li>
	<li></li>
</ul>

<script>
	$(function () {
		// 类选择器 举例
		console.log($('.nav'));
		// S.fn.init(1)
		// 0: div.nav
		// length: 1
		// prevObject: S.fn.init [document]
		// __proto__: Object(0)


		// 后代选择器 举例
		console.log($('ul li'));
		// S.fn.init(4)[li, li, li, li, prevObject: S.fn.init(1)]
		// 0: li
		// 1: li
		// 2: li
		// 3: li
		// length: 4
		// prevObject: S.fn.init[document]
		// __proto__: Object(0)
	})
</script>
```

## 隐式迭代

jquery设置样式 `$('div').css('attribute','value')`

隐式迭代
- 遍历内部DOM元素（伪数组形式存储）的过程叫做隐式迭代
- 简单理解：给匹配到的所有元素进行循环遍历，执行相应的方法，而不用再进行循环，简化了操作

```html
<script src="jquery.min.js"></script>

	<div>意不意外？</div>
	<div>意不意外？</div>
	<div>意不意外？</div>
	<div>意不意外？</div>

	<ul>
		<li>相同的操作</li>
		<li>相同的操作</li>
		<li>相同的操作</li>
	</ul>

	<script>
		// 获取四个div元素
		// 给四个div元素设置背景色为pink
		$('div').css('background', 'pink');  //隐式迭代，而无需遍历循环
		$('ul li').css('color', 'red');

	</script>
```

## jquery 筛选选择器

- `:first` 举例：`$('li:first')` 获取第一个li元素
- `:last` 举例：`$('li:last')` 获取最后一个li元素
- `:eq(index)` 举例：`$('li:eq(2)')` 获取到的li元素中，选择索引号为2的
- `:odd` 举例：`$('li:odd')` 获取到的li元素中，选择为奇数
- `:even` 举例：`$('li:even')` 获取到的li元素中，选择为偶数的

```html
<script src="jquery.min.js"></script>
<ul>
	<li>多个里面筛选</li>
	<li>多个里面筛选</li>
	<li>多个里面筛选</li>
	<li>多个里面筛选</li>
	<li>多个里面筛选</li>
</ul>
<ol>
	<li>多个里面筛选</li>
	<li>多个里面筛选</li>
	<li>多个里面筛选</li>
	<li>多个里面筛选</li>
	<li>多个里面筛选</li>
</ol>
<script>
	$(function () {
		$('ul li:first').css('color', 'red');
		$('ul li:last').css('color', 'green');
		$('ul li:eq(2)').css('color', 'blue');
		$('ol li:odd').css('color', 'orange');
	})
</script>
```
## jquery 筛选方法

> 重点记 `parent()`，`children(selector)`，`find(selector)`，`siblings(selector)`，`eq(index)`

- `parent()` 用法: `$('li').parent()` 说明:查找父级
- `children(selector)` 用法: `$('ul').('li')` 说明:查找最近一级的子元素(亲儿子),相当于 `$('ul>li')`
- `find(selector)` 用法: `$(ul).find('li')` 说明:后代选择器,相当于`$('ul li')`
- `siblings(selector)` 用法: `$('.first').siblings(li)` 说明: 查找兄弟接节点,不包括本身
- `nextAll([expr])` 用法: `$('.first').nextAll()` 说明: 查找当前元素之后所有的同辈元素
- `prevAll([expr])` 用法: `$('.last').prevAll()` 说明: 查找当前元素之前所有的同辈元素
- `hasClass(class)` 用法: `$('div').hasClass(protected)` 说明: 检查当前元素是否含有某个特定的类,如果有,返回true
- `eq(index)` 用法: `$('li').eq(2)` 说明: 相当于 `$('li:eq(2)')` index从0开始

> 使用`parent()`，`children(selector)`，`siblings(selector)`

```html
<script src="jquery.min.js"></script>
<div class="yeye">
	<div class="father">
		<div class="son">儿子</div>
	</div>
</div>
<div class="nav">
	<p>pppppppppppp</p>
	<div>
		<p>pppppppppppp</p>
	</div>
</div>
<script>
	$(function () {
		// 父 
		// parent() 返回的是最近一级的父元素
		console.log($('.son').parent();
		// 子 
		// children() 返回的是最近一级的子元素
		$('.nav').children('p').css('color', 'purple');
		// find()  返回的是所有子代元素
		$('.nav').find('div p').css('color', 'green');
		// 兄
		console.log($('.nav p').siblings('div');
	})
</script>
```



> 使用`siblings()`，`prevAll()`，`nextAll()`，`hasClass()`，`eq(index)`

```html
<script src="jquery.min.js"></script>
<style>
	.test {
		font-weight: ;
	}
</style>
<ol>
	<li>我是ol的li</li>
	<li>我是ol的li</li>
	<li class="item">我是ol的li</li>
	<li>我是ol的li</li>
	<li>我是ol的li</li>
</ol>
<ul>
	<li>我是ul的li</li>
	<li>我是ul的li</li>
	<li class="test">我是ul的li</li>
	<li>我是ul的li</li>
	<li>我是ul的li</li>
</ul>
<div class="current">I have current</div>
<div>I don't have current</div>
<script>
	$(function () {
		// siblings 选取的除了自身以外的所有亲兄弟
		$('ol .item').siblings('li').css('color', 'red');
		// prevAll nextAll 当前元素之前/之后的同辈元素
		$('ul .test').prevAll('li').css('color', 'green');
		$('ul .test').nextAll('li').css('color', 'orange');
		// eq(index) 更推荐用方法写
		$('ul li').eq(2).css('color', 'blue');
		// 等同于如下
		$('ul li:eq(2)').css('color', 'blue');
		// 判断是否有某个类名
		$('div:first').hasClass('current');  //true
		$('div:last').hasClass('current');  //false
	})
</script>
```


## 案例：新浪下拉菜单

- 四个菜单项
- 每个菜单项，鼠标悬浮会出现另外三个菜单项
- 鼠标经过事件、鼠标离开事件

```html
<script src="jquery.min.js"></script>
<style>
	.nav>li>ul {
		display: none;
	}
</style>
<ul class="nav">
	<li>
		<a href="">weibo</a>
		<ul>
			<li>
				<a href="">私信</a>
			</li>
			<li>
				<a href="">评论</a>
			</li>
			<li>
				<a href="">@我</a>
			</li>
		</ul>
	</li>
	<li>
		<a href="">weibo</a>
		<ul>
			<li>
				<a href="">私信</a>
			</li>
			<li>
				<a href="">评论</a>
			</li>
			<li>
				<a href="">@我</a>
			</li>
		</ul>
	</li>
	<li>
		<a href="">weibo</a>
		<ul>
			<li>
				<a href="">私信</a>
			</li>
			<li>
				<a href="">评论</a>
			</li>
			<li>
				<a href="">@我</a>
			</li>
		</ul>
	</li>
	<li>
		<a href="">weibo</a>
		<ul>
			<li>
				<a href="">私信</a>
			</li>
			<li>
				<a href="">评论</a>
			</li>
			<li>
				<a href="">@我</a>
			</li>
		</ul>
	</li>
</ul>
<script>
	$(function () {
		// 鼠标经过
		$('.nav>li').mouseover(function () {
			// $(this) jQuery 中的当前元素 无需引号
			// show() 显示元素 hide() 隐藏元素
			// $(this).children('ul').show();
			$(this).children('ul').slideDown(200);
		})
		// 鼠标移开
		$('.nav>li').mouseout(function () {
			// $(this).children('ul').hide();
			$(this).children('ul').slideUp(200);
		})
	})
</script>
```
## jquery中的排他思想

> 排他思想：当前元素设置样式，其余的兄弟元素清除样式

```html
<script src="jquery.min.js"></script>
<button>快速</button>
<button>快速</button>
<button>快速</button>
<button>快速</button>
<button>快速</button>
<button>快速</button>
<button>快速</button>
<script>
	$(function () {
		// 隐式迭代 所有的按钮都绑定了点击事件
		$('button').click(function () {
			//其余的兄弟去掉背景颜色 隐式迭代
			$(this).siblings('button').css('background', '');
			// 当前的元素变化背景颜色
			$(this).css('background', 'pink');
		})
	})
</script>
```
## 案例：淘宝服饰精品

- 左侧有9个标签（li），鼠标移动到任意标签上，右侧的内容区盒子显示对应图片，其余的图片隐藏
- 需要得到当前小li的索引号，就可以显示对应索引号的图片
- jQuery得到当前元素索引号`$(this).index()`
- 通过`eq(index)`方法选择对应的图片
- 显示隐藏元素 `show()` `hide()`


```html
<script src="jquery.min.js"></script>

	<style>
		#content div {
			display: none;
		}
	</style>
	<div class="wrapper">
		<ul id="left">
			<li><a href="">女靴</a></li>
			<li><a href="">雪地靴</a></li>
			<li><a href="">冬裙</a></li>
			<li><a href="">呢大衣</a></li>
			<li><a href="">毛衣</a></li>
			<li><a href="">棉服</a></li>
			<li><a href="">女裤</a></li>
			<li><a href="">羽绒服</a></li>
			<li><a href="">牛仔裤</a></li>
		</ul>
	</div>

	<div id="content">
		<div style="display:block"><a href="#"><img src="images/01.jpg" width="200" height="120"></a></div>
		<div><a href="#"><img src="images/02.jpg" width="200" height="120"></a></div>
		<div><a href="#"><img src="images/03.jpg" width="200" height="120"></a></div>
		<div><a href="#"><img src="images/04.jpg" width="200" height="120"></a></div>
		<div><a href="#"><img src="images/05.jpg" width="200" height="120"></a></div>
		<div><a href="#"><img src="images/06.jpg" width="200" height="120"></a></div>
		<div><a href="#"><img src="images/07.jpg" width="200" height="120"></a></div>
		<div><a href="#"><img src="images/08.jpg" width="200" height="120"></a></div>
		<div><a href="#"><img src="images/09.jpg" width="200" height="120"></a></div>
	</div>

	<script>
		$(function () {
			// 鼠标经过事件
			$('#left li').mouseover(function () {

				// 获取当前经过的小li索引号
				var index = $(this).index();

				// 让右侧对应图片显示出来
				$('#content div').eq(index).show();

				// 隐藏其余图片
				$('#content div').eq(index).siblings('div').hide();

			})
		})
	</script>
```

# jquery 样式操作

简单样式修改css，复杂样式操作类

简答样式修改
- 参数只写属性名，则是返回属性值 `$(this).css('color');`
- 参数写了属性名和属性值，逗号分隔，可以修改对应属性的属性值 `$(this).css('color','red');` 注意属性名必须加引号，值为数字可以不带单位和引号
- 参数修改可以是对象形式，方便设置多组样式，属性名和属性值用冒号隔开，属性可以不加引号 `$(this).css({'color':'white','font-size':'20px'})`

```html
	<script src="jquery.min.js"></script>

	<style>
		div {
			width: 200px;
			height: 200px;
			background-color: pink;
		}
	</style>
	<div>
		托尔斯泰
	</div>
	<script>
		$(function () {
			console.log($('div').css('width')); // 200px
			$('div').css('width', '300px');  //宽度发生变化
			$('div').css({
				'color': 'blue',
				'font-size': '20px',
				height: 500,
				weight: 500,
				backgroundColor: 'red' //复合属性必须采用驼峰命名法
			})  //以对象形式修改css, 属性可以不加引号不是数字则需要加引号
		})
	</script>
```


复杂样式修改类
- 作用等同于`classList` 可以操作样式，注意操作类里面的参数不需要加点
- 添加类 `$('div').addClass('current')` 注意类名无需加点
- 删除类 `$('div').removeClass('current')` 
- 切换类 `$('div').toggleClass('current')`

```html
<script src="jquery.min.js"></script>

	<style>
		div {
			width: 200px;
			height: 200px;
			background-color: pink;
			margin: 100px auto;
			transition: all 0.5s;
		}

		.current {
			background-color: red;
			transform: rotate(360deg);
		}
	</style>
	<div class='div1'></div>
	<div class="current">haha</div>
	<div class="div3"></div>


	<script>
		$(function () {
			// 添加类
			$('.div1').click(function () {
				$(this).addClass('current');
			})

			// 删除类
			$('.current').click(function () {
				$(this).removeClass('current');
			})

			// 切换类
			$('.div3').click(function () {
				$(this).toggleClass('current');
			})
		})
	</script>
```

## 案例：tab栏切换
- 点击上部li,当前li添加current类,其余兄弟移除类
- 点击的同时,得到当前li的索引号
- 让下部里面相应索引号的item显示,其余的item隐藏


```html
	<style>
		li {
			height: 30px;
			width: 80px;
			background-color: lightgrey;
			color: black;
			display: inline-block;
		}

		.tab_con .item {
			height: 200px;
			width: 200px;
			background-color: pink;
			display: none;
		}

		.current {
			background-color: darkred;
			color: white;
			display: inline-block;

		}
	</style>
	<script src="jquery.min.js"></script>

	<div class="tab">
		<div class="tab_list">
			<ul>
				<li class="current">a</li>
				<li>b</li>
				<li>c</li>
				<li>d</li>
				<li>e</li>
			</ul>
		</div>
		<div class="tab_con">
			<div class="item" style="display:block;">a_content</div>
			<div class="item">b_content</div>
			<div class="item">c_content</div>
			<div class="item">d_content</div>
			<div class="item">e_content</div>
		</div>
	</div>


	<script>
		$(function () {
			$(".tab_list li").click(function () {
				// 点击上部的li, 当前li添加current类,其余兄弟移除类
				// 链式编程操作
				console.log($(this));
				$(this).addClass("current").siblings().removeClass("current");

				// 得到li的索引号
				var index = $(this).index();
				// 让下部里面相应索引号的item显示,其余item隐藏
				$('.tab_con .item').eq(index).show().siblings().hide();
			})
		})
	</script>

```

## 类操作与className的区别

- 原生JS种的className会覆盖元素原先的类名
- jquery的类操作只对特定类进行操作,不影响原先类名

```html
<script src="jquery.min.js"></script>
	<style>
		.one {
			background-color: pink;
			height: 200px;
			width: 200px;
		}

		.two {
			transform: rotate(720deg);
		}
	</style>
	<div class="one"></div>
	<script>
		// var one = document.querySelector('.one');
		// one.className = 'two'; //会覆盖掉原有类名one

		$('.one').addClass('two');  //原有类名和新类名同时都有,addClass相当于追加类名

		$('.one').removeClass('two');  //移除类名
	</script>
```

# jquery 效果
动画效果,常见的如:
- 显示隐藏 show() hide() toggle()
- 滑动 slideDown() slideUp() slideToggle()
- 淡入淡出 fadeIn() fadeOut() fadeToggle() fadeTo()
- 自定义动画 animate() 

## 显示隐藏效果

显示/隐藏/切换,语法规范 `show([speed,[easing],[fn]])`
- 三个参数可以都省略,无动画直接显示
- speed: 速度,预定速度字符串'slow' 'normal' 'fast' 或者表示动画时长的毫秒数值,如1000
- easing: 用来指定切换效果, 默认是'swing', 可用参数 'linear'
- fn: 回调函数,可以再动画完成时执行的函数,每个元素执行一次

```html
<style>
		div {
			width: 200px;
			height: 200px;
			background-color: pink;
		}
	</style>
	<script src="jquery.min.js"></script>
	<button>show</button>
	<button>hide</button>
	<button>toggle</button>
	<div></div>
	<script>
		$(function () {
			$('button').eq(0).click(function () {
				$('div').show(1000, function () {
					alert('1');
				});
			})

			$('button').eq(1).click(function () {
				$('div').hide(1000, function () {
					alert('1');
				});
			})

			$('button').eq(2).click(function () {
				$('div').toggle(1000, function () {
					alert('1');
				});
			})
			//一般情况下,我们都不加参数,直接显示或者隐藏
		});
	</script>
```

## 滑动效果

- 语法规范  `slideDown([speed,[easing],[fn]])`, 和show()系列是一样的

```html
<style>
	div {
		width: 200px;
		height: 200px;
		background-color: pink;
		display: none;
	}
</style>
<script src="jquery.min.js"></script>
<button>slideDown</button>
<button>slideUp</button>
<button>sildeToggle</button>
<div></div>
<script>
	$(function () {
		$('button').eq(0).click(function () {
			$('div').slideDown(1000);
		})
		$('button').eq(1).click(function () {
			$('div').slideUp(500);
		})
		$('button').eq(2).click(function () {
			$('div').slideToggle(500);
		})
	});
</script>
```

## 事件切换

`hover([over,] out)`
over 鼠标经过触发的函数,相当于mouseover
out 鼠标离开触发的函数,相当于mouseout


> 利用该函数对前述新浪微博导航栏的写法再改进

```html
<script src="jquery.min.js"></script>
<script>
		$(function () {
			// 鼠标经过
			// $('.nav>li').mouseover(function () {
			// 	// $(this) jQuery 中的当前元素 无需引号
			// 	// show() 显示元素 hide() 隐藏元素
			// 	// $(this).children('ul').show();
			// 	$(this).children('ul').slideDown(200);  //改成动画效果
			// })
			// // 鼠标移开
			// $('.nav>li').mouseout(function () {
			// 	// $(this).children('ul').hide();
			// 	$(this).children('ul').slideUp(200);  //改成动画效果
			// })


			// 简化
			// 鼠标经过和离开的复合效果
			// $('.nav>li').hover(function () {
			// 	$(this).children('ul').slideDown(200);
			// }, function () {
			// 	$(this).children('ul').slideUp(200);   
			// })


			// 极度简化
			// hover如果只写一个函数,那么鼠标经过和离开都会触发这个函数
			$('.nav>li').hover(function () {
				$(this).children('ul').slideToggle(200);
			})
		})
	</script>

```
## 动画队列及其停止排队方法

- 动画队列/效果队列:动画或者效果一旦触发就会执行,如果多次触发,就会造成多个动画或者效果排队执行
- 停止排队 `stop()` 停止上一次动画
- `stop()`必须写到动画前面
 
```html
<script src="jquery.min.js"></script>
<script>
		$(function () {
			$('.nav>li').hover(function () {
				// stop()方法必须写到动画前面
				$(this).children('ul').stop().slideToggle(200);
			})
		})
	</script>

```

## 淡入淡出效果

- 有四个:`fadeIn()` `fadeOut()`  `fadeToggle()` `fadeTo()`
- 前三个语法规范: `fadeIn([speed,[easing],[fn]])`, 和show()系列是一样的
- `fadeTo()`语法规范: `fadeTo([speed,opacity,[easing],[fn]])` 
  - opacity 为透明度必须写, 取值0~1之间
  - speed: 速度,预定速度字符串'slow' 'normal' 'fast' 或者表示动画时长的毫秒数值,如1000
  - easing: 用来指定切换效果, 默认是'swing', 可用参数 'linear'
  - fn: 回调函数,可以再动画完成时执行的函数,每个元素执行一次

## 案例: 高亮显示案例

```html
<style type="text/css">
		* {
			margin: 0;
			padding: 0;
		}

		ul {
			list-style: none;
		}

		body {
			background: #000;
		}

		.wrap {
			margin: 100px auto 0;
			width: 630px;
			height: 394px;
			padding: 10px 0 0 10px;
			background: #000;
			overflow: hidden;
			border: 1px solid #fff;
		}

		.wrap li {
			float: left;
			margin: 0 10px 10px 0;
		}

		.wrap img {
			display: block;
			border: 0;
			width: 200px;
			height: 200px;
		}
	</style>

	<script src="jquery.min.js"></script>

	<div class="wrap">
		<ul>
			<li>
				<a href="#"><img src="images/01.jpg" alt="" /></a>
			</li>
			<li>
				<a href="#"><img src="images/02.jpg" alt="" /></a>
			</li>
			<li>
				<a href="#"><img src="images/03.jpg" alt="" /></a>
			</li>
			<li>
				<a href="#"><img src="images/04.jpg" alt="" /></a>
			</li>
			<li>
				<a href="#"><img src="images/05.jpg" alt="" /></a>
			</li>
			<li>
				<a href="#"><img src="images/06.jpg" alt="" /></a>
			</li>
		</ul>
	</div>


	<script>
		$(function () {
			$('.wrap li').hover(function () {
				// 鼠标进入, 其他的li透明度降低为0.5
				$(this).siblings().stop().fadeTo(400, 0.5);
			}, function () {
				// 鼠标离开, 其他的li透明度恢复为1
				$(this).siblings().stop().fadeTo(400, 1)
			})
		})
	</script>
```

## 自定义动画 animate 

- 语法规范: `animate(params, [speed], [easing], [fn])`
- params: 想要更改的样式属性,以对象形式传递,必须写,属性名可以不带引号,如果是复合属性需要采用驼峰命名法,其余的参数都可以省略

```html
<style>
		div {
			position: absolute;
			width: 200px;
			height: 200px;
			background-color: pink;
		}
	</style>
	<script src="jquery.min.js"></script>
	<button>动起来</button>
	<div></div>
	<script>
		$(function () {
			$('button').click(function () {
				$('div').animate({
					left: 500,
					top: 300,
					opacity: 0.4,
					width: 500
				}, 500);
			})
		})
	</script>
```

## 案例:王者荣耀手风琴效果(折叠卡片)
效果分析:
- 鼠标经过某个小li, 
  - 当前li宽度变为224px
  - 同时里面的图片淡出, 大图片淡入
  - 其余兄弟li宽度变为69px, 小图片淡入, 大图片淡出

```html
<script>
		$(function () {
			// 鼠标经过某个小li
			$('.king li').mouseenter(function () {
				// 当前li宽度变为224px, 同时里面的图片淡出, 大图片淡入
				$(this).stop().animate({
					width: 224
				}, 200).find('.small').stop().fadeOut().siblings('.big').stop().fadeIn();

				// 其余兄弟li宽度变为69px, 小图片淡入, 大图片淡出
				$(this).siblings('li').stop().animate({
					width: 69
				}, 200).find('.small').stop().fadeIn().siblings('big').stop().fadeOut();
			})
			// 记得加stop()
		})
</script>
```

# jquery 属性操作

- 获取元素固有属性值 `prop('attributeName')`
- 设置~ : `prop('attributeName')`
- 获取元素自定义属性值: `attr('attributeName')`
- 设置~: `attr('attributeName')`
- `attr()`方法也可以获取h5自定义属性

数据缓存
- `data()`方法可以再指定的元素上存取数据,并不会修改DOM元素的结构,一旦页面刷新,之前存放的数据都将被移除
- 附加数据语法 `data('name','value')`
- 获取数据语法 `data('name')`
- 同时该方法还可以读取会h5自定义属性(可省略data-前缀),得到的是数字型

```html
	<a href="http://cn.bing.com" title="good">hahahhaha</a>
	<input type="checkbox" checked>
	<div index="nothing" data-index="2">自定义</div>
	<span>123</span>
	<script>
		$(function () {
			// 获取固有属性值
			console.log($('a').prop('href'));

			// 设置固有属性值
			$('a').prop('title', 'all good');
			$('input').change(function () {
				console.log($(this).prop('checked'));  // true|false
			})

			// 获取自定义属性
			console.log($('div').attr('index'));  // nothing

			// 设置自定义属性
			$('div').attr('index', 'something')
			console.log($('div').attr('index'));  // something
			console.log($('div').attr('data-index'));  // 2

			// 数据缓存 data() 存放在元素的内存里面
			$('span').data('uname', 'andy');
			console.log($('span').data('uname')); // 可以取到andy
			console.log($('div').data('index'));  //可以不用写data-前缀,同样可以取到值2, 2为数字型
		})
	</script>
```

## 案例:购物车模块-全选

案例分析:点击上面或者下面的全选按钮,所有商品都选中
- 全选思路:里面3个小的复选框按钮 j-checkbox 选中状态 checked 跟着全选 checkall 按钮走
- 因为 checked 是复选框的固有属性,所以利用 prop() 方法获取和设置该属性
- 把全选按钮状态赋值给三个小的复选框即可
- 当我们每次点击小的复选框按钮时,就做判断,如果小的复选框被选中的个数等于3,就应该把全选按钮选上,否则不选
- `:checked` 选择器 查找被选中的表单元素
- 
```html
<script>
		$(function () {
			// 全选功能, 把全选按钮的状态赋值给三个小的按钮即可
			$('.checkall').change(function () {
				$('.j-checkbox, .checkall').prop('checked', $(this).prop('checked'));
			})

			// 单个点击小的按钮, 所有的都选中后, 全选按钮也自动跟着选中
			$('.j-checkbox').change(function () {
				// 被选中的复选框个数 = 所有的复选框个数
				if ($('.j-checkbox:checked').length === $('.j-checkbox').length) {
					$('.checkall').prop('checked', true);
				} else {
					$('.checkall').prop('checked', false);
				}
			})
		})
	</script>
```

# jquery 文本属性值
- 主要针对元素的内容/表单的值 操作
- 普通元素内容 `html()` 相当于原生的 `innerHTML()`
  - `html()` 获取元素内容
  - `html('content')` 设置元素内容
- 普通元素文本内容 `text()` 相当于原生的 `innerText()`
  - `text()` 获取元素文本内容
  - `text('content')` 设置元素文本内容
- 表单元素的值 `val()`
  - `val()` 获取元素内容
  - `val('content')` 设置元素内容


```html
<div>
		<span>iamcontent</span>
	</div>
	<input type="text" value="please enter something">
	<script>
		$(function () {
			// 设置元素内容 html()
			console.log($('div').html());
			$('div').html('123');

			// 设置文本内容 text()
			console.log($('div').text());
			$('div').text('123');

			// 设置表单的值 val()
			console.log($('input').val());
			$('input').val('changed');
		})
	</script>
```

## 案例: 购物车增减商品数量

核心思路:
- 首先声明一个变量,点击+号,就让这个值++,然后赋值给文本框
- 注意只能增加本商品的数量,即当前+号的兄弟文本框的值
- 修改表单的值用val()方法
- 变量的初始值是文本框的值,在这个值的基础上++
- 减号的思路同理,如果文本框的值是1,就不能再减了

```html
<script>
		$(function () {

			// 增加
			$('.increment').click(function () {
				// 得到当前兄弟文本框的值
				var n = $(this).siblings('.itxt').val();
				n++;
				$(this).siblings('.itxt').val(n);
			})


			// 减少
			$('.decrement').click(function () {
				var n = $(this).siblings('.itxt').val();
				// 减不能小于1
				if (n == 1) {
					return false;
				} else {
					n--;
				}
				$(this).siblings('.itxt').val(n);
			})
		})
	</script>
```

## 案例: 购物车修改商品小计

小计模块
- 核心思路:每次点击加号或者剑减号,根据文本框的值乘以当前商品的价格,就是商品的小计
- 注意只能增加本商品的小计模块
- 修改普通元素的内容用 text() 方法
- 当前商品的价格要把人民币符号去掉再相乘,截取字符串用 substr()方法
- parents('selector') 方法可以返回指定祖先元素
- 最后计算的结果如果想保留两位小数可以使用 toFixed(2) 方法
- 用户也可以直接修改表单里面的值,同样要计算小计,用表单change事件
- 用最新的表单内的值乘以单价即可,但是还是当前商品小计

总计和总额模块
- 核心思路:把所有文本框里面的值相加就是总计数量,总额同理
- 文本框里面值不相同,如果想要相加需要用到each()遍历,声明一个变量,相加即可
- 点击加减号,会改变总结和总额,如果用户修改了文本框里面的值同样会改变总计和总额
- 因此可以封装一个函数求总计和总额,以上2个操作调用这个函数即可
- 注意:总计是文本框里面的值相加用val() 总额是普通元素内容用text()
- 注意:普通元素里面的内容要去掉￥并且转换为数字型才能相加

```html
<script>
		$(function () {

			// 增加数量 商品小计随之改变
			$('.increment').click(function () {
				// 得到当前兄弟文本框的值
				var n = $(this).siblings('.itxt').val();
				n++;
				$(this).siblings('.itxt').val(n);

				// 计算当前商品的价格
				var p = $(this).parents('.p-num').siblings('.p-price').html();
				// 去掉人民币符号
				p = p.substr(1);
				$(this).parents('.p-num').siblings('.p-sum').html('￥' + (p * n).toFixed(2)); // toFixed(2) 结果保留2位小数

			})


			// 减少数量 商品小计随之改变
			$('.decrement').click(function () {
				var n = $(this).siblings('.itxt').val();
				// 减不能小于1
				if (n == 1) {
					return false;
				} else {
					n--;
				}
				$(this).siblings('.itxt').val(n);
				getSum(); // 总计随之变化

				// 计算当前商品的价格
				var p = $(this).parents('.p-num').siblings('.p-price').html();
				p = p.substr(1);
				$(this).parents('.p-num').siblings('.p-sum').html('￥' + (p * n).toFixed(2));
				getSum(); // 总计随之变化
			})

			// 用户修改文本框的值 计算小计模块
			$('.txt').change(function(){
				// 先得到文本框里面的值 乘以 当前商品的单价
				var n = $(this).val();
				var p = $(this).parents('.p-num').siblings('.p-price').html();
				p = p.substr(1);
				$(this).parents('.p-num').siblings('.p-sum').html('￥' + (p * n).toFixed(2));
				getSum(); // 总计随之变化

			})

			// 总计和总额模块
			getSum(); // 进入页面先调用一次
			// 总计
			function getSum() {
			var count = 0;  // 计算总件数
			var money = 0;  // 计算总价钱
			$('.itxt').each(function (i, ele) {
				count += parseInt($(ele).val());
			})

			$('.amount-sum em').text(count);

			// 总额
			$('.p-sum').each(function (i,ele) {
				money += parseFloat($(ele).text().substr(1));
			})
			$('.price-sum em').text('￥'+ money.toFixed(2));


		}


		})
	</script>
```


寻找祖先元素 parents()

```html
<div class="one">
		<div class="two">
			<div class="three">
				<div class="four">
					我不容易
				</div>
			</div>
		</div>
	</div>
	<script>
		// 一个一个寻找父节点
		$('.four').parent().parent().parent();

		// parents('selector') 可以返回祖先元素 
		$('.four').parents('.one');	
	</script>
```


# jquery 元素操作

主要是遍历 创建 添加 删除 元素操作

## 遍历元素

jquery隐式迭代是对同一类元素做相同操作,如果想给同一类元素做不同操作,就需要用到遍历

语法:`$('div'.each(fucntion(index, domEle){xxx;}))`

1. each() 方法遍历匹配的每一个元素, 主要用DOM处理
2. 里面的回调函数有两个参数, index是元素的索引号, domEle 每个DOM元素对象, 而不是jquery对象
3. 要使用jquery方法, 需要将DOM元素转换为jquery对象 $(domEle)

```html
	<div>111</div>
	<div>222</div>
	<div>333</div>
	<script>
		$(function () {
			var arr = ['red', 'green', 'blue'];
			var sum = 0;
			$('div').each(function (i, domEle) {
				// 回调函数第一个参数为索引号,名称可以自定义
				// 回调函数第二个参数为dom对象,使用jquery方法需要转换

				// 借助数组为每个元素添加不同颜色
				$(domEle).css('color', arr[i]);

				// 累加三个div内的值, 需要转换为字符型
				sum += parseInt($(domEle).text());
			})
			console.log(sum);
		})
	</script>
```

另一种遍历方式 `$.each(object, function(index, element){xxx;})`

1. $.each() 方法可用于遍历任何对象,主要用于**数据处理**,比如数组,对象
2. 里面的函数有2个参数, index是元素索引号,element遍历内容

```html
	<div>111</div>
	<div>222</div>
	<div>333</div>
	<script>
		$(function () {
			var arr = ['red', 'green', 'blue'];

			// 遍历元素
			$.each($('div'), function (i, ele) {
				console.log(i);
				console.log(ele);
			})

			// 遍历数组
			$.each($(arr), function (i, ele) {
				console.log(i);
				console.log(ele);
			})

			// 遍历对象
			$.each({ name: 'andy', age: 18 }, function (i, ele) {
				console.log(i);  // 输出属性名
				console.log(ele); // 输出属性值
			})
		})
	</script>
```

## 创建元素

直接写HTML标签用$()包裹即可动态创建

语法:`$('<li></li>')`

## 添加元素

1. 内部添加 

- `element.append('content')` 把内容添加到匹配元素内部最后面,类似原生的appendChild
- `element.prepend('content')` 把内容添加到匹配元素内部最前面

2. 外部添加

- `element.before('content')` 把内容添加到目标元素后面
- `element.after('content')` 把内容添加到目标元素前面

内部添加元素,生成之后,是父子关系
外部添加元素,生成之后,是兄弟关系


## 删除元素

- `element.remove()` 删除匹配的元素(自杀)
- `element.empty()` 删除匹配的元素集合中所有的子节点(杀孩子)
- `element.html('')` 清空匹配的元素内容(换成空)

```html
	<ul>
		<li>
			我是原先的li
		</li>
	</ul>
	<div class="test">我是原先的div</div>
	<script>
		// 创建元素
		var li = $('<li>我是后来的li</li>');
		var lili = $('<li>我是后来的lili</li>');

		// 添加元素

		// (1)内部添加
		$('ul').append(li);  // 放到原来的小li后面
		$('ul').prepend(lili);

		// (2)外部添加
		var div1 = $('<div>我是后来的div1</div>');
		var div2 = $('<div>我是后来的div2</div>');

		$('.test').after(div1);
		$('.test').before(div2);

		// 删除元素
		// $('ul').remove();
		// $('ul').empty(); // ul还在,只是内部的小li都没了
		$('ul').html(''); //ul还在,内部换成空白
```

## 案例: 购物车删除商品模块

- 核心思路：把商品remove() 删除元素即可
- 有三个地方可以进行删除操作：1. 商品后面的删除按钮，2. 删除选中的商品 3. 清理购物车
- 商品后面的删除按钮：一定是删除当前的商品，所以从$(this)出发
- 删除选中的商品：先判断小的复选框按钮是否为选中状态，如果是选中，则删除对应的商品
- 清理购物车：


```html 
<script>
		// 删除商品模块
		// 1. 商品后面的删除按钮
		$('.p-action a').click(function () {
			// 删除当前的商品
			$(this).parents('.cart-item').remove();
			getSum(); //删除后重新计算价格
		})

		// 2. 删除选中的商品
		$('.remove-batch').click(function () {
			$('.j-checkbox:checked').parents('.cart-item').remove(); //含有隐式迭代
			getSum();
		})

		// 3. 清理购物车
		$('.clear-all').click(function () {
			$('.cart-item').remove();
			getSum();
		})
</script>
```

## 案例：购物车案例-选中商品添加背景

- 核心思路：选中的商品添加背景，不选中移除背景即可
- 全选按钮点击：如果全选是选中的，则所有的商品添加背景，否则移除背景
- 小的复选框点击：如果为选中状态，则当前商品添加背景，否则移除背景
- 这个背景，可以童工类名修改，添加类和删除类

```html
<style>
		.check-cart-item {
			background: #fff4e8;
		}
</style>

<script>
		$(function () {
			// 全选功能, 把全选按钮的状态赋值给三个小的按钮即可
			$('.checkall').change(function () {
				$('.j-checkbox, .checkall').prop('checked', $(this).prop('checked'));
				if ($(this).prop('checked')) {
					// 添加类名 check-cart-item
					$('.cart-item').addClass('check-cart-item');
				} else {
					// 移除类名 check-cart-item
					$('.cart-item').removeClass('check-cart-item');
				}

				// 单个点击小的按钮, 所有的都选中后, 全选按钮也自动跟着选中
				$('.j-checkbox').change(function () {
					// 被选中的复选框个数 = 所有的复选框个数
					if ($('.j-checkbox:checked').length === $('.j-checkbox').length) {
						$('.checkall').prop('checked', true);
					} else {
						$('.checkall').prop('checked', false);
					}

					if ($(this).prop('checked')) {
						// 当前商品添加类名 check-cart-item
						$(this).parents('.cart-item').addClass('check-cart-item');
					} else {
						// 当前商品移除类名 check-cart-item
						$(this).parents('.cart-item').removeClass('check-cart-item');
					}
				})
			})
		})
</script>
```


# jquery 尺寸、位置操作

???
