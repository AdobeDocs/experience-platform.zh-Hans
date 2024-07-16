---
title: 传输层安全性(TLS)信息
description: 有关使用哪些TLS版本和密码的信息
exl-id: 04948cd8-6cf0-4159-a9d3-3130b97af106
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# 传输层安全性(TLS)信息

>[!NOTE]
>
>Adobe Experience Platform Launch已更名为Adobe Experience Platform中的一套数据收集技术。 因此，产品文档中的术语有一些改动。 有关术语更改的综合参考，请参阅[术语更新](../../term-updates.md)文档。

传输层安全性(TLS)是一种加密协议，为通过Internet在应用程序之间发送的数据提供端到端的安全性。 有关TLS的更多详细信息，请阅读[TLS基础知识](https://www.internetsociety.org/deploy360/tls/basics/)文档。

Adobe Experience Platform中的标记是一个标记管理系统，旨在动态地在您的网站上加载脚本。 加载这些脚本时，TLS保护Adobe主机`assets.adobedtm.com`与您的网站之间的通信。

有多种可用的TLS版本，并且支持多种不同的密码。 并非所有版本和密码都与某些版本相同，它们被认为不如其他版本安全或安全性更高。

## 支持的TLS版本和密码

Adobe主机选项当前支持以下TLS版本和密码：

```
PORT    STATE SERVICE
443/tcp open  https
| ssl-enum-ciphers:
|   TLSv1.2:
|     ciphers:
|       TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|     compressors:
|       NULL
|     cipher preference: server
|   TLSv1.3:
|     ciphers:
|       TLS_AKE_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|       TLS_AKE_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_AKE_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|     cipher preference: client
|_  least strength: A
```

### 自托管

如果您[自托管](../publishing/hosts/self-hosting-libraries.md)您的库，则支持的TLS版本将由您自己的托管服务决定。

## TLS密码将于2024年5月1日删除

```
PORT    STATE SERVICE
443/tcp open  https
| ssl-enum-ciphers:
|   TLSv1.2:
|     ciphers:
|       TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA (secp256r1) - A
|       TLS_RSA_WITH_AES_256_GCM_SHA384 (rsa 2048) - A
|       TLS_RSA_WITH_AES_128_GCM_SHA256 (rsa 2048) - A
|       TLS_RSA_WITH_AES_256_CBC_SHA256 (rsa 2048) - A
|       TLS_RSA_WITH_AES_128_CBC_SHA256 (rsa 2048) - A
|       TLS_RSA_WITH_AES_256_CBC_SHA (rsa 2048) - A
|       TLS_RSA_WITH_AES_128_CBC_SHA (rsa 2048) - A
|     compressors:
|       NULL
|     cipher preference: server
|   TLSv1.3:
|     ciphers:
|       TLS_AKE_WITH_AES_128_CCM_8_SHA256 (secp256r1) - A
|       TLS_AKE_WITH_AES_128_CCM_SHA256 (secp256r1) - A
|     cipher preference: client
|_  least strength: A
```
