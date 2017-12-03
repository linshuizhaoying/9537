---
title: URL 长度限制
toc: true
date: 2017-11-24  15:00:32
tags: [前端, HTTP 协议, URL]
---

### 知识点
- HTTP 协议针对 URL 的长度限制
- 浏览器中对 URL 长度的限制
- 服务器如何对 URL 进行限制
- 为什么进行 URL 长度限制

### Http 协议针对 URL 的长度限制
在回答“为什么进行 URL 长度限制”时，我觉得首先需要明确的是：在Http1.1 协议中并没有提出针对 URL 的长度进行限制，RFC 协议里面是这样描述的，HTTP 协议并不对 URI 的长度做任何的限制，服务器端必须能够处理任何它们所提供服务多能接受的 URI，并且能够处理无限长度的URI，如果服务器不能处理过长的 URI，那么应该返回 414 状态码，以下是 HTTP 协议的原文：

> The HTTP protocol does not place any a priori limit on the length of a URI. Servers MUST be able to handle the URI of any resource they serve, and SHOULD be able to handle URIs of unbounded length if they provide GET-based forms that could generate such URIs. A server SHOULD return 414 (Request-URI Too Long) status if a URI is longer than the server can handle (see section 10.4.15).

> Note: Servers ought to be cautious about depending on URI lengths above 255 bytes, because some older client or proxyimplementations might not properly support these lengths.

对于 GET 请求，在 URL 的长度限制范围之内，请求的参数个数没有限制。

虽然 HTTP 协议规定了没有限制，但是 Web 服务器和浏览器对 URI 都有自己的长度限制。

### 浏览器中对 URL 长度的限制
每种浏览器也会对 URL 的长度有所限制，下面是几种常见浏览器的 URL 长度限制：(单位：字符)

- IE: 2083（如果超过这个数字，提交按钮没有任何反应）
- Firefox: 65536
- Chrome: 8182
- Safari: 80000
- Opera: 190000

### 服务器如何对 URL 进行限制
服务端也有最大承受的 URL 长度：(单位：字符)

- Apache: 8192
- IIS: 16384

服务端都是通过控制 HTTP 请求头的长度来进行限制的，nginx 的配置参数为 large_client_header_buffers，tomcat 的请求配置参数为 maxHttpHeaderSize，都是可以自己去进行设置。

注：对于中文的传递，最终会为 urlencode 后的编码形式进行传递，如果浏览器的编码为 UTF8 的话，一个汉字最终编码后的字符长度为 9 个字符。

因此如果使用的 GET 方法，最大长度等于URL最大长度减去实际路径中的字符数。

### 为什么进行 URL 长度限制

了解了以上三点，这个问题就可以答了。

首先 HTTP 协议中并没有针对 URL 的长度进行限制，只是规定了如果 URI 太长的话服务器又处理不了的话，应该返回 414 状态码。所以，按照协议，服务器和浏览器对 URI 都有自己的长度限制。