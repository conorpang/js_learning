# jquery 事件
- [jquery 事件](#jquery-事件)
- [jquery 事件注册](#jquery-事件注册)
- [jquery 事件处理](#jquery-事件处理)
	- [事件绑定on()](#事件绑定on)
	- [案例：发布微博](#案例发布微博)
	- [事件解绑off()](#事件解绑off)
	- [自动触发事件 trigger()](#自动触发事件-trigger)
- [jquery 事件对象](#jquery-事件对象)


# jquery 事件注册

单个事件注册

- 以前的写法 element.event(function(){})
- eg: $('div').click(funcion(){ ... })
- 基本和原生JS一致

# jquery 事件处理

## 事件绑定on()

- on() 方法在匹配元素上绑定一个或多个事件的处理函数
- 语法 element.on(events, (selector), fn)

说明
1. events 一个或多个用空格分隔的事件类型，如click， keydown
2. selector 元素的子选择器
3. fn 回调函数 即绑定在元素身上的侦听函数

优势
1. 可以绑定多个事件，多个事件处理程序;;可以为多个事件绑定相同的处理程序
2. 可以事件委派操作，即把原来加给子元素身上的事件绑定在父元素身上，把事件委派给父元素（此前有bind() delegate()等方法处理事件绑定或者事件委派，最新版本请用on()方法）
3. 可以为动态创建的元素绑定事件

```html
	<style>
		div {
			height: 200px;
			width: 200px;
			background-color: pink;
		}

		.current {
			background-color: purple;
		}
	</style>
	<div></div>
	<ul>
		<li>we are good kids</li>
		<li>we are good kids</li>
		<li>we are good kids</li>
		<li>we are good kids</li>
	</ul>
	<ol>

	</ol>
	<script>
		$(function () {
			// 单个事件注册
			// $('div').click(function () {
			// 	$(this).css('background', 'purple');
			// })

			// $('div').mouseover(function () {
			// 	$(this).css('background', 'skyblue');
			// })

			// 事件处理on 内部可以以对象的形式绑定多个事件
			$('div').on({
				mouseenter: function () {
					$(this).css('background', 'skyblue');
				},
				click: function () {
					$(this).css('background', 'purple');
				},
				mouseleave: function () {
					$(this).css('background', 'blue');
				}
			})

			// 多个事件相同的处理程序
			$('div').on('mouseenter mouseleave', function () {
				$(this).toggleClass('current');
			})

			// on可以实现事件委托
			// $('ul li').click(); 存在隐式迭代
			$('ul').on('click', 'li', function () {  //事件绑定在ul上，li为触发元素
				alert('yes, you are!');  //会事件冒泡
			})

			// 为未来动态创建的元素绑定事件
			// $('ol li').click(function () {
			// 	alert('li');    // 这里绑定的事件对未来创建的元素无效
			// })

			$('ol').on('click', 'li', function () {
				alert('li');  // 可以为未来动态创建的元素绑定事件
			})

			var li = $('<li>我是后来创建的li</li>');
			$('ol').append(li);
		})
	</script>
```

## 案例：发布微博

- 点击发布按钮，动态创建一个小li，放入文本框的内容和删除按钮，将这个小li添加到ul中
- 点击删除按钮，可以删除当前微博

```html
	<style>
		div {
			border: 1px solid black;
			margin: 50px;
			padding: 10px;
		}

		ul li {
			display: none;
		}
	</style>
	<div class="box" id="weibo">
		<span>微博发布</span>
		<textarea name="" id="" cols="80" rows="10" class="txt"></textarea>
		<button class="btn">发布</button>
		<ul>

		</ul>
	</div>

	<script>
		$(function () {
			// 点击发布按钮，动态创建一个小li，放入文本框的内容和删除按钮，将这个小li添加到ul中
			$('.btn').on('click', function () {
				var li = $('<li></li>');
				li.html($('.txt').val() + '<a href = "javascript:;">删除</a>');
				$('ul').prepend(li);
				li.slideDown();  // 下滑的动态效果
				$('.txt').val('');
			})

			// 点击删除按钮，可以删除当前微博
			$('ul').on('click', 'a', function () {
				$(this).parent().slideUp(function () {   // 上滑的动态效果
					$(this).remove();
				});
			})
		})
	</script>
```

## 事件解绑off()

off()方法可以移除通过on()方法添加的事件处理程序

```html
<style>
		div {
			width: 200px;
			height: 200px;
			background-color: pink;
		}
	</style>
	<div></div>
	<ul>
		<li>we are good kids</li>
		<li>we are good kids</li>
		<li>we are good kids</li>
		<li>we are good kids</li>
	</ul>

	<script>
		$(function () {
			$('div').on({
				click: function () {
					console.log('i clicked');
				},
				mouseover: function () {
					console.log('mouse passed over');
				}
			})
			$('ul').on('click', 'li', function () {
				alert('li');
			})

			// 事件解绑 off()
			// $('div').off();  //off()参数为空，解除所有事件
			$('div').off('click');  //解除了click事件
			$('ul').off('click', 'li'); // 解除事件委托

		})
	</script>
```

如果有的事件只触发一次，可以使用one()来绑定事件

```html
	<p>i am p</p>
	<script>
		$('p').one('click', function () {
			alert('one-time p');  //只触发一次
		})
	</script>
```

## 自动触发事件 trigger()

有些事件希望自动触发，比如轮播图自动播放功能跟点击按钮一直，可以利用定时器自动触发右侧按钮点击事件，不必鼠标点击触发

有三种方式
1. element.click() // 第一种简写形式
2. element.trigger('type') // 第二种自动触发方式
3. element.triggerHandler(type)  // 第三种自动触发方式,不会触发元素的默认行为

```html
<style>
	div {
		width: 200px;
		height: 200px;
		background-color: pink;
	}
</style>
<div></div>
<input type="text">
<script>
	$(function () {
		$('div').on('click', function () {
			alert(11);
		})

		// 自动触发事件
		// 1. element.click()
		// $('div').click();

		// 2. element.trigger('type')
		// $('div').trigger('click');

		// 3. element.triggerHandler(type)
		$('div').triggerHandler('click');
		$('input').on('focus', function () {
			$(this).val('nihao');
		});
		$('input').triggerHandler('focus');
	})
</script>
```

# jquery 事件对象

事件被触发,就会有事件对象产生
element.on(events, [selector], function(event){})

- 阻止默认行为: event.preventDefault() / return false
- 阻止冒泡: event.stopPropagation()

```html
<style>
	div {
		width: 200px;
		height: 200px;
		background-color: pink;
	}
</style>
<div></div>
<script>
	$(function () {
		$(document).on('click', function () {
			console.log('点击了doocument');
		})

		$('div').on('click', function (e) {  // 这里的e为事件对象
			console.log('点击了div');
			e.stopPropagation(); // 停止冒泡
		})


	})
</script>
```