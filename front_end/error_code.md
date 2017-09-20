### 常见的状态码解析

200 --> 服务器成功返回页面

404 --> 请求的网页不存在

503 --> 服务器不可用


### 错误码的解析

|http状态代码|说明|
|---|---|
|1xx|(临时响应)表示临时响应并需要请求者继续执行操作的状态码|
|100|Continue(继续) 初始的请求已经接受，客户应当继续发送请求的其余部分|
|101|Switching Protocols（切换协议）服务器将遵循从客户的请求转换到另外一种协议|
||
|200|OK（成功）服务器已成功处理了请求。通常，这表示服务器提供了请求的网页。|
|201|Created（已创建）请求成功并且服务器已经创建了文档，Location头给出了它的URL|
|202|Accepted（已接受）已经接受请求，但是尚未处理完成|
|203|Non-Authoritative Information（非授权信息）服务器已经成功处理了请求，但是尚未处理。|
|204|No Content（无内容） 没有新的内容，但是浏览器应该继续显示原来的文档。如果用户定期地刷新页面，而Server可以确定用户文档足够新，这个状态码是很有用的|
|205|Reset Content（重置内容） 没有新的内容，但是浏览器应该重置它所显示的内容。用来强制浏览器清除表单输入内容|
|206|Partial Content（部分内容） 客户端发送了一个带有Range头的GET请求，服务器完成了它。也就是服务器成功处理了部分GET请求。|
|301|Moved Permanently 客户端请求的文档在其他地方，新的URL在Location头中给出，浏览器应该自动地访问新的URL|
|302|Found类似301，但是新的URL应该被视为临时性的代替，而不是永久性的。注意，在HTTP1.0中对应的状态信息是"Moved Temporatily"。出现该代码时，浏览器能够自动访问新的URL，因此是一个很有用的状态代码。**注意⚠️**这个状态码有时候可以和301替换使用。例如，如果浏览器错误的请求`http://host/~user(缺少了后面的斜杆)`，有的服务器返回301，有的就返回302|
|303|See Other 类似于301/302，不同之处在于，如果原来的请求是POST，Location头指向的重定向目标文档应该通过GET提取|
|304|Not Modified 客户端有缓冲的文档并发出了一个条件性的请求（一般是踢提供If-Modified-Since头表示客户只想要指定日期更新的文档）。服务器告诉客户，原缓冲的文档还可以继续使用。|
|305|Use Proxy 客户请求的文档应该通过Location头指明的代理服务器提供|
|307|Temporary Redirect 和 302（Found）相同。许多浏览器会错误地响应302应答进行重定向，即使原来的请求是POST，即使它实际上只能在POST请求的应答是303时才能重定向。|
|400|Bad Request 请求出现语法错误。|
|401|Unauthorized 客户试图未经授权访问受密码保护的页面。应答中包含一个WWW-Authenticate头，浏览器据此显示用户名／密码对话框，然后在填写合适的Authoization头再次发出请求|
|403|SC_Forbidden 的意思是除非拥有授权否则服务器拒绝提供所请求的资源。这个状态经常会由于服务器上的损坏文件或目录许可而引起。|
|404|SC_Not_Found 告诉客户端所给的地址无法找到任何资源。它是表示“没有所访问的页面”的标准方式。这个状态码是常用的响应并且在`HttpServletResponse`类中有专门的方法来实现它：`sendError("message")`。相对于setStatus使用sendError的好处是：服务器会自动生成一个错误页面来显示错误信息。但是，Internet Explorer 5浏览器（忽略ie5等介绍）|
|405|Method Not Allow 请求方法（GET、POST、HEAD、DELETE、PUT、TRACE等）对指定的资源不适用。|
|406|Not Acceptable 指定的资源已经找到，但它的MIME类型和客户在Accpet头中所指定的不兼容。|
|407|Proxy Authentication Required 类似于401，表示客户必须先经过代理服务器的授权。|
|408|Request Timeout 在服务器许可的等待时间内，客户一直没有发出任何请求。客户可以在以后重复同一请求。|
|409|Confict 通常和PUT请求有关。由于请求和资源的当前状态相冲突，因此请求不能成功。|
|410|Gone 所请求的文档已经不再可用，而且服务器不知道应该重定向到哪个地址。它和404的不同在于，返回407表示文档永远地离开了指定的位置，而404表示由于未知的原因文档不可用|
|411|Length Rquired 服务器不能处理请求，除非客户发送一个Content-Length头。|
|412|Precondition Failed 请求头中指定的一些前提条件失败|
|413|Request Entity Too Large 目标文档的大小超过服务器当前愿意处理的大小。如果服务器认为自己能够稍后再处理该请求，则应该提供一个Retry-After头|
|414|Request URI Too Long URI太长|
|416|Requested Range Not Satisfiable 服务器不能满足客户在请求中指定的Range头。|
|500|Internal Server Error 服务器遇到了意料不到的情况，不能完成客户的请求。|
|501|Not Implemented 服务器不支持实现请求所需要的功能。丽日，客户发出了一个服务器不支持的PUT请求。|
|502|Bad Gateway 服务器作为网关或者代理时，为了完成请求访问下一个服务器，但该服务器返回了非法的应答。|
|503|Service Unavailable 服务器由于维护或者负载过重未能应答。例如，Servlet可能在数据库链接池已满的情况下返回503。服务器返回503时可以提供一个Retry-After头。|
|504|Gateway Timeout 由作为代理或网关的服务器使用，表示不能及时地从远程服务器获得应答。|
|505|HTTP Version Not Supported 服务器不支持请求中所指明的HTTP版本。|



### 参考文章

- [HTTP状态代码（各种错误代码集合）](http://blog.csdn.net/guoyuqi0554/article/details/17678459)

- [HTTP状态查询-站长工具](http://tool.chinaz.com/pagestatus/)


### 说明

本文章结合上面的两篇文章进行整合，如有涉及到侵权的地方，请与本人联系，本人会在第一时间进行更改或者删除。邮箱 1837895991@qq.com,望见谅
