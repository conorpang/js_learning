【jQuery常用API】

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

- `parent()` 用法: `$('li').parent()` 说明:查找父级
- `children(selector)` 用法: `$('ul').('li')` 说明:查找最近一级的子元素(亲儿子),相当于 `$('ul>li')`
- `find(selector)` 用法: `$(ul).find('li')` 说明:后代选择器,相当于`$('ul li')`
- `siblings(selector)` 用法: `$('.first').siblings(li)` 说明: 查找兄弟接节点,不包括本身
- `nextAll([expr])` 用法: `$('.first').nextAll()` 说明: 查找当前元素之后所有的同辈元素
- `prevAll([expr])` 用法: `$('.last').prevAll()` 说明: 查找当前元素之前所有的同辈元素
- `hasClass(class)` 用法: `$('div').hasClass(protected)` 说明: 检查当前元素是否含有某个特定的类,如果由,返回true
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
		console.log($('.son').parent());
		// 子 
		// children() 返回的是最近一级的子元素
		$('.nav').children('p').css('color', 'purple');
		// find()  返回的是所有子代元素
		$('.nav').find('div p').css('color', 'green');
		// 兄
		console.log($('.nav p').siblings('div'));
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

13.over
https://www.bilibili.com/video/BV1Wz411B7N5?p=14

# jquery 样式操作
# jquery 效果
# jquery 属性操作
# jquery 文本属性值
# jquery 元素操作
# jquery 尺寸、位置操作