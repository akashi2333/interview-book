# Cookie和Session

会话跟踪。

## Cookie

cookie是服务器发送到浏览器并保存在本地的一小块数据，对于同源的每个请求都会自动携带cookie，于是服务端就可以判断用户身份。

## Session

session代表着服务器与客户端一次会话的过程。对于客户端的每个会话，都有一个唯一的`SESSIONID`与其对应，服务端将用户数据存储进`SESSIONID`对应的文件或者是内存中，只要客户端每次请求将`SESSIONID`交予服务端，服务端就能区别用户进行会话跟踪。

## Cookie和Session的区别

- cookie保存在客户端，session保存在服务器端。
- cookie只能保存ASCII码，session可以保存任意数据类型。
- cookie相较于session不安全。
- cookie只有4K左右大小，session可存取数据远高于cookie。
- cookie可以长时间保存，session一般客户端关闭或者session超时都会失效。

## Cookie和Session的配合

用户第一次请求服务器时，服务器会根据用户提交的信息创建对应的session，然后会把`SESSIONID`返回给浏览器，浏览器将`SESSIONID`存入cookie，同时记录`SESSIONID`的域名。

当用户再次请求服务器时，请求会自动判断当前域名是否存在cookie，如果存在就将cookie一起发送给服务器，服务器会从中获取`SESSIONID`，再通过`SESSIONID`查找相应的session，如果没有找到就说明用户没有登陆或者登录失效，如果找到就执行之后的操作。

## 浏览器禁用Cookie

- 每个请求都带有`SESSIONID`参数信息。
- `Token`机制：当用户第一次登录后，服务器根据提交的用户信息生成一个 `Token`，响应时将 `Token` 返回给客户端，以后客户端只需带上这个 `Token` 前来请求数据即可，无需再次登录验证。

## 分布式Session

将session存在数据库里，保障分发到每一个服务器的响应结果都一致。