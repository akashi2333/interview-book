# HTTP缓存

强缓存：直接从本地缓存读取资源，返回状态码200。

协商缓存：向服务器发送请求，由服务器通知缓存是否可以使用，返回状态码304。

- 浏览器请求 a.js。

- 服务器返回 a.js，同时告诉浏览器过期绝对时间（Expires）以及相对时间（Cache-Control：max-age=10），以及a.js上次修改时间Last-Modified，以及 a.js 的Etag。
- 10秒内浏览器再次请求 a.js，不再请求服务器，直接使用本地缓存。

- 11秒时，浏览器再次请求 a.js，请求服务器，带上上次修改时间 If-Modified-Since 和上次的 Etag 值 If-None-Match。

- 服务器收到浏览器的If-Modified-Since和Etag，发现有If-None-Match，则比较 If-None-Match 和 a.js 的 Etag 值，忽略If-Modified-Since的比较。

- a.js 文件内容没变化，则Etag和If-None-Match 一致，服务器告诉浏览器继续使用本地缓存（304）。

![img](https://barryyeee.github.io/InterviewGuide/Images/HTTP%E7%BC%93%E5%AD%98.jpg)