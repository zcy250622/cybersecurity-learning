## ssl和tsl的核心区别

TSL是SSL的标准升级版本，二者同时与加密通信协议体系，核心目标一致（提供机密性，完整性，身份认证）。目前**SSL 已完全废弃**，主流应用使用**TLS 1.2/1.3**，日常所说的 "SSL 证书" 多为习惯叫法，实际是 TLS 证书。

**疑问一：这是传输层的协议，只抓到传输层的包**

1. TLS 不是传输层协议

虽然名字里有 “Transport Layer Security”，但 TLS 并不是 OSI 模型里的**传输层协议**（比如 TCP/UDP），而是位于**应用层和传输层之间**的安全层。它的作用是为应用层协议（如 HTTP、SMTP）提供加密和认证，然后把加密后的数据封装在 TCP 段中传输。

所以，你抓到的 “TLS 包”，本质上还是 **TCP 包**，只是 Wireshark 解析出了 TCP payload 里的 TLS 内容。

2.  为什么 Wireshark 显示的是 TLS，而不是 TCP？

这是 Wireshark 的**协议解析优先级**决定的：

- 当一个 TCP 包的 payload 符合 TLS 记录格式时，Wireshark 会优先把它解析为 TLS 协议，并在 “Protocol” 列显示为 `TLSv1.2` 或 `TLSv1.3`。
- 如果你想看到底层的 TCP 信息，可以展开任意一个包，在详细信息里就能看到完整的 Ethernet II、IP、TCP 头部。

3.   为什么看不到应用层数据？

因为 TLS 已经把应用层数据（比如 HTTP 请求 / 响应）加密了。Wireshark 无法解密这些数据，所以只能显示为 `Application Data`，而无法解析出 HTTP 等应用层协议的内容。

如果你想看到明文的应用层数据，需要配置 Wireshark 使用 **TLS 会话密钥**（如 RSA 私钥或预共享密钥）来解密流量。

4. 总结一下

- 你抓到的包，底层还是 **TCP 传输层包**。
- Wireshark 只是把其中的 TLS 内容解析出来，优先显示为 TLS 协议。
- TLS 是应用层之下的安全层，不是独立的传输层协议。

























