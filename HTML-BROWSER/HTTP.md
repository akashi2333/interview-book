# HTTP

超文本传输协议，基于TCP/IP通信协议，是应用层的协议，浏览器作为HTTP客户端通过URL向HTTP服务端即WEB服务器发送所有请求。Web服务器根据接收到的请求后，向客户端发送响应信息。

## 特点

- 可以传输任意类型的数据对象。
- 简单快速。
- 无连接：每次连接只能处理一个请求。
- 无状态：指协议对于事务处理没有记忆能力。缺少状态意味着如果后续处理需要前面的信息，则它必须重传，这样可能导致每次连接传送的数据量增大。另一方面，在服务器不需要先前信息时它的应答就较快。

## URL

统一资源定位器，一种特殊的URI。

`https://www.example.com:80/path/to/myfile.html?key1=value1&key2=value2#anchor`

- 协议部分（protocol）：该URL的协议部分为`https://`。
- 域名部分（domain）：该URL的域名部分为`www.example.com`。一个URL中，也可以使用IP地址作为域名使用。
- 端口部分(port)：该URL的端口部分为`:80`。，域名和端口之间使用“:”作为分隔符。
- 路径部分（path）：该URL的路径部分为`/path/to/myfile.html`。
- 锚点部分（anchor）：该URL的锚点部分为`#anchor`。从“#”开始到最后，都是锚部分。
- 查询参数部分(parameter)：该URL的查询参数部分为`?key1=value1&key2=value2`。从“？”开始到“#”为止之间的部分为参数部分，又称搜索部分、查询部分。参数可以允许有多个参数，参数与参数之间用“&”作为分隔符。

## 请求消息Request

请求消息一般包括请求行、请求头部、空行和请求数据四个部分。

```
POST / HTTP1.1
Host:www.wrox.com
User-Agent:Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 2.0.50727; .NET CLR 3.0.04506.648; .NET CLR 3.5.21022)
Content-Type:application/x-www-form-urlencoded
Content-Length:40
Connection: Keep-Alive

name=Professional%20Ajax&publisher=Wiley
```

## 响应消息Response

响应消息一般包括状态行、消息包头、空行和响应正文四个部分。

```
HTTP/1.1 200 OK
Date: Fri, 22 May 2009 06:07:21 GMT
Content-Type: text/html; charset=UTF-8

<html>
      <head></head>
      <body>
            <!--body goes here-->
      </body>
</html>
```

## 状态码

| 状态码 |                         含义                         |
| :----: | :--------------------------------------------------: |
|  200   |                    客户端请求成功                    |
|  301   | 永久移动，资源移动到新的URI中，之后用新的URI请求资源 |
|  302   |    暂时移动，资源临时移动，可以用旧的URI请求资源     |
|  304   |      未修改，请求的资源没有改动，不返回任何资源      |
|  400   |                  客户端请求语法错误                  |
|  401   |                     需要用户验证                     |
|  404   |                    请求资源不存在                    |
|  500   |                    服务器发生错误                    |

## 请求方法

| 请求方法 |                           方法含义                           |
| :------: | :----------------------------------------------------------: |
|   get    |                   请求页面信息返回响应主体                   |
|   post   |                           提交数据                           |
|   head   |             获取响应头信息，常用于查看客户端性能             |
| options  | 请求服务器返回该资源所支持的所有请求方法，常用于客户端查看服务器的性能 |
|  trace   |  请求服务器回显其收到的请求信息，常用于HTTP请求的测试或诊断  |
|   put    |                   指定资源位置上传最新内容                   |
|  delete  |                   删除所请求URI标识的资源                    |
| connect  | 将连接改为管道方式的代理服务器，常用于SSL加密服务器与非加密的HTTP代理服务器的通信 |

## 工作原理

