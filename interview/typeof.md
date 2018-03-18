## 使用 typeof === "object" 判断bar是不是一个对象有什么潜在的弊端？如何避免？

使用`typeof`如下：

```javascript
let obj = {};
let arr = [];

console.log(typeof obj === 'object'); // true
console.log(typeof arr === 'object'); // true
console.log(typeof null === 'object'); // true
```

使用`typeof bar === 'object'`并不能准确判断bar就是一个object，可以通过`Object.prototype.toString.call(bar) == '[object Object]'`来避免这种弊端。

```javascript
Object.prototype.toString.call([]); # [object Array]
Object.prototype.toString.call({}); # [object Object]
Object.prototype.toString.call(); # [object Undefined]
Object.prototype.toString.call(6); # [object Number]
Object.prototype.toString.call('reng'); # [object String]
Object.prototype.toString.call(null); # [object Null]
Object.prototype.toString.call(true); # [object Boolean]
```

另外，不要用`==`代替`===`的使用哦
