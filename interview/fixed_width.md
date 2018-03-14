## 实现左侧固定宽度，右边自适应

假设有html的布局如下：

```html
<body>
  <div id="left"></div>
  <div id="right"></div>
</body>
```

> 方法一

结合float飘出文档流并结合margin-left来实现：

```css
div{
  height: 200px;
}
#left{
  float: left;
  width: 200px;
  background: blue;
}
#right{
  margin-left: 200px;
  background: red;
}
```

> 方法二

使用display+flex啦

```css
body{
  display: flex;
  flex-flow: row;
}
div{
  height: 200px;
}
#left{
  width: 200px;
  background: blue;
}
#right{
  flex: 1;
  background: red;
}
```

首先将body的display为flex，让body遵从flex布局，并且设置flex-flow为row，横向的，然后就是左侧div宽度200px，
右侧div的flex:1，这里很关键，1会将剩余宽度全部占满，即如果左侧宽度发生改变的话，右侧能够自适应。

> 方法三

使用position:absolute;和margin-left

```css
		body{
			position: relative;		}
		div{
			height: 200px;
		}
		#left{
			position: absolute;
			left: 0;
			top:0;
			width: 200px;
			background: blue;
		}
		#right{
			margin-left: 200px;
			background: red;
		}
```
