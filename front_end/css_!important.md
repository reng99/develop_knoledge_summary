## !important

> !important 为开发者提供了一个增加样式权重的方法。

⚠️需要注意的是`!important`是对整条样式的声明，包括这个样式的属性和属性值。

```html

<style>
#Box div{
     color:red;
}
.important_false{
     color:blue;
}
important_true{
     color:blue !important;
}
</style>


<div id="Box">
    <div class="important_false">这一行末使用important</div>
    <div class="important_true">这一行使用了important</div>
</div>

```

CSS代码第一行设定了box里面所有div中字体色为红色，第二行和第三行都用class重新定义了自身div的字体色为蓝色，不同的是，第二行末使用important，而第三行使用了！ 
默认情况下，class的优先级小于id，所以，第二行中即使用class重定义了自身样式，也无法生效，所以继承父级属性，这行字还是红色！ 
但是，第三行中，用了important提升优先级（或看成强制重定义），所以这里的css得以生效，这行字变为了蓝色！

**参考**

- [css中!important的用法](http://blog.csdn.net/w617777/article/details/51766420)
