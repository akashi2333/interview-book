# websocket

H5提供的属于应用层的全双工通信协议，它基于TCP协议，并且复用HTTP的握手通道。

## 特点

- 支持双向通信。
- 没有同源限制。
- 可以发送文本也可以发送二进制数据。
- 基于TCP协议，并且复用HTTP的握手通道。

## 握手部分

客户端：申请协议升级

```
GET /chat HTTP/1.1
Host: server.example.com
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
Origin: http://example.com
Sec-WebSocket-Protocol: chat, superchat
Sec-WebSocket-Version: 13
```

服务端：响应协议升级

```
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: s3pPLMBiTxaQ9kYGzzhZRbK+xOo=
Sec-WebSocket-Protocol: chat
```

`Sec-WebSocket-Key/Sec-WebSocket-Accept` 在主要作用在于提供基础的防护，减少恶意连接、意外连接。

## 传输数据部分

- 数据分片：发送端将消息割成多个帧，并发送给服务端；接收端接收消息帧，并将关联的帧重新组装成完整的消息。

- 连接保持+心跳：客户端和服务端虽然长时间没有数据往来，但仍需要保持连接。这个时候，可以采用心跳来实现。

  - 发送方 ->接收方：ping

  - 接收方 ->发送方：pong

  ping、pong 的操作，对应的是 WebSocket 的两个控制帧，opcode分别是 `0x9、0xA`。