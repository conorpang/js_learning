【变量】

- [变量概述](#变量概述)
- [变量的使用](#变量的使用)
- [变量的使用](#变量的使用-1)
	- [案例01](#案例01)
	- [案例02](#案例02)
- [变量语法扩展](#变量语法扩展)
- [变量命名规范](#变量命名规范)
- [交换变量案例](#交换变量案例)
- [变量小结](#变量小结)

# 变量概述

- 装东西的盒子，容器，通过变量名获取，可以修改
- 本质：内存中一块存放数据的空间

```html
<script>
	num1 = 5
	num2 = 6

	age = 18
	name = "pink老师"
</script>
```

# 变量的使用

```html
<script>
	// 1.声明
	var age; //age为变量名  //var是固定的，age是变量名，自己定


	// 2.赋值
	age = 10; //把这个变量赋值为10
	
	// 3.输出结果
	console.log(age);
	
	// 4.变量的初始化
	var myName = 'pink老师';
</script>
```


# 变量的使用

## 案例01

有个叫卡卡西的人在旅店登记的时候前台让他填一张表，这张表里的内容要存到电脑上，表中的内容有：姓名、年龄、邮箱、家庭住址和工资，存储之后需要把这些信息显示出来，所显示的内容如下：

我叫旗木卡卡西，我住在火影村，我今年30岁了，我的邮箱是kakaxi@itcast.cn，我的工资2000

```html
<script>
	var name = 'kakaxi';
	var address = 'huoyingcun';
	var age = 30;
	var mail = 'kakaxi@itcast.cn'

	console.log(name);
	console.log(address);
	console.log(age);
	console.log(mail);
</script>
```


## 案例02

1.弹出一个输入框，提示用户输入姓名。
2.弹出一个对话框，输出用户刚才输入的姓名。

```html
<script>
	var myname = prompt('input name:');
	alert(myname);
</script>
```


# 变量语法扩展

重新赋值会覆盖原有，以最后一次为准

```html
<script>
	//声明一个变量并赋值
	var age = 18;
	age = 81;

	//声明多个变量
	var age = 18, address = 'huoyingcun', sex = 2;
</script>
```

特殊情况

1. 声明不赋值，结果是undefined
2. 不声明不赋值，直接使用会报错 is not deined
3. 不声明直接赋值，可以使用，但是不推荐这样用


# 变量命名规范

- 由字母（A-Za-z）、数字（0-9）、下划线（_）、美元符号（$）组成，如：usrAge，num01，name
- 严格区分大小写，var app; var App; 是两个变量
- 不能以数字开头，18age是错误的
- 不能是关键字、保留字，例如：var、for、while
- 变量名必须有意义
- 遵守驼峰命名法，首字母小写，后面单词的首字母需要大写，myFirstName
- 最好不要用name这个词命名，因为这个词在浏览器中有特殊含义


# 交换变量案例

要求：交换两个变量的值（实现思路：使用一个临时变量用来做中间存储）

```html
<script>
	var apple1 = '青苹果', apple2 = '红苹果', temp;

	temp = apple1;
	apple1 = apple2;
	apple2 = temp;

	console.log(apple1);
	console.log(apple2);
</script>
```


# 变量小结

- 为什么需要变量？

因为我们一些数据需要保存，所以需要变量

- 变量是什么？

变量就是一个容器，用来存放数据的。方便我们以后使用里面的数据

- 变量的本质是什么？

变量是内存里的一块空间，用来存储数据。

- 变量怎么使用的？

我们使用变量的时候，一定要声明变量，然后赋值
声明变量本质是去内存申请空间。

- 什么是变量的初始化？

声明变量并赋值我们称之为变量的初始化

- 变量命名规范有哪些？

变量名尽量要规范，见名知意驼峰命名法，区分哪些变量名不合法

- 交换2个变量值的思路？

学会交换2个变量