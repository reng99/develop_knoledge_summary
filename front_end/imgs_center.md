## css图片居中（水平居中和垂直居中）

css图片居中分为图片的`水平居中`和`垂直居中`两种情况，有时候还需要图片同时水平垂直居中，下面分几种情况介绍下：

**图片水平居中**

> 利用margin:0 auto实现图片水平居中

利用`margin:0 auto;`实现图片水平居中就是在图片上加上样式margin:0 auto;如下：

```html

  <div style="width:800px;min-height:500px;border:1px solid #e5e5e5;">
    <img alt="" src="path/to/img"/ style="margin:0 auto;">
  </div>

```

然而，你像上面的这段代码运行的话，得不到图片水平居中的效果。因为`<img/>`标签是行内元素。`margin:0 auto;`这种居中的方式不起效果，需要将`<img/>`元素
设为块级元素。改写上面的代码如下即可（添加一个"display:block;"样式）：


```html

  <div style="width:800px;min-height:500px;border:1px solid #e5e5e5;">
    <img alt="" src="path/to/img"/ style="display:block;margin:0 auto;"> <!--注意⚠️设置成display:inline;或者display:inine-block;是没有效果的-->
  </div>

```

> 利用父级标签中text-align:center实现图片水平居中

实现的代码如下所示：

```html

  <div style="width:800px;min-height:500px;border:1px solid #e5e5e5;">
    <img alt="" src="path/to/img"/>
  </div>

```


**图片的垂直居中**

> 利用行高line-height实现图片的垂直居中

这种方法的使用前提是：你要知道图片父框的高度才可以的。例如：

```html

  <div style="width:800px;height:500px;line-height:500px;border:1px solid #e5e5e5;">
    <img alt="" src="path/to/img"/>
  </div>

```

> 利用table实现图片垂直居中

利用`table`的方法是利用了`table的垂直居中属性`，代码如下：

```html

  <div style="width:800px;height:500px;display:table;border:1px solid #e5e5e5;">
    <span style="display:table-cell;vertical:middle">
      <img alt="" src="path/to/img"/>
    </span>
  </div>

```

这里是使用`display:table;display:table-cell;`来模拟table，这种方法并不兼容ie6/ie7,ie67不支持display:table,如果不需要支持ie67那就可以用。

⚠️缺点：当你设置`display:table;`可能会改变你的原有布局。

> 利用绝对定位实现图片的垂直居中

如果已经知道图片的宽度和高度就可以使用这种方法，示例的代码如下：

```html

  <div style="width:800px;height:500px;position:relative;border:1px solid #e5e5e5;"> <!--要在父元素设置position:relative;-->
    <img alt="" src="path/to/img" style="width:100px;height:80px;position:absolute;left:50%;top:50%;margin:-40px 0 0 -50px;"/>
  </div>

```

> 移动端可以使用flex来实现（这里不做介绍，感兴趣可以自行百度呢）


那么，同时实现图片的水平和垂直居中，将上面水平居中和垂直居中的方法结合起来就ok啦。

### 参考

[css图片居中(水平居中和垂直居中)](http://www.51xuediannao.com/html+css/htmlcssjq/css_img_center.html)


















