---
title: 位置提示
description: 本文介绍位置提示在Edge Network Server API中的工作方式，以便始终将最终用户请求路由到同一服务器。
exl-id: 8cd2f8e2-2065-4b7e-8d35-4ed1a716f1b3
source-git-commit: 2c7a5f007189d897ed32302a2a80c1e16af6af80
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# 位置提示

## 概述 {#overview}

此 [!DNL Adobe Experience Platform Edge Network] 使用多台分布在全球的服务器，以确保无论最终用户位于何处，均能快速响应。 它还使用基于DNS的路由，确保请求始终路由到最接近最终用户的边缘网络位置。

如果最终用户在会话过程中连接到VPN，或在其移动设备上切换网络类型，则边缘网络请求通常可以路由到其他位置。 由于Adobe Experience Platform和Adobe Experience Cloud解决方案会将最终用户配置文件信息存储在Edge Network上，因此服务器之间的会话期间路由可能会产生问题。

这是位置提示发挥作用的地方。

为确保最终用户始终与包含其当前配置文件数据的Edge Network区域服务器进行交互，位置提示功能可确保向Edge Network发出的所有请求都发送到发出会话第一个请求的同一服务器。 这有助于用户获得一致的体验，无论他们在会话期间可能会遇到什么网络更改。

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

此 `EdgeNetwork` 范围包含Edge Network相应地路由后续请求所需的所有相关信息。 在对Edge网络的初始请求和每个后续请求的响应中，句柄中将有一个部分具有以下类型 `locationHint:result`.

与 `EdgeNetwork` 作用域可以包含以下值之一：

* `or2`
* `va6`
* `irl1`
* `ind1`
* `jpn3`
* `sgp3`
* `aus3`

**API格式**

为确保正确路由后续请求，通常在基本路径之间后续API调用的URL路径中插入位置提示 `ee`、和 `v2` API版本。

```http
POST 'https://edge.adobedc.net/ee/{LOCATION_HINT}/v2/interact?dataStreamId={DataStream_ID}'
```

## 将位置提示存储在Cookie中 {#storing-hints-in-cookies}

要确保Edge Network返回的位置提示在会话期间持续存在，您可以将位置提示值以及Cookie生命周期存储在Cookie中，后者包含在 `ttlSeconds` 字段（通常为1800秒）。

与大多数Cookie一样，每次有来自Edge Network的响应时，您都应延长此Cookie的生命周期。 要确保与Web SDK的最大兼容性，请使用Cookie名称 `kndctr_{IMSORG}_AdobeOrg_cluster`. 组织ID通常以下列内容结尾 `@AdobeOrg`. 此 `@` 值必须转换为下划线，以确保Cookie的格式正确。