1. 寻找服务器ip，现在缓存中找，然后在本地hosts文件里找，最后查询DNS服务器。
2. 构建http请求，用TCP封装http请求，依次经过传输层、网络层、数据链路层和物理层到达服务器，服务器解析请求返还相应的html。
3. 浏览器根据返回的html构建DOM树，中途如果遇到图片、视频等资源会并行下载，如果遇到js脚本，会先下载相应的js脚本，这会造成阻塞，然后根据样式构建CSSOM树，接着两棵树合成render树。
4. 最后进行布局绘制。

## GET和POST的区别

- get参数放在URL中传递、post参数放在request body中传递。
- get只能进行URL编码，而post可以用多种方式编码。
- get能够使用缓存，post不行。
- get传递参数有长度限制，post没有。
- get产生一个TCP包，而post产生两个TCP包（get把header和data一并发送，而post先发送header，响应100后再继续发送data）。
- get参数会被保留在历史记录里，而post不会。
- get浏览器回退无害，post会再次请求。
- get满足幂等性，post不满足。（幂等性：一次请求和多次请求某一资源具有同样的副作用，put、delete都满足）

## HTTP发展阶段的特点

### HTTP1.0的特点

- 协议版本信息会随着每个请求发送，即`HTTP 1.0`被追加到了`GET`行。
- 引入请求头，在发起请求时候会通过`HTTP`请求头告诉服务器它期待服务器返回什么类型的文件、采取什么形式的压缩、提供什么语言的文件以及文件的具体编码。
- 引入响应头，服务器以请求头中信息准备数据，并以响应头的信息告诉客户端数据采用何种格式返回，倘若遇到不支持的格式，只能返回服务器支持的格式，并在响应头中体现，也就是说最终浏览器是以响应头的信息解析数据。
- 引入状态码，状态码会在响应开始时发送，使浏览器能了解请求执行成功或失败，并相应调整行为。
- 引入了缓存机制，通过状态码与`If-Modified-Since`、`Expires`等控制更新或使用本地缓存。
- 引入了`Content-Type`头，使`HTTP`具备了传输除纯文本`HTML`文件以外其他类型文档的能力。

### HTTP1.1的特点

- 缓存处理，`HTTP 1.1`引入了更多的缓存控制策略，例如`Entity tag`、`If-Unmodified-Since`、`If-Match`、`If-None-Match`等更多可供选择的缓存头来控制缓存策略。
- 带宽优化以及网络连接的使用，在请求头中引入了`range`，它允许只请求资源的某一个部分，即返回`206`状态码，这样方便了开发者自由选择以便充分利用带宽和链接，并且可以使用`Range`和`Content-Range`制作断点续传功能。
- 错误通知的管理，在`HTTP 1.1`中新增了`24`个错误状态码。
- 增加`Host`请求头，能够使不同域名配置在同一个`IP`地址的服务器上。
- 支持长连接，`HTTP 1.1`支持长连接，在一个`TCP`连接上可以传输多个`HTTP`请求和响应，减少了建立和关闭连接的消耗和延迟，在`HTTP 1.1`中默认开启`Connection：keep-alive`，一般浏览器对于同一个域名允许同时建立`6`个长链接。
- 增加管线化技术，允许在第一个应答被完全发送之前就发送第二个请求，以改善队头阻塞问题，但响应的顺序还是会按照请求的顺序返回。
- 支持响应分块，通过设置`Transfer-Encoding: chunked`进行分块响应，允许响应的数据可以分成多个部分，配合服务端尽早释放缓冲可以获得更快的响应速度。

### HTTP2.0的特点

- 二进制分帧，`HTTP 2.0`是二进制协议而不是文本协议，将所有传输的信息分割为更小的消息和帧,并对它们采用二进制格式的编码。
- 多路复用，并行的请求能在同一个链接中处理，在同一域名下所有访问都是从同一个`TCP`连接中走，`HTTP`消息被分解为独立的帧，服务端根据标识符和首部将消息重新组装起来，移除了`HTTP 1.1`中顺序和阻塞的约束。
- 压缩`header`，`header`在一系列请求中常常是相似的，其移除了重复和传输重复数据的成本。
- 服务端推送，服务器可以主动地向客户端推送资源，而无需客户端明确的请求。