【函数】

- [函数定义](#函数定义)
- [函数使用](#函数使用)
	- [求1-100的累加和](#求1-100的累加和)
- [函数的参数](#函数的参数)
	- [函数形参和实参的匹配问题](#函数形参和实参的匹配问题)
- [函数的返回值return](#函数的返回值return)
	- [利用函数求任意两个数的最大值](#利用函数求任意两个数的最大值)
	- [利用函数求任意一个数组中的最大值](#利用函数求任意一个数组中的最大值)
	- [return终止函数只能返回一个值](#return终止函数只能返回一个值)
	- [函数没有return返回的是undefined](#函数没有return返回的是undefined)
	- [break, continue, return的区别](#break-continue-return的区别)
	- [通过榨汁机看透函数](#通过榨汁机看透函数)
- [arguments的使用](#arguments的使用)
	- [利用函数求任意个数的最大值](#利用函数求任意个数的最大值)
- [函数案例](#函数案例)
	- [利用函数翻转数组](#利用函数翻转数组)
	- [函数封装冒泡排序](#函数封装冒泡排序)
	- [利用函数判断闰年](#利用函数判断闰年)
- [函数可以调用另一个函数](#函数可以调用另一个函数)
	- [输出2月份天数](#输出2月份天数)
- [函数的两种声明方式](#函数的两种声明方式)


# 函数定义

封装了一段可以被重复执行调用的代码块，目的就是让大量代码重复使用

```html
<script>
	function getSum(num1, num2) {
		var sum = 0;
		for (var i = num1; i <= num2; i++) {
			sum += i;
		}
		console.log(sum)
	}
	getSum(1, 100);
	get(10, 50);
<script>
```


# 函数使用

两步：声明函数、调用函数

```html
<script>
	// 声明函数
	function sayHi() {
		// function 小写
		// 函数名，一般是动词
		// 函数不调用自己不执行
		console.log('hi');
	}

	// 调用函数
	// 函数名()
	sayHi();
<script>
```

函数的封装（打包）：通过函数封装起来，对外只提供一个简单的函数接口

## 求1-100的累加和

```html
<script>
	function getSum() {
		var sum = 0;
		for (var i = 1; i <= 100; i++) {
			sum += 1;
		}
		console.log(sum);
	}

	getSum();
<script>
```

# 函数的参数

形参和实参
```html
<script>
	function 函数名(形参1, 形参2, 实参n) {   //声明函数的小括号里面用形参

	}
	函数名(实参1, 实参2, 实参n)  //函数调用的小括号里面用实参


	//形参是接受实参的，相当于一个变量，无需声明
	//函数的参数，个数不限，可以没有
<script>
```


```html
<script>
	//利用函数求任意两个数的和
	function getSum(num1, num2) {
		console.log(num1 + num2);
	}
	getSum(3, 8);
<script>
```

```html
<script>
	//利用函数求任意两个数之间的和
	function getSums(start, end) {
		var sum = 0;
		for (var i = start; i <= end; i++) {
			sum += i;
		}
		console.log(sum);
	}
	getSum(3, 8);
<script>
```

注意：
1. 多个参数之间用逗号隔开
2. 形参可以看做无需声明的变量




## 函数形参和实参的匹配问题
```html
<script>

	function getSum(num1, num2) {
		console.log(num1, num2);
	}

	// 1.如果实参的个数和形参的个数一致，则正常输入结果
	getSum(1, 2); //3
	// 2.如果实参的个数 多于 形参的个数，会取到形参的个数
	getSum(1, 2, 3); //3
	// 3.如果实参的个数 小于 形参的个数
	// 形参可以看做不用声明的变量，没有接收值的话，进行运算会显示为NaN(not a number)
	getSum(1); //NaN

//建议：尽量让实参的个数和形参相匹配
<script>
```

# 函数的返回值return

希望函数将值返回给调用者，可用return语句实现

```html
<script>
	function 函数名() {
		return 需要返回的结果;

	}

	// 函数只实现某种功能，最终的结果需要返回给函数的调用者函数名，通过return实现
	// 只要函数遇到return，就把后面的结果返回给函数的调用者
<script>
```

代码验证

```html
<script>
	function getResult() {
		return 666;
	}
	getResult(); // getResult() = 666
	console.log(getResult());
<script>
```


```html
<script>
	//用return语句重写：利用函数求任意两个数的和
	function getSum(num1, num2) {
		return num1 + num2;

	}
	console.log(getSum(1, 2));
<script>
```

## 利用函数求任意两个数的最大值

```html
<script>
	function getMax(num1, num2) {
		if (num1 > num2) {
			return num1;
		} else {
			return num2;
		}

		// 或者用三元运算符
		// return num1 > num2 ? num1 : num12;
	}
	console.log(getMax(1, 3));

<script>
```

## 利用函数求任意一个数组中的最大值

求数组 [5,2,99,101,67,77] 中的最大值

```html
<script>
	function getArrMax(arr) {
		var max = arr[0];
		for (var i = 1; i < arr.length; i++) {
			if (arr[i] > max) {                    //注意这行的比较算法，是比较当前数和最大值，而不是当前数和后一个数
				max = arr[i];
			}
		}
		return max;
	}
	//实际开发中，常用一个变量来接受函数的返回结果
	var re = getArrMax([5, 2, 99, 101, 67, 77]);  //实参是一个数组
	console.log(re);
<script>
```


## return终止函数只能返回一个值

```html
<script>

	// return终止函数，之后的程序都不会执行

	function getSum(num1, num2) {
		return num1 + num2;
		alert('will not be executed') // 这句话不会被执行
	}
	console.log(getSum(1, 2))

	// return只能返回一个值，多个值以最后一个值为准

	function fn(num1, num2) {
		return num1, num2;
	}
	console.log(fn(1, 2)) // 只会输出2


	// *多个值可以用数组返回
	function getResult(num1, num2) {
		return [num1, num2];
	}
	var re = getResult(1, 2);
	console.log(re);

<script>
```

## 函数没有return返回的是undefined

```html
<script>
	// 函数有return，则返回return后面的值
	// 没有return，则返回undefined

	function fun2() {

	}
	console.log(fun2());  //返回undefined

<script>
```


## break, continue, return的区别

- break - 结束当前循环体，比如for, while
- continue - 跳出本次循环，继续执行下次循环，比如for, while
- return - 不仅可以退出循环，还能够返回return语句中的值，同时还可以结束当前函数体内的代码

## 通过榨汁机看透函数

实现某种功能：输入 => 内部处理 => 输出

作业：
- 1.输入任意两个数字的任意算数运算，弹出运算后的结果
- 2.输入任意两个数字的最大值，弹出运算后的结果
- 3.输入三个不同数字的最大值，弹出运算后的结果
- 4.输入一个数判断是否是质数，弹出返回值

# arguments的使用

```html
<script>

	// 不确定有多少参数传递时，可以用arguments获取，是函数中的内置对象，存储了传递的所有实参

	// arguments 伪数组 并不是真正意义上的数组
	// 1.具有数组的length属性
	// 2.按照索引的方式进行存储的
	// 3.没有真正数组的一些方法 pop() push() 等

	function fn() {
		console.log(arguments); //arguments中存储了所有传递来的实参
		console.log(arguments.length);
		console.log(arguments[2]);

		// 可以按照数组的方式遍历arguments
		for (var i = 0; i < arguments.length; i++) {
			console.log(arguments[i]);
		}
	}
	fn(1, 2, 3);
	fn(1, 2, 3, 4, 5);
<script>
```

## 利用函数求任意个数的最大值

```html
<script>
	function getMax() {
		var max = arguments[0];
		for (var i = 0; i < arguments.length; i++) {
			if (arguments[i] > max) {
				max = arguments[i];
			}
		}
		return max;
	}
	var re = getMax(1, 5, 6);
	console.log(re);
<script>
```

# 函数案例

## 利用函数翻转数组

```html
<script>
	function reverseArr(arr) {
		var newArr = []; //注意声明数组的写法，需要复习
		for (var i = 0; i < arr.length; i++) {
			newArr[newArr.length] = arr[arr.length - i - 1];   //注意新数组的索引号问题！
		}
		return newArr;


		// 遍历的程序也可以这样写 by Pink
		// for (var i = arr.length - 1; i >= 0; i--) {
		// 	newArr[newArr.length]  = arr[i];
		// }

	}
	var arr = [1, 2, 3, 4, 5];
	var re = reverseArr(arr);
	console.log(re);

<script>
```


## 函数封装冒泡排序

```html
<script>

<script>
```


## 利用函数判断闰年

```html
<script>

<script>
```


# 函数可以调用另一个函数

```html
<script>

	// 函数可以相互调用

	function fn1() {
		console.log(111);
		fn2();  // 这里调用了fn2()函数
		console.log('fn1');
	}
	function fn2() {
		console.log(222);
		console.log('fn2');
	}
<script>
```

## 输出2月份天数

输入年份，输出当前年份2月份的天数

```html
<script>

	//输入年份，输出当前年份2月份的天数
	function febDays() {
		var year = prompt('请输入年份：')
		if (isLeapYear(year)) {
			alert('当前年份是闰年，2月有29天');
		} else {
			alert('当前年份是平年，2月有28天');
		}
	}

	febDays();

	//判断是否为闰年的函数
	function isLeapYear(year) {
		//是闰年返回true, 不是闰年返回false
		var leap = false;
		if (year % 4 == 0 && year % 100 != 0 || year % 400 == 0) {
			leap = true;
		}
		return leap;
	}
<script>
```


# 函数的两种声明方式

```html
<script>
	// 1.利用函数关键字自定义函数(命名函数)
	function fn() {

	}

	// 2.函数表达式，类似变量的声明方式
	var 变量名 = function () { };

	// 举个例子看看怎么用
	var fun = function () {
		console.log('expressions');
	}
	fun();
	// 这个函数没有名字，也称为匿名函数，fun是变量名
	// 调用时用变量名调用
	// 匿名函数也可以传递参数

<script>
```