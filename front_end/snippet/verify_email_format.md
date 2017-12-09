## js正则验证邮箱格式

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
