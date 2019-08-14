1. 100

2. 200

3. 300

   * 307 Internal Redirect

     http强制重定向到https. **HTTP严格传输安全** (**H**TTP **S**trict **T**ransport **S**ecurity) 使用[HTTPS](https://zh.wikipedia.org/wiki/超文本传输安全协议)与网站进行通信，以减少[会话劫持](https://zh.wikipedia.org/wiki/会话劫持)风险

     该响应代码与[302重定向](https://zh.wikipedia.org/wiki/HTTP_302)有所区别的地方在于，收到307响应码后，客户端应保持请求方法不变向新的地址发出请求。

     HSTS的作用是强制客户端（如浏览器）使用HTTPS与服务器创建连接。服务器开启HSTS的方法是，当客户端通过HTTPS发出请求时，在服务器返回的[超文本传输协议](https://zh.wikipedia.org/wiki/超文本传输协议)（HTTP）响应头中包含`Strict-Transport-Security`字段。非加密传输时设置的HSTS字段无效。 (SSL剥离攻击)

4. 400

5. 500

6. 