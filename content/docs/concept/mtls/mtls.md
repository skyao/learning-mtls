---
title: "mTLS概述"
linkTitle: "概述"
weight: 10
date: 2023-01-29
description: >
  什么是mTLS?
---

## 什么是 SSL？

Mutual TLS (相互 TLS) 简称 mTLS，是一种相互身份验证的方法。mTLS 通过验证他们都拥有正确的私人密钥来确保网络连接两端的各方都是他们声称的身份。他们各自的 TLS 证书中的信息提供了额外的验证。

mTLS 通常被用于零信任安全框架，以验证组织内的用户、设备和服务器。它也可以帮助保持 API 的安全。

> 零信任意味着默认情况下不信任任何用户、设备或网络流量，这种方法有助于消除许多安全漏洞。

## mTLS 如何运作？

通常在 TLS 中，服务器有一个 TLS 证书和一个公钥/私钥对，而客户端没有。典型的 TLS 流程是这样运作的：

1. 客户端连接到服务器
2. 服务器出示其 TLS 证书
3. 客户端验证服务器的证书
4. 客户端和服务器通过加密的 TLS 连接交换信息

![TLS 握手的基本步骤](https://www.cloudflare.com/resources/images/slt3lc6tev37/37w1tzGsD4XvYUkQCHbWG8/6fbbb48d0f5077cc2c662a4cc6817b1c/how_tls_works-what_is_mutual_tls.png)

然而，在 mTLS 中，客户端和服务器都有证书，并且双方都使用它们的公钥/私钥对进行身份验证。与常规 TLS 相比，mTLS 中有一些额外步骤来验证双方（额外的步骤**加粗**显示）。

1. 客户端连接到服务器
2. 服务器出示其 TLS 证书
3. 客户端验证服务器的证书
4. **客户端出示其 TLS 证书** (mTLS增加)
5. **服务器验证客户端的证书 **(mTLS增加)
6. **服务器授予访问权限** (mTLS增加)
7. 客户端和服务器通过加密的 TLS 连接交换信息

![相互 TLS (mTLS) 握手的基本步骤](https://www.cloudflare.com/resources/images/slt3lc6tev37/5SjaQfZzDLEGqyzFkA0AA4/d227a26bbd7bc6d24363e9b9aaabef55/how_mtls_works-what_is_mutual_tls.png)

## mTLS 中的证书颁发机构

实施 mTLS 的组织充当其自己的证书颁发机构。这与标准 TLS 相反，标准 TLS 的证书颁发机构是一个外部组织，负责检查证书所有者是否合法拥有关联域（了解 TLS 证书验证）。

mTLS 需要“根”TLS 证书；这使组织能够成为他们自己的证书颁发机构。授权客户端和服务器使用的证书必须与此根证书相对应。根证书是自签名的，这意味着组织自己创建它。（这种方法不适用于公共互联网上的单向 TLS，因为必须由外部证书颁发机构颁发这些证书。）

## 为什么使用 mTLS？

mTLS 有助于确保客户端和服务器之间的流量是安全和可信的。这为登录到组织网络或应用程序的用户提供了一个额外的安全层。它还可以验证与不遵循登录过程的客户端设备的连接，如物联网 ([IoT](https://www.cloudflare.com/learning/ddos/glossary/internet-of-things-iot/)) 设备。

mTLS 可以防止各种类型的攻击，包括：

- **在途攻击：**[在途攻击者](https://www.cloudflare.com/learning/security/threats/on-path-attack)把自己放在客户端和服务器之间，拦截或修改两者之间的通信。当使用 mTLS 时，在途攻击者不能对客户端或服务器进行身份验证，使这种攻击几乎不可能进行。
- **欺骗攻击：**攻击者可以试图在用户面前“伪装”（模仿）Web 服务器，或在 Web 服务器面前伪装用户。当双方都必须用 TLS 证书进行身份验证时，欺骗攻击就会困难得多。
- **凭证填充：**攻击者使用从[数据泄露](https://www.cloudflare.com/learning/security/what-is-a-data-breach/)中泄露的凭证集，试图以合法用户身份登录。如果没有合法颁发的 TLS 证书，[凭证填充](https://www.cloudflare.com/learning/bots/what-is-credential-stuffing/)对使用 mTLS 的组织的攻击就无法成功。
- **暴力攻击：**[暴力攻击](https://www.cloudflare.com/learning/bots/brute-force-attack/)通常由[机器人](https://www.cloudflare.com/learning/bots/what-is-a-bot/)执行，是指攻击者使用快速试错法来猜测用户的密码。mTLS 确保一个密码不足以获得对组织网络的访问权。（[速率限制](https://www.cloudflare.com/learning/bots/what-is-rate-limiting/)是处理这种类型的机器人攻击的另一种方法。）
- **网络钓鱼攻击：**[网络钓鱼攻击](https://www.cloudflare.com/learning/access-management/phishing-attack/)的目的通常是为了窃取用户的凭证，然后利用这些凭证入侵网络或应用程序。即使用户上当受骗，攻击者仍然需要 TLS 证书和相应的私钥才能使用这些凭证。
- **恶意 API 请求：**当用于 [API 安全](https://www.cloudflare.com/learning/security/api/what-is-api-security/)时，mTLS 可确保 API 请求只来自合法的、经过身份验证的用户。这可以阻止攻击者发送恶意的 API 请求来利用漏洞或破坏 API 的预期运作方式。

## 网站已经使用 TLS，那为什么没有在整个互联网上使用 mTLS？

对于日常用途，单向身份验证提供了足够的保护。公共互联网上 TLS 的目标是：1) 确保人们不会访问[欺骗性网站](https://www.cloudflare.com/learning/ssl/what-is-domain-spoofing/)，2) 确保[私有数据](https://www.cloudflare.com/learning/privacy/what-is-data-privacy/)在通过[包含互联网](https://www.cloudflare.com/learning/network-layer/how-does-the-internet-work)的各种网络时安全且加密，以及 3) 确保数据在传输过程中没有改变。客户端仅验证服务器身份的单向 TLS 足以实现这些目标。

此外，将 TLS 证书分发到所有最终用户设备将非常困难。生成、管理和验证为此所需的数十亿证书几乎是不可能的任务。

但在较小的规模上，mTLS 对单个组织非常有用且非常实用，尤其是当这些组织采用零信任方法来确保网络安全时。由于零信任方法默认不信任任何用户、设备或请求，因此组织必须能够在每次尝试访问网络中的任何时间对每个用户、设备和请求进行身份验证。mTLS 通过验证用户和验证设备来帮助实现这一点。

## 资料来源

- [什么是 SSL？](https://www.cloudflare.com/zh-cn/learning/ssl/what-is-ssl/)
