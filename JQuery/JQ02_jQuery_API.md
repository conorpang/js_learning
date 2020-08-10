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
- [jquery 属性操作](#jquery-属性操作)
- [jquery 文本属性值](#jquery-文本属性值)
- [jquery 元素操作](#jquery-元素操作)
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
		// sibilings 选取的除了自身以外的所有亲兄弟
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
			$(this).children('ul').show();
		})
		// 鼠标移开
		$('.nav>li').mouseout(function () {
			$(this).children('ul').hide();
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

显示,语法规范 `show([speed,[easing],[fn]])`
- 三个参数可以都省略,无动画直接显示
- speed: 速度,预定速度字符串'slow' 'normal' 'fast' 或者表示动画时长的毫秒数值,如1000
- easing: 用来指定切换效果, 默认是'swing', 可用参数 'linear'
- fn: 回调函数,可以再动画完成时执行的函数,每个元素执行一次

隐藏/切换,语法规范 `hide/toggle([speed,[easing],[fn]])`,用法和show()类似

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

21.over
https://www.bilibili.com/video/BV1Wz411B7N5?p=22



# jquery 属性操作
# jquery 文本属性值
# jquery 元素操作
# jquery 尺寸、位置操作