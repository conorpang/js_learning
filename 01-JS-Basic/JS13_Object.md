【对象】

- [对象的定义](#对象的定义)
- [创建对象的三种方式](#创建对象的三种方式)
	- [利用字面量创建对象](#利用字面量创建对象)
	- [变量、属性、函数、方法总结](#变量属性函数方法总结)
		- [变量和属性](#变量和属性)
		- [函数和方法](#函数和方法)
	- [利用 new Object 创建对象](#利用-new-object-创建对象)
	- [利用构造函数创建对象](#利用构造函数创建对象)
	- [构造函数和对象的区别](#构造函数和对象的区别)
	- [new关键字执行过程](#new关键字执行过程)
- [遍历对象属性](#遍历对象属性)
- [小结](#小结)

# 对象的定义

对象：万物皆对象，一个*具体*的事物

- 苹果：不是对象
- 这个苹果：是对象

在JS中，对象是无序的相关属性和方法的集合，所有的事物都是对象，例如：字符串、数值、数组、函数等

对象包含属性和方法：

- 属性： 事物的特征，常用名词
- 方法： 事物的行为，常用动词


为什么需要对象？

```html
<script>
	// 保存一个值：用变量

	// 保存多个值：用数组
	var arr = ['Jake', 'male', 128, 154];

	// 对象表达结构更清晰
	person.name = 'Jake';
	person.sex = 'male';
	person.age = 128;
	person.height = 154;
</script>
```


# 创建对象的三种方式

对象 object

- 字面量创建
- new Object创建
- 构造函数创建


## 利用字面量创建对象

用花括号 `{ }` 可包含属性和方法

```html
<script>

	// var obj = {}; //创建了一个空的对象
	var obj = {
		uname: 'Jake',
		age: 18,
		sex: 'male',
		sayHi: function () {
			console.log('Hi....')
		}

		// 属性和方法采用键值对的方式，属性名: 属性值（键：值）
		// 多个属性和方法中间用逗号(,)隔开
		// 方法冒号后面跟的是一个匿名函数
	}


	//使用对象

	//调用对象的属性，方法1：对象名.属性名
	console.log(obj.uname);

	//调用对象的属性，方法2：对象名['属性名']
	console.log(obj['uname']);

	//调用对象的方法，对象名.方法名
	obj.sayHi(); //要加小括号()
</script>
```

小练习：

请用对象字面量的形式创建一个名字为可可的狗对象。
- 姓名：可可
- 类型：阿拉斯加犬
- 年龄：5岁
- 颜色：红色
- 技能：汪汪bark，演电影showFilm

```html
<script>
	var dogObj = {
		name: 'keke',
		type: 'alaska',
		age: 5,
		color: 'red',
		bark: function () {
			console.log('bark...');
		},
		showFilm: function () {
			console.log('show film in houhuiwuqi...');
		}
	}

	console.log(dogObj.name + ', ' + dogObj.type);
</script>
```

## 变量、属性、函数、方法总结


### 变量和属性

```html
<script>

	// 相同点：都是用来存储数据的
	// 不同点：
	// 变量单独声明并赋值，使用的时候直接写变量名，单独存在
	// 属性在对象里面不需要声明，使用的时候必须 对象.属性
	var num = 10;
	var obj = {
		age: 18
	}
</script>
```


### 函数和方法

```html
<script>
	// 相同点：都是实现某种功能的
	// 不同点：
	// 函数是单独声明，并且调用的，函数名单独存在
	// 方法在对象里面，调用的时候，对象.方法

	var num = 10;
	var obj = {
		age: 18,
		fn: function () {

		}
	}

	function fn() {

	}

</script>
```

## 利用 new Object 创建对象
```html
<script>

	var obj = new Object();   //创建了一个空的对象   //注意这里的O要大写
	obj.uname = 'Jake';       //利用等号赋值的方法添加对象的属性和方法
	obj.age = 18;				//每个属性和方法之间用分号结束
	obj.sex = 'male';

	obj.sayHi = function () {
		console.log('Hi~~~');
	}

	console.log(obj.uname);
	console.log(obj['sex']);
	obj.sayHi();

</script>
```


小练习：

请用 new Object形式创建一个鸣人对象

- 姓名：鸣人
- 性别：男
- 年龄：19岁
- 技能：影分身术

```html
<script>
	var mingrenObj = new Object();
	mingrenObj.name = 'mingren';
	mingrenObj.sex = 'male';
	mingrenObj.age = 19;
	mingrenObj.skill = function () {
		for (var i = 0; i < 100; i++) {
			console.log('mingren');
		}
	}
</script>
```

## 利用构造函数创建对象

why?

因为前两种方法一次只能创建一个对象

可以利用函数的方法，重复相同的代码，这个函数称为*构造函数*

因为这个函数封装的不是普通代码，而是*对象*

构造函数就是把对象里面的一些相同的属性和方法抽象出来封装到函数里

```html
<script>
	// 构造函数创建对象
	// 举例：创建四大天王对象，相同的 属性：名字，年龄，性别 方法：唱歌
	// 构造函数的语法格式
	function 构造函数名() {
		this.属性 = 值;
		this.方法 = function () {
		}
	}
	new 构造函数名();
</script>
```




```html
<script>
	function Star(uname, age, sex) {
		this.name = uname;
		this.age = age;
		this.sex = sex;
		this.sing = function (song) {
			console.log(song);
		}
	}
	var ldh = new Star('ldh', 18, 'male'); //调用函数返回的是一个对象
	console.log(typeof ldh);

	console.log(ldh.name);
	console.log(ldh.sex);
	ldh.sing('冰雨');

	var zxy = new Star('zxy', 19, 'male');

// 构造函数的首字母大写
// 构造函数不需要return就可以返回结果
// 调用构造函数必须使用new
// 只要new Star()调用函数就创建了一个对象 ldh{}
// 属性和方法前必须加this

</script>
```

小练习：

利用构造函数创建两个英雄对象，函数的公共部分包括：

| 姓名属性 | 类型属性 | 血量属性 | 攻击方式   |
| -------- | -------- | -------- | ---------- |
| 廉颇     | 力量型   | 500血量  | 攻击：近战 |
| 后羿     | 射手型   | 100血量  | 攻击：远程 |

```html
<script>

</script>
```

## 构造函数和对象的区别

对象是一个具体的事物，特指某一个，如上一例的刘德华

构造函数是泛指的某一大类，抽取了对象的公共部分，类似java的类

利用构造函数创建对象的过程称为对象的‘实例化’，所以上一例的刘德华既可以叫做‘对象’，也可以叫做‘实例’

## new关键字执行过程

```html
<script>
	// new 构造函数可以在内存中创建一个空的对象
	// this 指向刚才创建的对象
	// 执行构造函数里面的代码，给这个空对象添加属性和方法
	// 返回这个对象，所以不需要return

	// new四件事：new和构造函数确认了眼神，
	// 1.生了一个宝宝
	// 2.必须是亲生的this指向
	// 3.教孩子读书一肚子墨水
	// 4.长大挣钱回报父母

</script>
```


# 遍历对象属性

一个一个打印对象属性太过麻烦

```html
<script>
	var obj = {
		name: 'pink',
		age: 18,
		sex: 'male'
	}

	console.log(obj.name);
	console.log(obj.age);
	console.log(obj.sex);

</script>
```



`for...in`语句：用于对数组或者对象的属性进行循环操作

```html
<script>
	for (变量 in 对象) {

	}
</script>
```

```html
<script>
	for (var k in obj) {
		console.log(k);   //k变量输出得到的是 属性名
		console.log(obj[k]);  //obj[k]输出得到的是 属性值 k不加引号

		// for in 变量常用k或者key
		// for in 也可以遍历方法，但是很少用
	}
</script>
```

# 小结

对象可以让代码结构更加清晰
复杂数据类型object
本质：无序的相关属性和方法的集合
构造函数泛指某一大类
对象实例特指某一个事物
for in语句可用于对象属性的循环操作


作业：

1. 创建一个电脑对象，该对象要有颜色、重量、品牌、型号，可以看电影、听音乐、打游戏和敲代码
2. 创建一个按钮对象，该对象包含宽、高、背景颜色和点击行为
3. 创建一个车对象，该对象要有重量、颜色、牌子、可以载人、拉货和耕田
4. 写一个函数，实现翻转任意数组
5. 写一个函数，实现对数字数组的排序
6. 做一个简易计算器
7. 欢迎使用简易计算器

- 1.加法运算
- 2.减法运算
- 3.乘法
- 4.除法
- 5.退出
- 请输入您的选项
- 请输入一个数值
- 请输入一个数值