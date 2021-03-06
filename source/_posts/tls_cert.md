title: TLS握手、中断恢复、证书中心与SSH
date: 2019-04-19 17:48:03
updated: 2020-01-05
categories:
- 网络
tags:
- TLS
- DH
- RSA
- 数字证书

---

{% note info %} 我们在以前的多篇文章中都有提到各类网络协议的特征(如[常见网络协议优化与演进](https://blog.dreamtobe.cn/network_basic/))，但是对于网络安全相关这块却很零碎，我本地整理了挺多文章但是我给文章定的框架过大，导致完全无法结束，今天就把其中两个常见的问题抽出来整理成文，希望对大家有所帮助。{% endnote %}

<!-- more -->

## I. TLS 握手

### 常见的RSA算法

![](/img/tls-cert-1.jpg)

在双方都拿到随机数A、B、C后，将会使用这三个随机数生成一个对话密钥，然后使用该对话密钥进行对称加密通信，这种方式我们可以看到，安全性取决于随机数C的加密，前面的几个都是明文传的，这里就取决于服务器的公私钥机制(默认是RSA算法)

### DH算法

![](/img/tls-cert-2.jpg)

Diffie-Hellman算法，Premaster secret不需要传递，双方只需要交换各自参数，就可以算出这个随机数

## II. TLS 中断恢复(Session 恢复）

对话中断，如何避免重新握手

### session ID

- 每一次对话都有一个编号(session ID)
- 重连时如果服务端有客户端给出的这个编号就重新使用已有对话密钥

![](/img/tls-cert-3.jpg)

- 优点: 所有浏览器都支持
- 缺点: session ID通常只保留在一台服务器

### session ticket

- 客户端发送服务器上一次对话中发过来的session ticket(服务端加密的(内容包括密钥、加密方法))
- 服务端如果能够解密发送过来的session ticket，就可以复用对话密钥了

![](/img/tls-cert-4.jpg)

- 优点: 不局限于单台服务器
- 缺点: 只有如Firefox与Chrome部分浏览器支持

## III. 非对称加密常见问题

### 常规使用

![](/img/tls-cert-5.jpg)

### 确保发送者可信

这里我们有可能遇到的问题是，如上面的TLS，我们无法确定发送者是否就是我们的服务端，因此这里引入了证书中心，由于证书中心是第三方可信机构，公钥不再直接明文发送，而是通过证书中心的私钥进行加密后与相关信息一起生成数字证书再发送给客户端，客户端此时逐个使用第三方可信机构的公钥进行解密，如果成功解密，则说明该公钥是可信的，可使用。

![](/img/tls-cert-6.jpg)

因此这里有一点，是我们通常往如Letsencrypt申请证书时，实际上就是将我们服务端生成的公钥给到Letsencrypt，Letsencrypt使用其私钥以及我们给过去的信息生成一个数字证书给我们。

## IV. SSH原因与解决方案

SSH最早是芬兰学者Tatu Ylonen设计的，将登陆信息全部加密，现在已经是Linux系统远程登陆的标配，最常见的是开源实现是[OpenSSH](http://www.openssh.com/)，其基本原理是:

1. 远端服务器收到登陆请求后将公钥发送给用户
2. 用户用该公钥对密码加密发给远程服务器
3. 远程服务器用自己私钥解密，密码正确完成登陆

但是很显然这个过程中存在"中间人攻击"的问题: 如果远程服务器是第三方伪装的，由于没有上面提到的证书中心，因此用户无法识别，攻击者插在用户与远程服务器之间，对用户冒充远程主机，安全荡然无存。针对这个问题的解决方案:

1. 用户侧在第一次拿到远程服务器的公钥后，会在默认`~/.ssh/known_hosts`中扫描，检查对应`ip`是否有记录的公钥
2. 如果公钥不存在，就会提示用户，让用户检查并信任公钥，用户通过md5对比信任后就会添加到`~/.ssh/known_hosts`便后续不用信任只要对比即可
3. 如果公钥匙存在，并与远端发回来的一致便继续让用户输入密码，否则弹出错误

### 公钥登陆

当然SSH协议还支持公钥登陆:

1. 用户先将自己的公钥添加到远程服务器的`~/.ssh/authorized_keys`下面（每行一个)
2. 后续要登陆时远程主机会向用户发送一段随机字符串，用户用自己的私钥加密后发给远程服务器
3. 远程服务器用`~/.ssh/authorized_keys`中记录的公钥进行解密，如果解密成功，便验证通过，用户登陆成功

---

- [图解SSL/TLS协议](http://www.ruanyifeng.com/blog/2014/09/illustration-ssl.html)
- [数字签名是什么？](http://www.ruanyifeng.com/blog/2011/08/what_is_a_digital_signature.html)
- [SSH原理与运用（一）：远程登录](https://www.ruanyifeng.com/blog/2011/12/ssh_remote_login.html)
