# Vue基础

- [Vue基础](#vue基础)
- [课程介绍](#课程介绍)
- [简介](#简介)
- [第一个Vue程序](#第一个vue程序)
- [el: 挂载点](#el-挂载点)
- [data: 数据对象](#data-数据对象)

# 课程介绍

Vue 学习前需要掌握
- HTML
- CSS
- Javascript
- Ajax

开发工具
- 开发工具 VScode
- 插件 Live Server 浏览器实时预览

课程安排
- vue基础
- 本地应用
- 网络应用
- 综合应用


# 简介

- JS框架
- 简化DOM操作：Vue特殊语法
- 响应式数据驱动


# 第一个Vue程序

- Vue文档：https://cn.vuejs.org
- 作者：尤雨溪

步骤：
- 导入‘开发版本’的Vue.js
- 创建Vue实例对象，设置el属性和data属性
- 使用简洁的模板语法{{}}把数据渲染到页面上


```html
<div id="app">
	{{ message }}
</div>

<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

<script>
	var app = new Vue({
		el: '#app',
		data: {
			message: 'Hello Vue!'
		}
	})
</script>
```

# el: 挂载点

el是用来设置Vue实例挂载（mount）的元素

疑问：
- Vue实例的作用范围是什么呢？
Vue会管理el选项命中的元素及其内部的后代元素

- 是否可以使用其他的选择器？
可以使用其他的选择器，但是建议使用ID选择器

- 是否可以设置其他的dom元素呢？
可以使用其他的双标签，不用于单标签，不用于HTML和BODY标签


```js
{{ message }}
<!-- el命中的元素外部不可以作用message属性 -->
<div id="app" class="app">
	{{ message }}
	<span>{{ message }}</span>
	<!-- el命中的元素内部可以作用message属性 -->
</div>

<p id="p"></p>

<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

<script>
	var app = new Vue({
		//el: '#app', //ID选择器，可以作用 //开发中更常使用ID选择器
		//el: '.app', //类选择器，可以作用
		el: 'div', //标签选择器，可以作用
		data: {
			message: 'programmer'
		}
	})
</script>
```


# data: 数据对象

- vue中用到的数据定义在data中
- data中可以写复杂类型的数据
- 渲染复杂类型数据时，遵守JS的语法即可，如{{school.mobile}}


data中除了可以有message，还可以添加别的数据类型

```html
<script>
	var app = new Vue({
		el: '#app',
		data: {
			message: '',
			array: [],
			obj: {}
		}
	})
</script>

<div id="app">
	{{ message }}
	<h2>{{ school.name }} {{ school.mobile }}</h2>
	<ul>
		<li>{{campus[0]}}</li>
		<li>{{campus[1]}}</li>
	</ul>
</div>

<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>


<script>
	var app = new Vue({
		el: '#app',
		data: {
			message: 'Hello Vue!',
			school: {
				name: 'heima',
				mobile: '400-618-9090'
			},
			campus: ['bj', 'sh', 'gz', 'sz']
		}
	})
</script>

```