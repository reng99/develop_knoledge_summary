## 验证密码的复杂程度

在注册账号和修改密码的时候，为了确保账号的安全，一般都会对密码的复杂程度进行监控。

```javascript
  
  /**
  * 判断字符类型
  */
  function CharMode(iN){
    if(iN >= 48 && iN <= 57){ // 数字
      return 1;
    }else if(iN >= 65 && iN <= 90){ // 大写字母
      return 2;
    }else if(iN >= 97 && iN <= 122){ // 小些字母
      return 4;
    }else{
      return 8; // 特殊字符
    }
  }
  
  /**
  * 统计字符类型
  */
  function bitTotal(num){
    var modes = 0;
    for(i = 0; i < 4;i++){
      if(num & 1) modes++;
      num >>>= 1;
    }
    return modes;
  }
  
  /**
  * 返回密码的强度级别
  */
  function checkStrong(sPW){
    var Modes = 0;
    if(sPW.length <= 4){
      return 0; // 密码太短
    }
    for(i = 0; i < sPW.length; i++){
      // 测试每一个字符的类别并统计一共有多少种模式
      Modes |= CharMode(sPW.charCodeAt(i));
    }
    return bitTotal(Modes);
  }
```

这里有几个知识点

1. `|=` 这是按位或后赋值

2. `>>>=` 这是无符号右移后赋值

3. `charCodeAt()` 方法可以返回指定位置的字符串的Unicode编码。这个返回值是0-65535之间的整数。讲到了`charCodeAt()`方法，觉得有必要讲下`charAt()`方法，它是返回指定位置的字符子串。

demo比较来一个：

```javascript

  var str = 'reng';
  console.log(str.charCodeAt(0)); // 114
  console.log(str.charAt(0)); //r

```


