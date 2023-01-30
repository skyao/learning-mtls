---
title: "SSL证书"
linkTitle: "SSL证书"
weight: 20
date: 2023-01-29
description: >
  SSL 证书是托管在网站源服务器中的数据文件。SSL 证书促成了 SSL/TLS 加密
---

## 什么是 SSL 证书？![SSL 证书安全浏览](https://cf-assets.www.cloudflare.com/slt3lc6tev37/2mkpUOPzl2jEPEERn2e57B/3b180ecab3ff7e0a5da1706434722573/ssl-certificate-secure-browsing.png)

SSL 证书使得网站能够从 HTTP 转到更加安全的 HTTPS。SSL 证书是托管在网站源服务器中的数据文件。SSL 证书促成了 SSL/TLS 加密，它们含有网站的公钥和网站标识以及相关信息。尝试与源服务器通信的设备将引用此文件，以获取公钥并验证服务器的身份。私钥应保密并妥善保管。

## 什么是 SSL？

SSL（通常称为 TLS）是用于加密互联网流量和验证服务器身份的协议。任何具有 HTTPS 网址的网站都使用 SSL/TLS。

## SSL 证书包含哪些信息？

SSL 证书包含以下信息：

- 针对其颁发证书的[域名](https://www.cloudflare.com/learning/dns/glossary/what-is-a-domain-name/)
- 证书颁发给哪一个人、组织或设备
- 证书由哪一证书颁发机构颁发
- 证书颁发机构的数字签名
- 关联的子域
- 证书的颁发日期
- 证书的到期日期
- 公钥（私钥为保密状态）

用于 SSL 的公钥和私钥本质上是用于加密和签署数据的长字符串。使用公钥加密的数据只能用私钥解密。

## 为什么网站需要 SSL 证书？

网站需要 SSL 证书，以确保用户数据的安全，验证网站的所有权，防止攻击者创建站点的虚假版本，并且获得用户信任。

**加密：**SSL/TLS 加密之所以可行，是因为 SSL 证书促成了公钥私钥配对。客户端（例如 Web 浏览器）从服务器的 SSL 证书获取打开 TLS 连接所需的公钥。

**身份验证：**SSL 证书可验证客户端正在与实际拥有该域的正确服务器进行通信。这有助于防止域[欺骗](https://www.cloudflare.com/learning/ddos/glossary/ip-spoofing/)和其他类型的攻击。

**HTTPS：**对企业而言，HTTPS 网址必须使用 SSL证书，这一点最为重要。HTTPS 是 HTTP 的安全形式，HTTPS 网站是通过 SSL/TLS 加密流量的网站。

除了在传输过程中保护用户数据外，HTTPS 还使站点更值得用户信赖。许多用户不会注意到以 http:// 和 https:// 开头的网址的区别，但大多数浏览器都使用醒目的方式[将 HTTP 站点标记为“不安全”](https://blog.cloudflare.com/today-chrome-takes-another-step-forward-in-addressing-the-design-flaw-that-is-an-unencrypted-web/)，并且尝试为切换到 HTTPS 和增强安全性提供奖励。

![SSL 证书非安全浏览](https://cf-assets.www.cloudflare.com/slt3lc6tev37/4wegfRUlYUggfQ409DnMaA/c7e1469930b95b5e686c46ba43578f71/ssl-certificate-not-secure-browsing.png)

## 网站如何获取 SSL 证书？

为了使 SSL 证书有效，域需要从证书颁发机构（CA）获取该证书。CA 是外部组织，也是受信任的第三方，它会生成并颁发 SSL 证书。CA 还使用自己的私钥对证书进行数字签名，以允许客户端设备对其进行验证。大多数（但不是全部）CA 为颁发 SSL 证书收取费用。

颁发之后，需要在网站的源站服务器上安装并激活证书。网站托管服务通常可以为网站运营者处理这一事务。在源站服务器上激活证书后，该网站便可通过 HTTPS 进行加载，并且往返于该网站的所有流量都将受到加密和保护。

## 什么是自签名 SSL 证书？

从技术上讲，任何人都可以通过生成公私钥对并包括上述所有信息来创建自己的 SSL 证书。此类证书称为自签名证书，因为使用的数字签名将是网站自己的私钥，而不是来自 CA。

但若使用自签名证书，就没有外部权威来验证源站服务器是否是它声称的身份。浏览器认为自签名证书不可信，并且尽管使用了 https:// URL，但可能仍然将站点标记为“不安全”。它们也可能会完全终止连接，从而阻止网站加载。







## 资料来源

- [什么是 SSL 证书？](https://www.cloudflare.com/zh-cn/learning/ssl/what-is-an-ssl-certificate/)
