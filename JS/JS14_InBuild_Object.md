【内置对象】

# 内置对象的定义

对象分类：
- 自定义对象
- 内置对象
- 浏览器对象

前两个对象是JS基础内容，属于ECMAScript，第三个‘浏览器对象’是JS独有的，到 JS API 再讲解

内置对象
- JS语言自带的对象，供开发者使用，
- 提供一些基本而必要的功能（属性和方法）
- 帮助快速开发
- 多个内置对象：如Math, Date, Array, String等

# 查阅文档

- MDN: https://developer.mozilla.org/zh-CN/
- W3C

步骤：
- 查询该方法的功能
- 查看参数的意义和类型
- 查看返回值的意义和类型
- demo测试

# Math对象

不是构造函数，所以不需要new来调用，而是直接调用属性或方法

```html
<script>
	console.log(Math.PI);  //圆周率属性
	console.log(Math.max(1, 99, 3));  //99
	console.log(Math.max(1, 99, 'pink'));  //NaN
	console.log(Math.max); //-Infinity

</script>
```

## 封装自己的数学对象

封装自己的数学对象，里面有PI、求最大值、求最小值

```html
<script>
	var myMath = {
		PI: 3.14159265357,
		max: function () {
			var max = arguments[0];
			for (var i = 1; i < arguments.length; i++) {
				if (arguments[i] > max) {
					max = arguments[i];
				}
			}
			return max;
		},

		min: function () {
			var min = arguments[0];
			for (var i = 1; i < arguments.length; i++) {
				if (arguments[i] < min) {
					min = arguments[i];
				}
			}
			return min;
		}
	}

	console.log(myMath.PI);
	console.log(myMath.max(1, 2, 3));
	console.log(myMath.min(1, 2, 3));
</script>
```

## Math取绝对值方法

```html
<script>
	// 绝对值
	console.log(Math.abs(-1)); //1
	console.log(Math.abs('-1'));  //隐式转换 会把字符串转换为数字型
	console.log(Math.abs('pink')); //无法转换 NaN
</script>
```

## Math三个取整方法

```html
<script>
	//取整
	Math.floor();   // 向下取整
	Math.ceil();    // 向上取整
	Math.round();   // 四舍五入，就近取整，注意 -3.5 取整为 -3
	// 四舍五入时，.5比较特殊，往大了取

	console.log(Math.floor(1.1)); // 1
	console.log(Math.floor(1.9)); // 1

	console.log(Math.ceil(1.1)); // 2
	console.log(Math.ceil(1.9)); // 2

	console.log(Math.round(1.1)); // 1
	console.log(Math.round(1.9)); // 2

	console.log(Math.round(-1.1)); // -1
	console.log(Math.round(-1.5)); // -1  !!!

</script>
```

## Math 随机数方法

```html
<script>
	// Math.random() 随机返回一个小数 [0,1)
	// 该方法不跟参数

	console.log(Math.random());

	//两个数之间的随机整数，并且包含这两个整数

	function getRandom(min, max) {
		return Math.floor(Math.random() * (max - min + 1)) + min;
	}
	console.log(getRamdom(1, 10));

	// 随机点名
	var arr = ['jake', 'jakee', 'jakeee', 'rose', 'rosee'];
	console.log(arr[getRandom(0, arr.length - 1)]);

</script>
```

## 猜数字游戏

程序随机生成一个1-10之间的数字，并让用户输入一个数字：
如果大于该数字，提示数字大了，继续猜；
如果小于该数字，提示数字小了，继续猜；
如果等于该数字，提示猜对了，结束程序；

```html
<script>
	function getRandom(min, max) {
		return Math.floor(Math.random() * (max - min + 1)) + min;
	}
	var randomNum = getRandom(1, 10);

	while (true) {
		//注意这里用while更好，for也行，但是需要多加两个分号
		var inputNum = prompt('猜猜我脑袋里想的一个什么数字呢？1~10之间哦！');

		if (randomNum > inputNum) {
			alert('猜小了，继续猜');
		}
		else if (randomNum < inputNum) {
			alert('猜大了，继续猜');
		}
		else {
			alert('恭喜你，猜对了');
			break;  //退出整个循环程序
		}
	}

</script>
```


