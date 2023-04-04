---
title: "概述"
linkTitle: "概述"
weight: 1
date: 2023-01-29
description: >
  方法概述
---



以下是公钥基础设施使用X.509（PKIX）规范所假定的体系结构模型的简化视图。

该模型中的组件包括：

- end entity: 最终实体, PKI证书的用户和/或作为证书主体的最终用户系统；

- CA: certification authority 证书颁发机构；

- RA: registration authority, 注册机构，即CA授权某些管理功能的可选系统；

- CRL issuer: CRL发卡机构：生成和签署CRL的系统；

- repository:  存储库, 存储证书和CRL的分布式系统或集合，用作将这些证书和CRL分发给终端实体的手段。

CA负责指示其颁发的证书的吊销状态。可以使用在线证书状态协议（OCSP）[RFC2560]、证书撤销列表（CRL）或一些其他机制来提供撤销状态信息。通常，当使用CRL提供撤销状态信息时，CA也是CRL颁发者。但是，CA可以将签发CRL的责任委托给其他实体。

请注意，属性颁发机构（AA）也可以选择将CRL的发布委托给CRL颁发者。



```
   +---+
   | C |                       +------------+
   | e | <-------------------->| End entity |
   | r |       Operational     +------------+
   | t |       transactions          ^
   | i |      and management         |  Management
   | f |       transactions          |  transactions        PKI
   | i |                             |                     users
   | c |                             v
   | a | =======================  +--+------------+  ==============
   | t |                          ^               ^
   | e |                          |               |         PKI
   |   |                          v               |      management
   | & |                       +------+           |       entities
   |   | <---------------------|  RA  |<----+     |
   | C |  Publish certificate  +------+     |     |
   | R |                                    |     |
   | L |                                    |     |
   |   |                                    v     v
   | R |                                +------------+
   | e | <------------------------------|     CA     |
   | p |   Publish certificate          +------------+
   | o |   Publish CRL                     ^      ^
   | s |                                   |      |  Management
   | i |                +------------+     |      |  transactions
   | t | <--------------| CRL Issuer |<----+      |
   | o |   Publish CRL  +------------+            v
   | r |                                      +------+
   | y |                                      |  CA  |
   +---+                                      +------+
        
```

图1: PKI实体
