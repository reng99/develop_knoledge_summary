## 验证QQ号码

目前qq号码的范围是10000-9999999999

```bash
  /**
  * 检查字符串是否为合法的qq号码
  * @param {String} 字符串
  * @return {Boolean} 是否为合法的qq号码
  */
```

相关代码

```
  function isQq(qqNum){
    var validate = RegExp(/^[1-9][0-9]{4,9}$/).test(qqNum);
    if(validate){
      return true;
    }else{
      return false;
    }
  }
```

