【jquery其他方法】

# jquery 拷贝对象

- 如果想把某个对象拷贝给另一个对象使用，可以使用`$.extend()`方法

语法：`$.extend([deep], traget, object1, [objectN])`
1. deep - true 深拷贝，false 浅拷贝
2. target - 要拷贝的目标对象
3. object1 - 待拷贝的第一个对象
4. objectN - 待拷贝的第N个对象
5. 浅拷贝是把被拷贝对象复杂数据类型中的地址拷贝给目标对象，修改目标对象会影响被拷贝对象（复杂数据类型会被覆盖）
6. 深拷贝，前面加true, 完全克隆（拷贝对象，而不是拷贝地址），修改目标对象不会影响被拷贝对象（如果有不冲突的属性，会合并到一起）

```html
<script>
	$(function () {

		var obj = {
			id: 1,
			name: 'andy',
		}

		// targetObj 为空，直接复制新内容进去
		var targetObj1 = {};
		$.extend(targetObj1, obj);
		console.log(targetObj1);


		// targetObj 存在内容，拷贝会覆盖旧内容
		var targetObj2 = {
			id: 0
		}
		$.extend(targetObj2, obj);
		console.log(targetObj2);

		// 拷贝复杂数据类型
		var obj3 = {
			id: 1,
			name: 'andy',
			msg: {
				age: 18
			}
		}
		var targetObj3 = {
			id: 3
		}
		$.extend(targetObj3, obj3);
		console.log(targetObj3);

		// 浅拷贝
		// 修改拷贝后的目标对象中的*复杂数据类型*，会影响被拷贝对象
		targetObj3.id = 100; // 只有目标对象变
		targetObj3.msg.age = 20;  // 目标对象、被拷贝对象都变
		console.log(targetObj3, obj3);

		// 深拷贝
		// 修改目标对象不会影响被拷贝对象
		var obj4 = {
			id: 1,
			name: 'andy',
			msg: {
				age: 18
			}
		}
		var targetObj4 = {
			msg: {
				sex: 'male',
				age: 17
			}
		}
		$.extend(true, targetObj4, obj4);
		targetObj4.id = 2; // 只有目标对象变
		targetObj4.msg.age = 19;  // 只有目标对象变
		console.log(targetObj4, obj4);

	})
</script>
```

小结

|            | 数据类型 | 拷贝什么 | A新属性 | AB冲突属性 | B旧属性  | 修改B      | 修改A     |
| ---------- | -------- | -------- | ------- | ---------- | -------- | ---------- | --------- |
| 浅拷贝A->B | 简单数据 | 拷贝内容 | 添加到B | A覆盖B     | 保留在B  | A不变, B变 | A变,B不变 |
|            | 复杂数据 | 拷贝地址 | 添加到B | A覆盖B     | 直接删除 | AB都变     | AB都变    |
| 深拷贝A->B | 简单数据 | 拷贝内容 | 添加到B | A覆盖B     | 保留在B  | A不变, B变 | A变,B不变 |
|            | 复杂数据 | 拷贝内容 | 添加到B | A覆盖B     | 保留在B  | A不变, B变 | A变,B不变 |

# 多库共存

- 问题概述：jQuery使用$作为标识符，随着jquery的流行，其他js库也会用$做标识符，一起用这些库时会引起冲突
- 客观需求：需要一个解决方案，让jquery和其他的js库不存在冲突，可以同时存在，这叫做多库共存
- jquery解决方案：1. `$` -> `jQuery` 2. 规定新的名称 `var xx = $.noConflict()`

```html
<div></div>
<span></span>

<script>
	$(function () {

		// 封装选择元素的函数$
		function $(ele) {
			return document.querySelector(ele);
		}
		console.log($('div'));

		// $符号冲突，用jQuery代替
		jQuery.each();  

		// 让jQuery释放对$的控制权，用户可以自定义
		var suibian = jQuery.noConflict();   
		console.log(suibian('span'));
	})

</script>
```

# jquery 插件

## jquery 插件

- jquery功能比较有限，想要有更加复杂的特效，可以借助jquery插件完成
- 这些插件也依赖于jquery, 所以必须先引入jquery
- 常用插件网站
  - jquery插件库 http://www.jq22.com/
  - jquery之家 http://www.htmleaf.com/ 均为免费开源


使用方法
- 下载，解压，进入index文件源代码
- 复制html,css和js

举例:
- 瀑布流插件
- 图片懒加载 easyLazyLoad
  - 图片使用延迟加载,可提高网页下载速度,也能帮助减轻服务器负载
  - 当滑动到可视区域时,再加载图片
- 全屏滚动 fullpage.js [github](https://github.com/alvarotrigo/fullPage.js/tree/master/lang/chinese#fullpagejs)

## bootstrap JS 插件

bootstrap框架也是依赖于jquery开发的，因此里面的js插件使用，也必须引入jquery文件（需要引入bootstrap的css/js，jquery的js）

[bootstrap JS插件](https://v3.bootcss.com/javascript/)
- 组件：常用功能组合在了一起
- JS插件：模态框、标签页、按钮等

# 案例：阿里百秀

bootstrap直接找组件复制后按需修改

# 综合案例： ToDOList

1. 功能介绍
   - 文本框里面输入内容，按下回车，就可以生成待办事项
   - 点击待办事项复选框，可以把当前数据添加到已完成事项里面
   - 点击已完成事项复选框，可以把当前数据添加到待办事项里
   - 本页面内容刷新后不会丢失（本地存储）

2. 前期准备
   - 基本HTML骨架代码
   - 引入的css，js
   - 自己的js可以单独写一个文件再引入


P58.over
https://www.bilibili.com/video/BV1Wz411B7N5?p=59