---
title: 位置提示
description: 本文介绍了位置提示在边缘网络服务器API中的工作方式，以便最终用户请求可以始终路由到同一服务器。
source-git-commit: 7f1d8fba34c5478f0d6e727a5a52af642852c9dd
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---


# 位置提示

## 概述 {#overview}

的 [!DNL Adobe Experience Platform Edge Network] 使用多台分布于全局的服务器来确保快速响应时间，而不考虑最终用户的位置。 它还使用基于DNS的路由来确保请求始终路由到最接近最终用户的边缘网络位置。

如果最终用户在会话期间连接到VPN或在其移动设备上切换网络类型，则边缘网络请求通常可以路由到其他位置。 由于Adobe Experience Platform和Adobe Experience Cloud解决方案将最终用户配置文件信息存储在边缘网络上，因此服务器之间的会话中间路由可能会出现问题。

这就是发挥位置提示作用的地方。

为确保最终用户始终与包含其当前配置文件数据的边缘网络区域服务器进行交互，位置提示功能可确保对边缘网络的所有请求都发送到发出会话第一个请求的同一服务器。 无论用户在会话过程中会经历哪些网络更改，这都有助于用户获得一致的体验。

## 使用位置提示

初始边缘网络请求的响应以及所有后续请求中都包含位置提示，如以下示例所示：

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

的 `EdgeNetwork` 范围包含边缘网络相应地路由后续请求所需的所有相关信息。 在响应对边缘网络的初始和每个后续请求时，句柄中将有一个部分，其类型为 `locationHint:result`.

与 `EdgeNetwork` 范围可以包含以下值之一：

* `or2`
* `va6`
* `irl1`
* `ind1`
* `jpn3`
* `sgp3`
* `aus3`

**API格式**

为确保后续请求正确路由，通常在基本路径之间的后续API调用的URL路径中插入位置提示 `ee`和 `v2` API版本。

```http
POST 'https://edge.adobedc.net/ee/{LOCATION_HINT}/v2/interact?dataStreamId={DataStream_ID}'
```

## 在Cookie中存储位置提示 {#storing-hints-in-cookies}

为确保边缘网络返回的位置提示在会话期间持续存在，您可以将位置提示值与Cookie生命周期(包含在 `ttlSeconds` 字段（通常为1800秒）。

与大多数Cookie一样，每当出现来自边缘网络的响应时，您应该延长此Cookie的生命周期。 要确保与Web SDK的最大兼容性，请使用Cookie名称 `kndctr_{IMSORG}_AdobeOrg_cluster`. IMS组织ID通常以 `@AdobeOrg`. 的 `@` 必须将值转换为下划线，以确保cookie的格式正确。
