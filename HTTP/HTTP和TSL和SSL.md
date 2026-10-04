## 什么是HTTP

最令人诟病的是安全性，所有数据都是明文传递的，数据完整性，**中间人攻击**

## 什么是HTTPS

http处于最上层的应用层

TLS协议 是专门对数据进行加密和解密的协议

## 什么是TLS协议

传输加密协议，规定了如何为网络中传输的数据进行加密和解密

- ssl:早期由网景公司设计的加密协议，后贡献给IETF组织，并最终重命名为TLS

ssl是tls 的前身

## 什么是对称加密

加密方和解密方具有相同的密钥

client  给Server发送一个client  Hello ,将支持的TLS版本和支持的加密算法发送给Server,

server选出最适合的TLS版本和加密算法，通过server  Hello发送给client   ,client设置一个预主密钥

将其发送给server，server获得预主密钥

## 什么是非对称加密

公钥和私钥

非对称加密是不可逆的

TLS&对称加密

![image-20260228093212142](C:\Users\angel\AppData\Roaming\Typora\typora-user-images\image-20260228093212142.png)



## 数字证书



























