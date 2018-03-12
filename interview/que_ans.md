## 整理的面试

心累的去整理 ...

### 介绍下你对浏览器内核的理解

主要分成两个部分：`渲染引擎（render engine）`和`js引擎`。

**渲染引擎（render engine）：**负责取得网页的内容（html,xml和图像等），整理讯息（例如css），以及计算网页的显示方式，然后输出到显示器或打印机。浏览器的内核不同对于网页的语法解析会不同，所以渲染的效果也不同。所有的网页浏览器、电子邮件客户端以及它需要编辑、显示网格内容的应用程序都需要内核。

**JS引擎：**负责解析和执行javascript来实现网页的动态效果。

最开始渲染引擎和js引擎没有区分的很明确，后来js引擎越来越独立，内核就倾向于只指渲染引擎。

常见的浏览器内核有下面这些：

Trident内核：IE,360,搜狗浏览器
Gecko内核：Netscape6及以上
Presto内核：Opera
Blink内核：Opera
Webkit内核：Safari,Chrome

### HTML5的离线缓存怎么使用？

有一个web应用有三个文件index.html,a.js,b.css，现在需要把js和css文件缓存起来

1. 在index.html里面加上 <html manifest="test.manifest">
2. manifest清单格式如下

```bash
CACHE MANIFEST 
# 上面一句必须
# V1.0.0
CACHE:
a.js
b.css
# 不需要缓存的文件
NETWORK:
*
# 无法访问页面
FALLBACK:
404.html
```

3. manifest文件的mime-type必须是 text/cache-manifest类型

```bash
1.对于每个index.html?id=1或index.html?id=2都会分别缓存index.html页面，可以通过chrome浏览器Resources/Application Cache观察
2.如果想更新缓存内容，只要修改下manifest文件即可，如改版本号v1.0.1
```

4. 离线存储如果资源有更新，可以通过如下代码来监听，但第一次加载还会是原来的版本

```javascript
window.applicationCache.addEventListener('updateready',function(e){
  if(window.applicationCache.status == window.applicationCahce.UPDATEREADY){
    window.applicationCache.swapCahe();
    if(confirm('loading new?')){
      window.location.reload();
    }
  }
},false)
```

### cookies,sessionStorage和localStorage的区别？

cookies是网站为了标示用户身份而储存在用户本地终端（client side）上的数据（通常经过加密）。

cookies数据始终在同源的http请求中携带（即使不需要），即会在浏览器和服务器间来回传递。

sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存。

**储存大小：**

cookies数据大小不能超过4k。

sessionStorage和localStorage 虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大。

**有效期：**

localStorage存储持久数据，浏览器关闭后数据不丢失，除非主动删除数据；

sessionStorage数据在当前浏览器窗口关闭后自动删除；

cookie设置cookie过期时间之前一直有效，即使窗口或浏览器关闭。

### iframe有哪些缺点？

1. iframe会阻塞主页面的onload事件
2. 搜索引擎的检索程序无法解读这种页面，不利于seo
3. iframe和主页面共享连接池，而浏览器对相同的连接有限制，所以会影响页面的并行加载。

使用iframe之前要考虑上面的1，3两个缺点。如果需要使用iframe，最好是通过javascript动态给iframe添加src属性值，这样可以绕开这两个问题。

### webSocket如何兼容低浏览器？(阿里)

Adobe Flash Socket 、 ActiveX HTMLFile (IE) 、 基于 multipart 编码发送 XHR 、 基于长轮询的 XHR

