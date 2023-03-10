---
title: "SSL概述"
linkTitle: "概述"
weight: 10
date: 2023-01-29
description: >
  什么是加密？有哪些类型的加密？
---

## 什么是 SSL？

安全套接字层 (SSL) 是一种加密安全协议。它最初由 Netscape 于 1995 年开发，旨在确保 Internet 通信中的隐私、身份验证和数据完整性。SSL 是如今使用的现代 TLS 加密的前身。

实施 SSL/TLS 的网站的 URL 中带有“HTTPS”，而不是“HTTP”。

![HTTP 与 HTTPS](https://www.cloudflare.com/img/learning/security/glossary/what-is-ssl/http-vs-https.svg)



## SSL/TLS 如何工作？

- 为了提供高度隐私，SSL 会对通过 Web 传输的数据进行加密。这意味着，任何试图截取此数据的人都只会看到几乎无法解密的乱码字符。
- SSL 在两个通信设备之间启动称为握手的身份验证过程，以确保两个设备确实是它们声称的真实身份。
- SSL 还对数据进行数字签名，以提供数据完整性，验证数据是否在到达目标接收者之前被篡改过。

SSL 已经过多次迭代，安全性逐代增强。SSL 在 1999 年更新为 TLS。

## SSL/TLS 为何重要？

最初，Web 上的数据是以明文形式传输的，任何人只要截获消息都可以读取。例如，如果消费者访问了购物网站，下了订单并在网站上输入了他们的信用卡号，那么该信用卡号将不加隐藏地在 Internet 上传播。

创建 SSL 就是为了纠正此问题并保护用户隐私。通过对用户和 Web 服务器之间传输的所有数据进行加密，SSL 可确保截获数据的人只能看到混乱的字符。消费者的信用卡号现在可以确保安全，仅在他们输入卡号的购物网站上可见。

SSL 还可以阻止某些类型的网络攻击：它对 Web 服务器进行身份验证，这非常重要，因为攻击者通常会尝试建立伪造网站来欺骗用户并窃取数据。它还可以防止攻击者篡改传输中的数据，就像药品容器上的防篡改封条一样。

## SSL 和 TLS 是同一回事吗？

SSL 是另一个称为 TLS（传输层安全性）的协议的直接前身。在 1999 年，互联网工程任务组（IETF）提出了对 SSL 的更新。由于此更新是由 IETF 开发的，不再牵涉到 Netscape，因此名称更改为 TLS。SSL 的最终版本（3.0）与 TLS 的第一版本之间并无明显差异，应用名称更改只是表示所有权改变。

由于它们紧密地联系在一起，这两个术语经常互换使用并混为一谈。有些人仍然使用 SSL 来指代 TLS，其他人则使用术语“SSL/TLS 加密”，因为 SSL 仍然具有很大的知名度。

## SSL 仍然没有落伍吗？

SSL 自 1996 年推出 SSL 3.0 以来未曾更新过，现已弃用。SSL 协议中存在多个已知漏洞，安全专家建议停止使用。实际上，大多数现代 Web 浏览器已彻底不再支持 SSL。

TLS 是依然在网络上实施的最新加密协议，尽管有许多人仍将其称为“SSL 加密”。这可能会使购买安全解决方案的消费者感到困惑。事实上，如今提供“SSL”的任何供应商提供的几乎肯定都是 TLS 保护，这已成为二十多年来的行业标准。但是，由于许多人仍在搜寻“SSL 保护”，因此这个术语在许多产品页面上仍然处于醒目位置。

## 什么是 SSL 证书？

SSL 只能由具有 SSL 证书（技术上称为“TLS 证书”）的网站来实现。SSL 证书就像身份证或徽章一样，证明某人就是他们所说的真实身份。SSL 证书由网站或应用程序的服务器存储并显示在 Web 上。

SSL 证书中最重要的信息之一是网站的公共密钥。公钥使得加密和身份验证成为可能。用户的设备查看公钥，并使用它与 Web 服务器建立安全的加密密钥。同时，Web 服务器还具有一个保密的私有密钥。私钥解密使用公钥加密的数据。

证书颁发机构（CA）负责颁发SSL证书。

## SSL 证书有哪些不同类型？

有几种不同类型的 SSL 证书。一个证书可以应用于一个或多个网站，具体取决于类型：

- 单域：单域 SSL 证书仅适用于一个域（“域”是网站的名称，例如 www.cloudflare.com）。
- 通配符：与单域证书一样，通配符 SSL 证书仅适用于一个域。但是，它也包括该域的子域。例如，通配符证书可以覆盖 www.cloudflare.com、blog.cloudflare.com，和 developers.cloudflare.com，而单域证书只能覆盖第一个。
- 多域：顾名思义，多域 SSL 证书可以应用于多个不相关的域。

SSL 证书还具有不同的验证级别。验证级别就像背景检查一样，并且级别会根据检查的彻底性而变化。

- 域验证：这是最严格的验证级别，也是最便宜的级别。企业只需要证明他们控制着域。
- 组织验证：这是一个需要亲力亲为的过程：证书机构直接联系请求证书的人员或企业。这些证书更受用户信赖。
- 扩展验证：在发出 SSL 证书之前，需要对组织进行全面的背景检查。

## 资料来源

- [什么是 SSL？](https://www.cloudflare.com/zh-cn/learning/ssl/what-is-ssl/)
