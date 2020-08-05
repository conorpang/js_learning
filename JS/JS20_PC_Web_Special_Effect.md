【PC网页特效】

- [元素偏移量 offset 系列](#元素偏移量-offset-系列)
- [元素可视区 client 系列](#元素可视区-client-系列)
- [元素滚动 scroll 系列](#元素滚动-scroll-系列)
- [动画函数封装](#动画函数封装)
- [常见网页特效案例](#常见网页特效案例)

# 元素偏移量 offset 系列

offset即偏移量，使用offset相关属性可以**动态**的得到该元素的位置（偏移）、大小等信息
- 获得元素距离带有定位父元素的位置
- 获得元素自身的大小（宽度高度）
- 返回的数值都**没有单位**

offset常用属性
- `element.offsetParent` 返回该元素带有定位的父元素，如果父元素没有定位返回body
- `element.offsetTop` 返回该元素相对定位父元素上方的偏移
- `element.offsetLeft` 返回该元素相对定位父元素左边框的偏移
- `element.offsetWidth` 返回自身包括padding, border, 内容区的宽度，无单位
- `element.offsetHeight` 返回自身包括padding, border, 内容区的高度，无单位

```html
<style>
	.father {
		position: relative;
		width: 200px;
		height: 200px;
		background-color: pink;
		margin: 100px;
	}

	.son {
		width: 100px;
		height: 100px;
		background-color: purple;
		margin-left: 45px;
	}
</style>
	
<div class="father">
	<div class="son"></div>
</div>

<script>
	var father = document.querySelector('.father');
	console.log(father.offsetTop);//100
	console.log(father.offsetLeft); //100

	var son = document.querySelector('.son');

	// 以带有定位的父元素为准，否则以body为准
	// 父元素是否有定位看css中的position
	console.log(son.offsetTop); //0
	console.log(son.offsetLeft); //45
</script>
```
P98.over
https://www.bilibili.com/video/BV1k4411w7sV?p=99

# 元素可视区 client 系列

# 元素滚动 scroll 系列
# 动画函数封装
# 常见网页特效案例