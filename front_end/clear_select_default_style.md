## 清除 select 的默认的样式

**清除下拉的箭头**

```css

  appearance:none;
  -moz-appearance:none;
  -webkit-appearance:none;

```

这个清除的样式对ie无效，即使加上`-ms-appearance:none;`

要对IE做兼容的话，需要加上`select::-ms-expand { display: none; }  `来清除ie默认的下拉的箭头样式。


**清除mac浏览器上的圆角**

在mac上浏览器默认的select是带有圆角的，所以在公共的样式的前面需要添加下面的代码来清除这种默认的样式。

```css

  select{
  
    border-radius:0;
    -webkit-border-radius:0;
    -moz-border-radius:0;
    -khtml-border-radius:0;
    
  }

```

如果添加上面的css还是不行的话，就需要多添加一条样式

```css

  select{
  
    -webkit-appearance:button;
  
  }

```

[参考-->苹果电脑如何去除select的圆角](http://blog.csdn.net/jerry_xiaobin/article/details/52609565)
