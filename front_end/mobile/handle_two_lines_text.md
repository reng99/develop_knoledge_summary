## 省略超出两行的文字

示例代码如下：

```css

.className{
  overflow: hidden;
  text-overflow: ellipsis;
  display: box;
  display: -webkit-box;
  line-clamp: 2;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
}

```
