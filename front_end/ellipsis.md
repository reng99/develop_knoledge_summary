## 文本超出部分省略

使用代码示范：


```html

    .
    <p>this is the content</p>
    .

```

需要将上面的文本段落超出`50px`的部分省略...，达到如`this is the ...`的效果

```css

    p{
        width:50px;
        height:20px;
        white-space:nowrap;
        overflow:hidden;
        text-overflow:ellipsis;
    }

```