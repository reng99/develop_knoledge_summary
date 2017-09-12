## 错误码的解析

|http状态代码|说明|
|---|---|
|100|Continue()初始的请求已经接受，客户应当继续发送请求的其余部分|
|101|Switching Protocols服务器将遵循从客户的请求转换到另外一种协议|
|200|OK一切正常，对GET 和 POST请求的应答文档跟在后面|
|201|Created服务器已经创建了文档，Location头给出了它的URL|
|202|Accepted已经接受请求，但是尚未处理完成|
|203|Non-Authoritative Information 文档已经正常地返回，但一些应答头可能不正确，因为使用的是文档的拷贝|
|204|No Content 没有新的内容，但是浏览器应该继续显示原来的文档。如果用户定期地刷新页面，而Server可以确定用户文档足够新，这个状态码是很有用的|
|205|Reset Content 没有新的内容，但是浏览器应该重置它所显示的内容。用来强制浏览器清除表单输入内容|
|206|Partial Content 客户端发送了一个带有Range头的GET请求，服务器完成了它|
|301|Moved Permanently 客户端请求的文档在其他地方，新的URL在Location头中给出，浏览器应该自动地访问新的URL|
|302|Found类似301，但是新的URL应该被视为临时性的代替，而不是永久性的。注意，在HTTP1.0中对应的状态信息是"Moved Temporatily"。出现该代码时，浏览器能够自动访问新的URL，因此是一个很有用的状态代码。**注意⚠️**这个状态码有时候可以和301替换使用。例如，如果浏览器错误的请求`http://host/~user(缺少了后面的斜杆)`，有的服务器返回301，有的就返回302|
|303|See Other 类似于301/302，不同之处在于，如果原来的请求是POST，Location头指向的重定向目标文档应该通过GET提取|
|304|Not Modified 客户端有缓冲的文档并发出了一个条件性的请求（一般是踢提供If-Modified-Since头表示客户只想要指定日期更新的文档）。服务器告诉客户，原缓冲的文档还可以继续使用。|
|305|Use Proxy 客户请求的文档应该通过Location头指明的代理服务器提供|
|307|Temporary Redirect 和 302（Found）相同。许多浏览器会错误地响应302应答进行重定向，即使原来的请求是POST，即使它实际上只能在POST请求的应答是303时才能重定向。|
|400|Bad Request 请求出现语法错误。|
|401|Unauthorized 客户试图未经授权访问受密码保护的页面。应答中包含一个WWW-Authenticate头，浏览器据此显示用户名／密码对话框，然后在填写合适的Authoization头再次发出请求|
|403|Forbidden|

