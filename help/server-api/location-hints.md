---
title: 位置提示
description: 本文介绍了位置提示在Edge Network服务器API中的工作方式，以便始终将最终用户请求路由到同一服务器。
exl-id: 8cd2f8e2-2065-4b7e-8d35-4ed1a716f1b3
source-git-commit: 2c7a5f007189d897ed32302a2a80c1e16af6af80
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# 位置提示

## 概述 {#overview}

[!DNL Adobe Experience Platform Edge Network]使用多个全局分布的服务器来确保快速响应时间，而不管最终用户位于何处。 它还使用基于DNS的路由来确保请求始终路由到最接近最终用户的Edge Network位置。

如果最终用户在会话过程中连接到VPN，或在其移动设备上切换网络类型，则Edge Network请求通常可以路由到其他位置。 由于Adobe Experience Platform和Adobe Experience Cloud解决方案会将最终用户配置文件信息存储在Edge Network上，因此服务器之间的中间会话路由可能会产生问题。

这是位置提示发挥作用的地方。

为确保最终用户始终与包含其当前配置文件数据的Edge Network区域服务器进行交互，位置提示功能可确保向Edge Network发出的所有请求都发送到发出会话第一个请求的同一台服务器。 这有助于用户获得一致的体验，无论他们在会话期间可能会遇到什么网络更改。

## 位置提示用法

位置提示包含在初始Edge Network请求的响应和所有后续请求中，如以下示例所示：

```json
{
   "payload":[
      {
         "scope":"EdgeNetwork",
         "hint":"or2",
         "ttlSeconds":1800
      }
   ],
   "type":"locationHint:result"
}
```

`EdgeNetwork`范围包含Edge Network相应地路由后续请求所需的所有相关信息。 在对Edge网络发出初始请求和每个后续请求的响应中，句柄中将有一个类型为`locationHint:result`的节。

与`EdgeNetwork`作用域关联的提示可以包含以下值之一：

* `or2`
* `va6`
* `irl1`
* `ind1`
* `jpn3`
* `sgp3`
* `aus3`

**API格式**

为确保正确路由后续请求，请在基本路径（通常为`ee`和`v2` API版本）之间的后续API调用的URL路径中插入位置提示。

```http
POST 'https://edge.adobedc.net/ee/{LOCATION_HINT}/v2/interact?dataStreamId={DataStream_ID}'
```

## 在Cookie中存储位置提示 {#storing-hints-in-cookies}

要确保Edge Network返回的位置提示在会话期间持续存在，您可以将位置提示值以及`ttlSeconds`字段（通常为1800秒）中包含的Cookie生命周期存储在Cookie中。

与大多数Cookie一样，每次出现Edge Network响应时，都应延长此Cookie的生命周期。 要确保与Web SDK的最大兼容性，请使用Cookie名称`kndctr_{IMSORG}_AdobeOrg_cluster`。 组织ID通常以`@AdobeOrg`结尾。 `@`值必须转换为下划线，以确保Cookie的格式正确。
