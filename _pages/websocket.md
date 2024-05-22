---
title: "websocket"
tags:
    - websocket
    - 通信协议
    - ws
date: "2024-05-22"
bookmark: true
thumbnail: "/assets/img/thumbnail/websocket.webp"
---
# WebSocket 教程

WebSocket 是一种在单个 TCP 连接上进行全双工通信的协议，它非常适合需要实时数据更新的应用，如在线聊天、游戏、股票交易等。本文将介绍 WebSocket 的基础知识、如何在浏览器和服务器上实现 WebSocket，以及一些常见的使用案例。

## 目录
1. [WebSocket 基础](#websocket-基础)
2. [浏览器端 WebSocket 实现](#浏览器端-websocket-实现)
3. [服务器端 WebSocket 实现](#服务器端-websocket-实现)
4. [WebSocket 使用案例](#websocket-使用案例)
5. [WebSocket 安全性](#websocket-安全性)
6. [总结](#总结)

## WebSocket 基础

### 什么是 WebSocket
WebSocket 是一种计算机通信协议，提供了一个全双工通信通道。它在单个 TCP 连接上实现了客户端和服务器之间的双向通信。

### WebSocket 与 HTTP 的区别
- **持久连接**：WebSocket 建立后，连接保持打开状态，直到显式关闭。
- **全双工通信**：允许客户端和服务器相互独立地发送数据。
- **较低的开销**：相比于 HTTP 的每次请求都要包含完整的头部信息，WebSocket 仅在握手时使用 HTTP，之后的数据帧开销很小。

### WebSocket 连接过程
1. **握手**：客户端发起 HTTP 请求，请求头包含 `Upgrade: websocket`，服务器确认并切换协议。
2. **通信**：客户端和服务器通过 WebSocket 连接进行数据传输。
3. **关闭**：任一方可以发起关闭连接请求。

## 浏览器端 WebSocket 实现

在浏览器中使用 WebSocket 非常简单。现代浏览器都原生支持 WebSocket API。

### 创建 WebSocket 连接

```javascript
const socket = new WebSocket('ws://example.com/socket');

// 连接打开时触发
socket.onopen = function(event) {
    console.log('WebSocket is open now.');
};

// 接收到消息时触发
socket.onmessage = function(event) {
    console.log('Received message:', event.data);
};

// 连接关闭时触发
socket.onclose = function(event) {
    console.log('WebSocket is closed now.');
};

// 发生错误时触发
socket.onerror = function(error) {
    console.error('WebSocket error observed:', error);
};
```

### 发送和接收数据

```javascript
// 发送消息
socket.send('Hello Server!');

// 接收消息
socket.onmessage = function(event) {
    console.log('Received message:', event.data);
};
```

## 服务器端 WebSocket 实现

服务器端 WebSocket 可以用多种编程语言实现。以下是使用 Node.js 和 `ws` 库实现的示例。

### 安装 `ws` 库

```bash
npm install ws
```

### 创建 WebSocket 服务器

```javascript
const WebSocket = require('ws');

const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', function connection(ws) {
    console.log('A new client connected.');

    // 接收消息
    ws.on('message', function incoming(message) {
        console.log('received: %s', message);

        // 发送消息
        ws.send('Hello Client!');
    });

    // 关闭连接
    ws.on('close', function close() {
        console.log('Client has disconnected.');
    });
});
```

## WebSocket 使用案例

### 实时聊天应用

使用 WebSocket 实现实时聊天非常合适。服务器可以广播消息给所有连接的客户端，实现实时聊天功能。

### 在线游戏

在线游戏需要实时通信来同步游戏状态，WebSocket 可以实现低延迟的通信，使得游戏体验更加流畅。

### 实时数据推送

股票行情、新闻推送等实时数据更新的场景，也适合使用 WebSocket 来实现。

## WebSocket 安全性

### 使用 WSS

为了确保数据传输的安全性，应使用加密的 WebSocket (`wss://`) 代替不加密的 WebSocket (`ws://`)。

### 验证和授权

在建立 WebSocket 连接之前，可以通过 HTTP 请求进行用户验证和授权。

### 防止恶意攻击

- **限制连接数**：防止服务器资源耗尽。
- **设置超时**：防止连接长时间闲置。
- **数据校验**：对接收到的数据进行校验，防止注入攻击。

## 总结

WebSocket 提供了一种高效、低延迟的双向通信方式，适用于各种需要实时数据更新的应用场景。通过本文，你了解了 WebSocket 的基础知识、如何在浏览器和服务器上实现 WebSocket 连接，以及一些常见的使用案例和安全性考虑。希望这些内容能帮助你更好地理解和使用 WebSocket。

---

这份教程简要介绍了 WebSocket 的基本概念和使用方法。如果你有任何问题或需要更详细的信息，请参考 [MDN WebSocket 文档](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket) 或 [WebSocket 规范](https://tools.ietf.org/html/rfc6455)。