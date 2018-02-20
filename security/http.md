## http 协议

http协议（hyperText Transfer Protocol，超文本传送协议）是因特网上应用最为广泛的一种网络传输协议，所有的www文件都必须遵循这个标准。

http是一个基于tcp/ip通信协议来传送数据（html文件，图片文件，查询结果等） 。

### http工作原理

http协议工作于客户端-服务端架构为上。浏览器作为http客户端通过url向http服务端（即web服务器）发送所有请求。

web服务器有：apache服务器，iis服务器（internet information services）等。

web服务器根据接收到的请求后，向客户端发送响应信息。

http默认端口号为80，但是你也可以改为8080或者其他端口号。

**需要注意的要点**

- http是无连接：无连接的含义是限制每次连接只处理一个请求。服务器处理完客户的请求，并收到客户的应当后，即断开连接。采用这种方式可以节省传输时间。

- http是媒体独立的：这以为着，只要客户端和服务器知道如何处理的数据内容，任何类型的数据都可以通过http发送。客户端以及服务器指定使适合的mime-type内容类型。

- http是无状态： http协议是无状态协议。无状态是指协议对于事务处理没有记忆能力。缺少状态意味着如果后续处理需要前面的信息，则它必须重传，这样可能导致每次连接
传送的数据量增大。另一方面，在服务器不需要先前信息时它的应答就较快。

### 请求方法

|序号|方法|描述|
|----|-----|----------|
|1|GET|请求指定的页面信息，并返回实体主体。|
|2|HEAD|类似于get请求，只不过返回的响应中没有具体的内容，用于获取报头|
|3|POST|向指定资源提交数据进行处理请求（例如提交表单或者上传文件）。数据被包含在请求体中。post请求可能会导致新的资源的建立和/或已有资源的修改。|
|4|PUT|从客户端向服务器传送的数据取代指定的文档的内容。|
|5|DELETE|请求服务器删除指定的页面。|
|6|CONNECT|http/1.1协议中预留给能够将连接改为管道方式的代理服务器。|
|7|OPTIONS|允许客户端查看服务器的性能。|
|8|TRACE|回显服务器收到的请求，主要用于测试或诊断。|


### http响应头信息

http请求头提供了关于请求，响应或者其他的发送实体的信息。

下面是关于响应头信息：

|应答头|说明|
|----|-----|
|Allow|服务器支持哪些请求方法（如get,post等）|
|Content-Encoding|文档的编码（encode）方法。只有在解码之后才可以得到content-type头指定的内容类型。利用gzip压缩文档能够显著地减少html文档的下载时间。java的GZIPOutputStream可以很方便地进行gzip压缩，但只有unix上的Netscape和Windows上的IE4,IE5才支持它。因此，Servlet应该通过查看Accept-Encoding头（即request.getHeader("Accept-Encoding")）检查浏览器是否支持gzip，为支持gzip的浏览器返回经gzip压缩的html页面，为其他浏览器返回普通页面。|
|Content-Length|表示内容长度。只有当浏览器使用持久http连接时才需要这个数据。如果你想利用持久连接的优势，可以把输出文档写入ByteArrayOutputStream, 完成后查看大小，然后把值放入Content-Length头，最后通过byteArrayStream.writeTo(response.getOutputStream())发送内容|
|Date|当前的GMT时间。你可以使用setDateHeader来设置这个头以避免转换时间格式的麻烦。|
|Expires|应该在证明时候认为文档已经过期，从而不再缓存它|
|Last-Modified|文档的最后改动时间。客户可以通过If-Modified-Since请求头提供一个日期，该请求头将被视为一个条件GET，只有改动时间迟于指定时间的文档才会返回，否则返回一个304（Not Modified）状态。Last-Modified也可以用setDateHeader方法来设置。|























## 参考

[http教程](http://www.runoob.com/http/http-tutorial.html)
