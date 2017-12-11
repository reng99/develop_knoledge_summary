## js正则验证邮箱格式

邮箱一般长酱紫***@**.**,比如自己的qq邮箱`1837895991@qq.com`

这里的正则匹配的规则考虑到`@`前面是任意的字符`@`后`.`前面是a-z | A-Z | 0-9还包括.和- ,在`.`后是a-z | A-Z | 0-9

```bash
/**
* 检查字符串是否为合法的邮件email地址
* @param {String} 字符串
* @return {Boolean} 是否为合法email地址
*/
```
```javascript
function isEmail(email) {
  var validate = RegExp(/^\w+((-\w+)|(\.\w+))*\@[A-Za-z0-9]+((\.|-)[A-Za-z0-9]+)*\.[A-Za-z0-9]+$/).test(email);
  if(validate) {
    return true;
  }else{
    return false;
  }
}
```

\w	代表字母或数字或下划线或汉字
