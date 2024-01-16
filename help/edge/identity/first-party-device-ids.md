---
title: Web SDK中的第一方设备ID
description: 了解如何为Adobe Experience Platform Web SDK配置第一方设备ID (FPID)。
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: dea75b92847320284e1dc1b939f3ae11a12077a8
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 0%

---

# Web SDK中的第一方设备ID

Adobe Experience Platform Web SDK分配 [Adobe Experience Cloud ID (ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html) 使用Cookie对网站访客进行跟踪，以跟踪用户行为。 要说明浏览器对Cookie有效期的限制，您可以选择设置和管理自己的设备标识符。 这些称为第一方设备ID (FPID)。

>[!NOTE]
>
>仅当通过Platform Web SDK向Platform Edge Network发送数据时，才支持第一方设备ID。

>[!IMPORTANT]
>
>第一方设备ID与 [第三方Cookie](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#identity) Web SDK中的功能。
>您可以使用第一方设备ID，也可以使用第三方Cookie，但不能同时使用这两项功能。

本文档介绍如何为Platform Web SDK实施配置第一方设备ID。

## 先决条件

本指南假定您熟悉身份数据如何用于Platform Web SDK，包括ECID和的角色。 `identityMap`. 有关更多详细信息，请参阅 [Web SDK中的身份数据](./overview.md) 以了解更多信息。

## 使用FPID

FPID使用第一方Cookie跟踪访客。 使用使用DNS的服务器设置第一方Cookie时，其效果最佳 [记录](https://datatracker.ietf.org/doc/html/rfc1035) （对于IPv4）或 [AAAA记录](https://datatracker.ietf.org/doc/html/rfc3596) （适用于IPv6），而不是DNS CNAME或JavaScript代码。

>[!IMPORTANT]
>
>`A` 或 `AAAA` 仅设置和跟踪Cookie支持记录。 数据收集的主要方法是通过DNS CNAME。 换句话说，FPID是使用A记录或AAAA记录设置的，然后使用CNAME发送到Adobe。
>
>此 [Adobe管理的证书计划](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) 仍支持第一方数据收集。

设置FPID Cookie后，在收集事件数据时，可以获取其值并将其发送到Adobe。 收集的FPID用作生成ECID的种子，ECID继续是Adobe Experience Cloud应用程序中的主要标识符。

要将网站访客的FPID发送到Platform Edge Network，您必须将FPID包含在 `identityMap` 给那个访客的。 有关更多详细信息，请参阅本文档后面部分： [在中使用FPID `identityMap`](#identityMap) 以了解更多信息。

### ID格式要求

Platform Edge Network仅接受符合 [UUIDv4格式](https://datatracker.ietf.org/doc/html/rfc4122). 将拒绝不采用UUIDv4格式的设备ID。

生成UUID几乎总是会生成唯一的随机ID，而发生冲突的概率可以忽略不计。 无法使用IP地址或任何其他个人身份信息(PII)为UUIDv4设定种子。 UUID无处不在，几乎每种编程语言都可以找到库来生成它们。

## 使用您自己的服务器设置Cookie

使用您拥有的服务器设置Cookie时，可以使用各种方法防止Cookie因浏览器策略而受到限制：

* 使用服务器端脚本语言生成Cookie
* 设置Cookie以响应对子域或网站上的其他端点发出的API请求
* 使用CMS生成Cookie
* 使用CDN生成Cookie

>[!IMPORTANT]
>
>使用JavaScript的 `document.cookie` 方法几乎永远不会受到限制Cookie持续时间的浏览器策略的保护。

### 何时设置Cookie

最好在向Edge Network发出任何请求之前设置FPID Cookie。 但是，在无法实现这一点的情况下，仍会使用现有方法生成ECID，并充当主要标识符（只要Cookie存在）。

假设ECID最终受到浏览器删除策略的影响，而FPID没有受到影响，则FPID将在下次访问时成为主标识符，并用于在每次后续访问时为ECID提供种子。

### 设置Cookie的过期时间

在实施FPID功能时，应仔细设置Cookie的过期时间。 在做出决定时，您应该考虑贵组织运营的国家或地区以及其中每个地区的法律和政策。

作为此决策的一部分，您可能希望采用全公司Cookie设置策略，或根据您运营的每个区域设置中的用户而有所不同。

无论您为Cookie的初始过期时间选择的设置如何，都必须确保包含每次发生对网站的新访问时都会延长Cookie过期时间的逻辑。

## Cookie标记的影响

有各种Cookie标记会影响Cookie在不同浏览器中的处理方式：

* [&#39;HTTPOnly&#39;](#http-only)
* [&#39;安全&#39;](#secure)
* [&#39;SameSite&#39;](#same-site)

### `HTTPOnly` {#http-only}

使用设置的Cookie `HTTPOnly` 无法使用客户端脚本访问标志。 这意味着，如果您设置 `HTTPOnly` 标记设置FPID时，必须使用服务器端脚本语言读取Cookie值以将其包含在 `identityMap`.

如果您选择让Platform Edge Network读取FPID Cookie的值，请设置 `HTTPOnly` 标记可确保任何客户端脚本均无法访问该值，但不会对Platform Edge Network读取Cookie的能力产生任何负面影响。

>[!NOTE]
>
>使用 `HTTPOnly` 标记对可能会限制Cookie生命周期的Cookie策略没有影响。 但是，在设置和读取FPID的值时，您仍应考虑这一点。

### `Secure` {#secure}

使用设置的Cookie `Secure` 属性仅通过HTTPS协议以加密请求发送到服务器。 使用此标记有助于确保中间人攻击者无法轻松访问Cookie的值。 如果可能，最好设置 `Secure` 标志。

### `SameSite` {#same-site}

此 `SameSite` 属性允许服务器确定Cookie是否随跨站点请求一起发送。 属性提供了一些针对跨站点伪造攻击的保护。 存在三个可能的值： `Strict`， `Lax`、和 `None`. 请咨询您的内部团队，确定适合您组织的设置。

如果否 `SameSite` 属性已指定，现在某些浏览器的默认设置为 `SameSite=Lax`.

## 在中使用FPID `identityMap` {#identityMap}

以下示例说明如何在 `identityMap`：

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ]
  }
}
```

与其他标识类型一样，您可以将FPID与其他标识一起包含在 `identityMap`. 以下是经过身份验证的CRM ID所包含的FPID示例：

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ],
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

如果启用第一方数据收集时，边缘网络正在读取的Cookie中包含FPID，则您应当仅捕获经过身份验证的CRM ID：

```json
{
  "identityMap": {
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

以下各项 `identityMap` 将导致Edge Network发出错误响应，因为它缺少 `primary` FPID的指示器。 中至少存在一个ID `identityMap` 必须标记为 `primary`.

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-12d3-a456-426614174000",
        "authenticatedState": "ambiguous"
      }
    ],
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated"
      }
    ]
  }
}
```

在这种情况下，Edge Network返回的错误响应类似于以下内容：

```json
{
    "type": "https://ns.adobe.com/aep/errors/EXEG-0306-400",
    "status": 400,
    "title": "No primary identity set in request (event)",
    "detail": "No primary identity found in the input event. Update the request accordingly to your schema and try again.",
    "report": {
        "requestId": "{REQUEST_ID}",
        "configId": "{CONFIG_ID}",
        "orgId": "{ORG_ID}"
    }
}
```

## ID层次结构

当ECID和FPID都存在时，ECID在识别用户时优先。 这可确保当浏览器Cookie存储中存在现有ECID时，该ECID仍保留为主要标识符，并且现有访客计数不会受到影响。 对于现有用户，在ECID过期或因浏览器策略或手动过程而被删除之前，FPID不会成为主要身份。

身份按以下顺序排定优先级：

1. ECID包含在中 `identityMap`
1. ECID存储在Cookie中
1. FPID包含在中 `identityMap`
1. FPID存储在Cookie中

## 迁移到第一方设备ID

如果您要使用之前实施的FPID迁移到，则可能很难在低级别上直观显示过渡情况。

为了帮助说明此过程，请考虑一个涉及以前访问过您网站的客户的情形，以及FPID迁移对Adobe解决方案中识别该客户的方式有何影响。

![显示客户ID值在迁移到FPID后如何在两次访问之间更新的图表](../assets/identity/tracking/visits.png)

>[!IMPORTANT]
>
>此 `ECID` Cookie的优先级始终高于 `FPID`.

| 访问 | 描述 |
| --- | --- |
| 首次访问 | 假设您尚未开始设置FPID Cookie。 ECID包含在 [AMCV Cookie](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) 将是用于识别访客的标识符。 |
| 第二次访问 | 第一方设备ID解决方案的推出已开始。 现有的ECID仍然存在，并且仍然是访客识别的主要标识符。 |
| 第三次访问 | 在第二次访问和第三次访问之间，经过了足够长的时间，即由于浏览器策略而删除了ECID。 但是，由于FPID是使用DNS A记录设置的，因此FPID会持续存在。 FPID现在被视为主ID，并用于种子化ECID，后者会写入最终用户设备。 此时，该用户将被视为Adobe Experience Platform和Experience Cloud解决方案中的新访客。 |
| 第四次访问 | 在第三次和第四次访问之间，由于浏览器策略而删除ECID已花费了足够多的时间。 与上次访问一样，FPID的设置方式仍然决定了它。 此时，会生成与上次访问相同的ECID。 在整个Experience Platform和Experience Cloud解决方案中，都会将该用户视为与上次访问相同的用户。 |
| 第五次访问 | 在第四次和第五次访问之间，最终用户清除了其浏览器中的所有Cookie。 将生成新的FPID，并使用它来创建新的ECID。 此时，该用户将被视为Adobe Experience Platform和Experience Cloud解决方案中的新访客。 |

{style="table-layout:auto"}

## 常见问题解答

以下是有关第一方设备ID的常见问题解答列表。

### 植入ID与仅生成ID有何不同？

种子设定概念的独特之处在于，传递给Adobe Experience Cloud的FPID会使用确定性算法转换为ECID。 每次向Adobe Experience Platform Edge Network发送相同的FPID时，都会从FPID中植入相同的ECID。

### 何时应生成第一方设备ID？

为了减少潜在的访客虚增，应在使用Web SDK发出第一个请求之前生成FPID。 但是，如果您无法执行此操作，仍将会为该用户生成ECID，并将该ECID用作主标识符。 生成的FPID将不会成为主要标识符，直到ECID不再存在。

### 哪些数据收集方法支持第一方设备ID？

当前仅Web SDK支持FPID。

### FPID是否存储在任何平台或Experience Cloud解决方案上？

使用FPID为ECID设定种子后，它会从 `identityMap` 并且将替换为已生成的ECID。 FPID未存储在任何Adobe Experience Platform或Experience Cloud解决方案中。