作业：猜1-50之间的数字，但是只有10次机会



# 日期对象

```html
<script>
	// Date() 日期对象，是一个构造函数，必须使用new 来调用
	var arr = new Array(); //创建一个数组对象
	var obj = new Object();  //创建了一个对象实例

	// 使用Date() 必须加new
	// 获取当前时间必须实例化
	var date = new Date();   // 如果没有参数，返回当前系统的当前时间
	console.log(date);

	// Date()构造函数的参数，常用的写法：
	// 数字型 2019,10,01 
	// 或者字符串型的 '2019-10-1 8:8:8'
	var date1 = new Date(2019, 10, 1);
	console.log(date1);  //返回的是11月

	var date2 = new Date('2019-10-1 8:8:8');
	console.log(date2);

</script>
```

## 格式化日期年月日星期

日期格式化

以下均为方法

- getFullYear() => dObj.getFullYear()
- getMonth() 获取当月 0-11
- getDate() 获取日期
- getDay() 获取周几，周日为0，周六为6
- getHours()
- getMinutes()
- getSeconds()

```html
<script>
	var date = new Date();
	console.log(date.getFullYear()); // 获得年份
	console.log(date.getMonth() + 1);  // 获得月份，返回的月份小一个月
	console.log(date.getDate());  // 获得日期
	console.log(date.getDay());  //周日为0，周六为6

	//按这个格式写 2019年 5月 1日 星期三
	var year = date.getFullYear();
	var month = date.getMonth() + 1;
	var dates = date.getDate();
	var arr = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
	var day = date.getDay();

	console.log('今天是： ' + year + '年' + month + '月' + dates + '日 ' + arr[day]);

	//重点是使用数组，改写为中文数字的星期几，即arr的索引为day的数组元素




	var time = new Date();
	// 封装一个函数返回当前的时分秒，格式为00:00:00
	function getTime() {
		var h = time.getHours();
		var m = time.getMinutes();
		var s = time.getSeconds();

		h = h < 10 ? '0' + h : h;
		m = m < 10 ? '0' + m : m;
		s = s < 10 ? '0' + s : s;

		return h + ':' + m + ':' + s;
	}
	console.log(getTime());

	console.log(getTime());

</script>
```

## Date()获取总的毫秒数

获取日期的总的毫秒数

所有程序的的起始时间：1970-01-01

不是当前时间的毫秒数，而是距离1970-01-01过了多久

```html
<script>
	// 1.通过 valueOf()  getTime()

	var date = new Date();
	console.log(date.valueOf());
	console.log(date.getTime());

	// 2.简单的写法，更常用

	var date1 = +new Date();  //+new Date() 返回的就是总的毫秒数
	console.log(date1);

	// 3.H5新增的 获得新的毫秒数

	console.log(Date.now());    // 低版本浏览器可能不认


	// 毫秒数永远不会重复，独一无二的，我们称之为“时间戳”
</script>
```


## 倒计时案例

```html
<script>
	// 核心算法：输入的时间减去现在的时间
	// 用时间戳来做
	// 时间戳与天时分秒的转换
	// d = parseInt(totalTimeinSeconds / 60 / 60 / 24); 计算天数
	// h = parseInt(totalTimeinSeconds / 60 / 60 % 24); 计算小时数
	// m = parseInt(totalTimeinSeconds / 60 % 60); 计算分钟数
	// s = parseInt(totalTimeinSeconds % 60); 计算秒数

	function countDown(time) {
		var nowTime = +new Date();
		var inputTime = +new Date(time);
		var times = (inputTime - nowTime) / 1000;

		d = parseInt(times / 60 / 60 / 24);
		h = parseInt(times / 60 / 60 % 24);
		m = parseInt(times / 60 % 60);
		s = parseInt(times % 60);

		d = d < 10 ? '0' + d : d;
		h = h < 10 ? '0' + h : h;
		m = m < 10 ? '0' + m : m;
		s = s < 10 ? '0' + s : s;

		return '剩余时间：' + d + 'd ' + h + ':' + m + ':' + s;

	}

	console.log(countDown('2021-05-06 00:00:00'));

</script>
```


