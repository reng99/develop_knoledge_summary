## 清除IE10+下input的叉叉（X）和密码输入框的眼睛图标

从IE 10开始，type=”text” 的 input 在用户输入内容后，会自动产生一个小叉叉（X），方便用户点击清除已经输入的文本.

```bash

 _______________
|	      x |
 ———————————————

```


对于type=”password”的 input 则会在右方显示一个小眼睛的图标，占击这个图标可以显示已经输入的内容。

大多数情况下，为了和其他浏览器呈现相同的效果，需要将input文本输入框右方的X给去掉，将密码输入框右边的小眼睛也给去掉。

只要使用以下CSS代码可轻松实现隐藏IE浏览器自带的文本删除按钮和密码查看按钮。

```css 

input::-ms-clear,input::-ms-reveal{
	display:none;
}

```

`input::-ms-clear`是清除文本中的删除icon

`input::-ms-reveal`是清除密码的眼睛icon

这里就不给出截图了，可以自行建一个demo尝试下哦。


### 参考链接

[清除IE10下input的叉叉（X）和密码输入框的眼睛图标](http://blog.csdn.net/web_qdkf/article/details/50039899)
