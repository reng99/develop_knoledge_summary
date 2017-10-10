## input的自定义属性

在实际的开发中，需要使用Input的自定义的属性，那么原生的javascript是如何获取这自定义属性的值的呢？

```html

<input custom='custom name' type='text' name='reng' id='test'/>
// custom是自定的Input的属性，其他的是原生的Input属性

```

我们用点 `.` 来获取这自定的属性值行不通，而用点 '.' 来获取自定义属性的值行得通。

```javascript

var _test = document.getElementById('test');



console.log(_test.custom); // undefined

console.log(_test['custom']); // undefined

console.log(_text.getAttribute('custom')); // custom name




console.log(_test.name); // reng

console.log(_test['name']); // reng

console.log(_test.getAttribute('name')); // reng

```

由上面的代码可以知道`你可以自己进行尝试`,非标准的Input属性要使用`obj.getAttribute('custom')`的方式进行调用，而原生的Input属性就比较灵活。