# 数组对象

数组的创建

```html
<script>
	// 1. 字面量创建
	var arr = [1, 2, 3];
	console.log(arr[0]);

	// 2. 利用 new Array();
	// var arr1 = new Array();  
	//利用Array()函数进行实例化，创建新数组

	// var arr1 = new Array(2);  
	//表示创建一个空数组，长度为2，有2个空的数组元素

	var arr1 = new Array(2, 3);
	//等价于用字面量创建2个数组元素，分别为2和3
	console.log(arr1);
</script>
```

## 检测输入的参数是否为数组

```html
<script>
	// 1. instanceof 运算符，用来检测是否为数组
	var arr = [];
	console.log(arr instanceof Array);  //true

	var obj = {};
	console.log(obj instanceof Array); //false

	// 2. Array.isArray(参数) 方法，为H5新增的方法 ie9以上才支持
	console.log(Array.isArray(arr));  // true
	console.log(Array.isArray(obj));  // false

	// !!!检测是否为数组，可以用于函数传参时确保传入的参数为数组类型

	// 之前的reverse() 数组翻转函数可以在传参后加入一个数组判断

</script>
```

## 添加或删除数组元素

```html
<script>
	// 提供了4种添加或删除元素的方法
	// push()后加  unshift()前加
	// pop()后删  shift()前删


	// push() 末尾添加一个或多个元素，返回新的长度

	var arr = [1, 2, 3]
	arr.push(4);
	console.log(arr);   // [1,2,3,4]

	arr.push(4, 'pink');
	console.log(arr);    // [1,2,3,4,'pink']

	// push 可以在数组末尾追加新的数组元素
	// push() 参数直接写，数组元素
	// 返回值为 新数组长度
	// 原数组发生变化

	// unshift() 数组开头添加一个或多个元素，返回新的长度

	arr.unshift('red', 'purple');
	console.log(arr);    // ['red','purple',1,2,3,4,'pink']



	// pop() 删除数组最后一个元素，数组长度-1，返回删除的元素的值

	arr.pop();  // 无参数
	console.log(arr); // ['red','purple',1,2,3,4]
	console.log(arr.pop());  //返回值为删除的元素 

	// shift() 删除数组的第一个元素，数组长度-1，返回第一个元素的值

	arr.shift();  // 无参数
	console.log(arr); // ['purple',1,2,3,4]
	console.log(arr.shift());  //返回值为删除的元素 

</script>
```


## 筛选数组

工资数组 [1500,1200,2000,2100,1800]，要求工资超过2000的删除，剩余的放到新数组里

```html
<script>
	var arr = [1500, 1200, 2000, 2100, 1800];
	var newArr = [];
	for (var i = 0; i < arrlength; i++) {
		if (arr[i] < 2000) {
			// newArr[newArr.length] = arr[i];
			newArr.push(arr[i]);    //小于2000的追加，push()更简单
		}
	}
	console.log(newArr);
</script>
```


## 数组排序

数组方法

### reverse() 
颠倒数组中元素的顺序，无参数，该方法会改变原有数组，返回新数组

### sort() 
对数组的元素进行排序，该方法会改变原有数组，返回新数组

```html
<script>
	// 翻转数组
	var arr = ['blue', 'red', 'pink'];
	arr.reverse();
	console.log(arr);

	// 数组排序，冒泡排序
	var arr1 = [3, 4, 7, 1];
	arr1.sort();
	console.log(arr1);

	//sort()只能对个位排序，以下办法可以解决这个问题
	var arr1 = [13, 4, 77, 17, 7];
	arr1.sort(function (a, b) {
		return a - b; //升序排列
		// return b - a; //降序排列
	});
	console.log(arr1);

</script>
```

## 数组索引方法

### indexOf() 
数组中查找给定元素的第一个索引，如果存在，返回索引号，如果不存在，返回-1

### lastIndexOf() 
从后往前查找索引，如果存在，返回索引号，如果不存在，返回-1

