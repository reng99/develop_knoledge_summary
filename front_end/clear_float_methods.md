## css中清除浮动的方法

### 前言

浮动对页面的影响：

如果一个父盒子中有一个子盒子，并且子盒子没有设置高，子盒子在父盒子中进行浮动，那么将来父盒子的高度为0，由于父盒子的高度为0，下面的元素会自动补位，所以这个时候有必要进行浮动的清除。

原代码

```html

<!DOCTYPE html>
<html>
<head>
	<title>清除浮动的方法</title>
	<style type="text/css">
        .outer{
			background: #999;
		}
		.red{
			width:100px;
			height: 100px;
			background:red;
		}
		.blue{
			width:100px;
			height:100px;
			background: blue;
		}
		.other{
			width:300px;
			height: 30px;
			background:yellow;
		}
	</style>
</head>
<body>
	<div class="outer">
		<div class="red"></div>
		<div class="blue"></div>
	</div>
	<div class="other"></div>
</body>
</html>

```

愿效果：

![origin_clear_float](./imgs/origin_clear_float.png)

为红色和绿色方块添加左浮动后

原代码

```html

<!DOCTYPE html>
<html>
<head>
	<title>清除浮动的方法</title>
	<style type="text/css">
		.outer{
			background: #999;
		}
		.red{
			float: left;
			width:100px;
			height: 100px;
			background:red;
		}
		.blue{
			float: left;
			width:100px;
			height:100px;
			background: blue;
		}
		.other{
			width:300px;
			height: 30px;
			background:yellow;
		}
	</style>
</head>
<body>
	<div class="outer">
		<div class="red"></div>
		<div class="blue"></div>
	</div>
	<div class="other"></div>
</body>
</html>

```

其效果为--

![float_left](./imgs/float_left.png)


### 方法一：使用overflow属性来清除浮动

```bash

.outer{
    overflow:hidden;
}

```

先找到浮动盒子的父元素（盒子），在父元素中田间一个属性`overflow:hidden`，就是清除这个父元素中的子元素浮动对页面的影响。

效果如下：

![after_clear_float_method1](./imgs/after_clear_float_method1.png)


**注意：**一般情况下不会使用这种方式，因为`overfloat:hidden`有一个特点，离开了这个元素所在的区域之后会被隐藏（overflow:hidden会将超出的部分隐藏起来）。


### 方法二：使用额外的标签

这又分两种情况--

情况一：内部标签

```html

	<div class="outer">
		<div class="red"></div>
		<div class="blue"></div>
        <div style="clear:both;"></div>
	</div>
	<div class="other"></div>


```

放在浮动元素的父元素里面，效果如下图：

![after_clear_float_method1](./imgs/after_clear_float_method1.png)

情况二：外部标签

```html

	<div class="outer">
		<div class="red"></div>
		<div class="blue"></div>
        <div style="clear:both;"></div>
	</div>
	<div class="other"></div>


```

放在浮动元素父元素同级位置，最终效果如下：

![after_clear_float_method2](./imgs/after_clear_float_method2.png)

这两种种清除的方式有下面的特点：

1.内部标签：会将这个浮动盒子的父盒子的高度重新撑开

2.外部标签：会将这个浮动盒子的影响清除，但是不会撑开父盒子。

**注意：**一般情况下不会使用这种方式来清除浮动。因为这种清除浮动方式会增加页面的标签，造成机构混乱。


### 方法三：使用伪元素:after

outer利用其伪类`clear:after`在元素内部增加一个类似div.clear的效果。

```html

.outer { /*==for IE6/7 Maxthon2  为了兼容IE==*/
        zoom:1;
    }  
.outer:after{
			content:"."; /*可以取值，也可以为空*/
			clear:both;
			display: block;
			width:0;
			height: 0;
			visibility: hidden;／*visibility:hidden;的作用是允许浏览器渲染它，但是不显示出来*／

　　　　　}

```

这是网上使用比较广泛，拉风的清除方式。

其效果如下：

![after_clear_float_method1](./imgs/after_clear_float_method1.png)

### 使用双伪元素清除浮动

```html

.outer { /*==for IE6/7 Maxthon2  为了兼容IE==*/
        zoom:1;
    }  
.outer:after,.outer:before{
			content:"."; /*取值只能为空*/
			clear:both;
			display: block;
　　　　　}


```

其效果如下：

![after_clear_float_method1](./imgs/after_clear_float_method1.png)


### 总结

第一种方法会将超出部分隐藏，在某些时候我们想清除浮动并且保留超出部分的时候做不到。

第二种方法会增加不必要的标签。

所以我们选择第三种方法来清除浮动。

为什么不选择第四种来清除呢？因为第四种是第三种的改良版，虽然比较简便，但是不够严谨，比如`content`的内容不为空的时候，会出现问题，感兴趣的话可以自行尝试下咯。


### 参考链接

[关于清除浮动的四种方法](http://www.cnblogs.com/qq364735538/p/5997134.html)

[css清除浮动float的三种方法总结](https://my.oschina.net/leipeng/blog/221125)


### 说明

代码和截图是自己自行设计和本机的截图，如果侵权还请邮件我--1837895991@qq.com，我会第一时间进行更正。
