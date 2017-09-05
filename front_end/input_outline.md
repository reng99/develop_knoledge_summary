## input中的outline的使用

### 问题描述

input正常写的时候，如果点击了input的标签，如：<input type="text"/>，会出现方框的外面有默认的高亮。但是在生产环境中，为了页面的简洁大方，一般会将高亮
移除。那么，我们是怎么移除的呢？

### 解决方案

input默认有一个ouline的属性，将outline的属性修改下就可以将默认的高亮移除--`outline:none`