```html
<script>
	var arr = ['red', 'green', 'blue', 'pink', 'blue'];
	console.log(arr.indexOf('blue'));   // 2
	// 如果有多个blue, 只返回第一个满足条件的索引号
	// 如果没有blue, 返回-1

	console.log(arr.lastIndexOf('blue'));  // 4
</script>
```

## 数组去重案例（重点）

要求去除数组中重复的元素 ['x','a','z','a','x','a','x','c','b']



```html
<script>

	// 核心算法：遍历旧数组，拿旧数组去查询新数组，如果该元素在新数组中不存在，就添加，否则不添加

	// 如何知道该元素是否存在于新数组中？利用indexOf()方法，如果返回-1，就说明没有该元素

	// 封装一个去重函数

	function unique(arr) {
		var newArr = [];
		for (var i = 0; i < arr.length; i++) {
			if (newArr.indexOf(arr[i]) === -1) {
				newArr.push(arr[i]);
			}
		}
		return newArr;
	}

	var demo = unique(arr = ['x', 'a', 'z', 'a', 'x', 'a', 'x', 'c', 'b']);

	console.log(demo);
</script>
```


## 数组转换为字符串方法

### toString() 
把数组转换成字符串，逗号分隔每一项，返回一个字符串

### join('delimiter') 
把数组中的所有元素转换为一个字符串，返回一个字符串

```html
<script>
	// toString()
	var arr = [1, 2, 3]
	console.log(arr.toString()); //1,2,3

	//join() 里面可以跟分隔符
	var arr1 = ['green', 'blue', 'pink'];
	console.log(arr1.join('-')); // green-blue-pink
	console.log(arr1.join('&')); // green&blue&pink
</script>
```

作业：查询以下方法

concat() 连接两个或多个数组，返回一个新的数组

slice() 数组截取slice(begin,end) 返回被截取项目的新数组

splice() 数组删除splice(begin, deleteNumbers) 返回被删除项目的新数组，会影响原数组

重点看下splice()


# 字符串对象

## 基本包装类型

为了方便操作基本数据类型，JS提供了三个特殊的引用类型String，Number,Boolean

基本包装类型就是把简单数据类型包装成为复杂数据类型，这样基本数据类型就有了属性和方法

一句话总结：系统自动将其提升为了对象，专业术语叫“**基本包装类型**”

```html
<script>
	var str = 'Andy';
	console.log(str.length);  // 4

	// 执行过程如下

	// 1.生成临时变量，把简单数据类型包装为复杂数据类型
	var temp = new String('Andy');

	// 2.赋值给声明的字符变量
	str = temp;

	// 销毁临时变量
	temp = null;

</script>
```


## 字符串不可变

字符串里面的值不可变，虽然看上去可以改变内容，其实是地址变了，内存中新开辟了一个内存空间

```html
<script>
	var str = 'andy';
	console.log(str);  //andy

	str = 'red';
	console.log(str);  //red 看似字符串变了，其实开辟了一块新的内存空间

	var str = '';
	for (var i = 1; i <= 100; i++) {
		str += i;    // 疯狂加字符串，电脑容易卡死，不建议尝试
	}
	console.log(str);

</script>
```

## 根据字符返回位置

字符串所有的方法，都不会修改字符串本身，操作完成会返回一个新的字符串

### indexOf() 
返回指定内容在元字符串中的位置，如果找不到就返回-1，开始的位置是index索引号

### lastIndexOf() 
从后往前找，只找第一个匹配的

```html
<script>
	// str.indexOf('要查找的字符',[起始的位置])

	var str = '改革春风吹满地，春天来了';
	console.log(str.indexOf('春'));  //2
	console.log(str.indexOf('春', 3));  //8

	// lastIndexOf() 同理

</script>
```

## 案例：返回字符位置

查找字符串'abcoefoxyozzopp'中所有o出现的位置以及次数

```html
<script>
	var str = 'abcoefoxyozzopp';
	var index = str.indexOf('o');
	var num = 0;

	while (index !== -1) {
		console.log(index);
		num++;
		str.indexOf('o', index + 1);
	}
	console.log('o出现的次数是：' + num);
</script>
```

作业：
求数组['red','blue','red','green','pink','red']中red出现的位置和次数



## 根据位置返回字符（重点）

### charAt(index) 
返回指定位置的字符，str.charAt(0)

### charCodeAt(index) 
获取指定位置处字符的ASCII码，str.charCodeAt(0)

### str[index]
获取指定位置处字符，H5，IE8+支持，和charAt()等效

```html
<script>

	// charAt()
	var str = 'Andy';
	console.log(str.charAt(3)); // y

	// 遍历所有字符
	for (var i = 0; i < str.length; i++) {
		console.log(str.charAt(i));
	}

	// charCodeAt() 用于判断用户的按键
	console.log(str.charCodeAt(0));  // 97, 对应字母a

	// str[] H5新增的
	console.log(str[0]); // a 

</script>
```

## 统计出现次数最多的字符

```html
<script>
	// 判断对象是否有某一属性
	var o = {
		age: 18
	}

	if (o['age']) {
		console.log('the attribute exists');
	} else {
		console.log('the attribute does not exist');
	}
</script>
```



```html
<script>
	// 判断一个字符串'abcoefoxyozzopp'中出现次数最多的字符，并统计次数

	// 核心算法：用charAt()遍历整个字符串
	// 把每个字符都存储为对象，如果对象没有该属性，就为1，如果存在就+1
	// 遍历对象，得到最大值和该字符

	var str = 'abcoefoxyozzopp';
	var o = {};
	for (var i = 0; i < str.length; i++) {
		var chars = str.charAt(i);
		if (o[chars]) {
			o[chars]++;
		} else {
			o[chars] = 1;
		}
	}
	console.log(o);

	// 遍历对象
	var max = 0;
	var ch = '';
	for (var k in o) {
		if (o[k] > max) {
			max = o[k];
			ch = k;
		}
	}
	console.log(max);
	console.log('最多的字符是：' + ch);

</script>
```


## 字符串的操作方法（重点）

### concat(str1,str2,str3,...) 
用于连接两个或多个字符串，拼接字符串，等效于+，+更常用

### substr(start,length) 
从start位置开始，取length个字符

### slice(start,end) 
从start位置开始，截取到end的位置，end取不到

### substring(start,end) 
从start位置开始，截取到end的位置，end取不到，基本和slice()相同，但是不接受负值

```html
<script>
	// 字符串操作

	// concat()
	var str = 'andy';
	console.log(str.concat('red')); //andyred

	// substr(start,length)
	var str1 = '改革春风吹满地';
	console.log(str1.substr(2, 2));  //春风

</script>
```

## 替换字符串

### replace('source char','target char')

```html
<script>

	// replace()
	var str = 'andyandy';
	console.log(str.replace('a', 'b'));  //bndyandy，只会替换第一个字符

	// 把字符串中'abcoefoxyozzopp'所有的o替换为*，利用循环

	var str1 = 'abcoefoxyozzopp';
	while (str1.indexOf('o') !== -1) {
		str1 = str1.replace('o', '*');
	}
	console.log(str1); //abc*ef*xy*zz*pp

	// 可以用于过滤敏感词

</script>
```


## 字符串转换为数组

### split('delimiter')

```html
<script>
	// 字符串=>数组 split('delimiter')
	// 联想到 数组=>字符串 join('delimiter')

	var str2 = 'red, pink, blue';
	console.log(str2.split(', '));

	var str3 = 'red&pink&blue';
	console.log(str3.split('&'));

</script>
```

作业：

1.查阅以下方法

toUpperCase() // 转换大写
toLowerCase() // 转换小写

2.给定一个字符串
abaasdffggghhjjkkgfddsssss3444343

问题如下

- 字符串的长度
- 取出指定位置的字符，如：0，3，5，9等
- 查找指定字符是否在以上字符串中存在，如：i, c, b等
- 替代指定的字符，如：g替换为22，ss替换为b等操作
- 截取指定开始位置到结束位置的字符串，如：取得1-5的字符串
- 找出以上字符串中出现次数最多的字符和出现的次数