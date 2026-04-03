---
title: 在数据收集中使用第一方设备ID
description: 在将数据发送到Edge Network的Web实施中，为持久身份配置第一方设备ID (FPID)。
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1905'
ht-degree: 0%

---

# 在数据收集中使用第一方设备ID

Experience Platform Edge Network使用Experience Cloud ID (ECID)来识别网站访客。 为了提高所拥有资产的身份持久性，您可以设置和管理自己的设备标识符，称为第一方设备ID (FPID)。 Edge Network使用FPID为Adobe解决方案使用的ECID提供种子。

本页假设您熟悉ECID和`identityMap`。 有关详细信息，请参阅数据收集中的[标识](./overview.md)。

## 何时使用FPID {#when-to-use}

浏览器限制可能会缩短Adobe用于识别回访访客的Cookie的生命周期。 如果您需要在组织拥有和控制的网站上拥有更持久的标识，FPID允许您管理自己的设备标识符并使用它来种子ECID。

使用Web SDK（包括Web SDK标记扩展）的Web实施支持FPID。 在以下情况下它们非常理想：您的主要目标是在组织拥有的域上实现更强大的身份持久性，或者您希望在拥有的Web资产上实现更好的报告和个性化连续性。 它们还允许您从控制的基础架构中设置和管理第一方Cookie。

当您的主要目标是跨多个域进行应用程序到Web切换或身份连续性时，FPID不是合适的工具。 对于这些方案，请参阅[移动到Web身份共享](./mobile-to-web.md)和[跨域共享](./cross-domain-sharing.md)。

使用FPID的好处包括：

* 对拥有的属性具有更强的持久性。
* 更好地控制设备标识符的生成和管理方式。
* 分析和个性化的持久基础。

使用FPID的权衡包括：

* 比依赖默认身份行为承担更多的实施责任。
* 在服务器端Cookie逻辑和数据收集配置之间进行协调。
* 用于确认标识符按预期使用的附加验证。

### 高级设置路径

1. 在您控制的基础架构上生成并管理第一方设备ID。
1. 将您的实施配置为从[第一方Cookie](#setting-cookie-datastreams)或[标识有效负载](#identityMap)读取该ID。
1. 验证回访访客是否会随着时间的推移在您拥有的资产上保持一致的身份。

## FPID的工作方式 {#how-fpids-work}

使用确定性算法将传递给Adobe Experience Cloud的FPID转换为ECID。 每次将相同的FPID发送到Edge Network时，都会从FPID中植入相同的ECID。 使用FPID为ECID设定种子后，该ECID将从`identityMap`中删除，并替换为生成的ECID。 FPID未存储在Adobe Experience Platform或Experience Cloud解决方案中。

当ECID和FPID都存在时，始终使用ECID首先标识用户。 此优先级划分可确保当浏览器Cookie存储中存在现有ECID时，该ECID仍保留为主要标识符，并且现有访客计数不会存在虚增风险。 对于现有用户，在ECID过期或因浏览器策略或手动操作而被删除之前，FPID不会成为主要身份。

身份按以下顺序排定优先级：

1. `identityMap`中包含的ECID
1. ECID存储在Cookie中
1. `identityMap`中包含的FPID
1. FPID存储在Cookie中

## 生成和设置FPID Cookie {#set-fpid-cookie}

Edge Network仅接受符合[UUIDv4格式](https://datatracker.ietf.org/doc/html/rfc4122)的ID。 不采用UUIDv4格式的设备ID将被拒绝。

* UUID具有唯一性和随机性，碰撞概率可以忽略不计。
* 无法使用IP地址或任何其他个人身份信息(PII)为UUIDv4设定种子。
* 用于生成UUID的库可用于每种编程语言。

### 服务器端Cookie设置 {#set-cookie-server}

通过您自己的服务器设置Cookie时，您可以使用各种方法帮助防止Cookie受浏览器策略限制：

* 使用服务器端脚本语言生成Cookie
* 设置Cookie以响应对子域或网站上的其他端点发出的API请求
* 使用内容管理系统(CMS)生成Cookie
* 使用内容交付网络(CDN)生成Cookie

当使用使用DNS [A记录](https://datatracker.ietf.org/doc/html/rfc1035)（对于IPv4）或[AAAA记录](https://datatracker.ietf.org/doc/html/rfc3596)（对于IPv6）而不是DNS `CNAME`或JavaScript代码的服务器设置第一方Cookie时，它们最有效。

>[!IMPORTANT]
>
>使用JavaScript的`document.cookie`方法（包括使用标记方法[`cookie.set()`](../tags/cookie.md)）设置的Cookie几乎永远不会受到限制Cookie持续时间的浏览器策略的保护。

请注意，仅支持`A`或`AAAA`记录来设置和跟踪Cookie。 数据收集的主要方法是通过DNS `CNAME`。 FPID是使用`A`或`AAAA`记录设置的，并使用`CNAME`发送到Adobe。 [Adobe管理的证书计划](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program)允许您为数据收集配置`CNAME`。

### 何时设置Cookie {#when-to-set-cookie}

在向Edge Network发送数据之前，最好先设置FPID Cookie。 如果您的实施在收集数据之前需要同意，请参阅[同意第一方设备ID](./consent.md#consent-with-fpids)，以获取有关协调FPID Cookie与您的同意流程的指导。 当您确保FPID可用于从第一个请求中为ECID设定种子时，访客虚增将会降低。 在不可能的情况下，仍会使用现有方法生成ECID，并在存在Cookie的情况下充当主标识符。 生成的FPID不会成为主标识符，直到ECID不再存在。 假设ECID最终受到浏览器删除策略的影响，而FPID没有受到影响，则FPID会在下次访问时成为主标识符，并用于在每次后续访问时为ECID提供种子。

### 设置到期 {#set-expiration}

Adobe建议仔细考虑FPID Cookie的生命周期。 确保将贵组织的隐私政策以及贵组织运营所在国家或地区的法律和政策考虑在内。 根据您组织的设置，您可以采用公司范围的Cookie设置策略，或根据您运营的每个区域设置中的用户而有所不同。 无论初始Cookie过期与否，请确保包含了在每次发生新网站访问时都会延长过期时间的逻辑。

### Cookie标记 {#cookie-flags}

有多个Cookie标记可影响在不同浏览器中处理Cookie的方式：

* **`HTTPOnly`**：无法使用客户端脚本访问使用`HTTPOnly`标志设置的Cookie。 这意味着，如果在设置FPID时设置了`HTTPOnly`标记，则必须使用服务器端脚本语言来读取包含在`identityMap`中的Cookie值。 如果您选择让Edge Network读取FPID Cookie的值，则设置`HTTPOnly`标志可确保客户端脚本无法访问该值，但不会对Edge Network读取Cookie的能力产生负面影响。 使用`HTTPOnly`标记不会影响可以限制Cookie生命周期的Cookie策略。 但是，在设置和读取FPID的值时，这仍然是需要考虑的事项。
* **`Secure`**：使用`Secure`属性设置的Cookie仅通过HTTPS协议以加密请求发送到服务器。 使用此标记有助于确保中间人攻击者无法轻松访问Cookie值。 如果可能，最好设置`Secure`标志。
* **`SameSite`**： `SameSite`属性允许服务器确定Cookie是否随跨站点请求一起发送。 属性提供了一些针对跨站点伪造攻击的保护。 存在三个可能的值： `Strict`、`Lax`和`None`。 请咨询您的内部团队，确定适合您组织的设置。 如果未指定`SameSite`特性，则某些浏览器的默认设置为`SameSite=Lax`。

## 将FPID发送到Edge Network {#send-fpid}

您可以通过两种方式将FPID发送到Edge Network：

* **[方法1](#setting-cookie-datastreams)**：为您的Web SDK调用配置`CNAME`，并在数据流配置中包含FPID Cookie的名称。
* **[方法2](#identityMap)**：在标识映射中包含FPID。

### 方法1：配置`CNAME`并在数据流中设置第一方ID Cookie {#setting-cookie-datastreams}

要从您自己的域设置FPID Cookie，您必须为Web SDK调用配置自己的`CNAME`，然后在数据流配置中启用第一方ID Cookie功能。 DNS中的`CNAME`记录允许您创建一个域名之间的别名。 此别名可使第三方服务看起来像您自己的域的一部分，使其Cookie看起来像第一方Cookie。 使用`CNAME`启用第一方数据收集后，将对数据收集端点发出的请求发送您域的所有Cookie。

1. 与Adobe合作创建一个`CNAME`记录以在您的组织内用于数据收集。 有关完整过程，请参阅[Adobe管理的证书计划](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert)。
1. 在数据流中启用&#x200B;**[!UICONTROL First Party ID Cookie]**&#x200B;选项。 此设置会告知Edge Network在查找第一方设备ID时引用指定的Cookie，而不是在身份映射中查找值。 在启用此设置时，必须提供预期存储FPID的Cookie的名称。 有关详细信息，请参阅[创建和配置数据流](/help/datastreams/configure.md#advanced-options)。

   ![平台UI图像，该图像显示了突出显示第一方ID Cookie设置的数据流配置](/help/collection/js/assets/first-party-id-datastreams.png)

### 方法2：在`identityMap`中使用FPID {#identityMap}

作为将FPID存储在您自己的Cookie中的替代方法，您可以通过身份映射将FPID发送到Edge Network。

以下是如何在`identityMap`中设置FPID的示例：

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

与其他标识类型一样，您可以将FPID与`identityMap`中的其他标识一起使用。 以下示例包含具有经过身份验证的CRM ID的FPID：

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": false
      }
    ],
    "EMAIL": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

如果在启用第一方数据收集时，FPID包含在Edge Network正在读取的Cookie中，则仅捕获经过身份验证的CRM ID：

```json
{
  "identityMap": {
    "EMAIL": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

以下`identityMap`导致Edge Network发出错误响应，因为它缺少FPID的`primary`指示器。 `identityMap`中存在的ID中至少有一个必须标记为`primary`。

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
        "id": "user@example.com",
        "authenticatedState": "authenticated"
      }
    ]
  }
}
```

## 迁移到FPID {#migrating-to-fpid}

如果您从以前的实施迁移到第一方设备ID，则可能很难在低级别看到过渡情况。 为了帮助说明此过程，请考虑一个涉及以前访问过您网站的客户的情形，以及FPID迁移将如何影响在Adobe解决方案中标识该客户。

![显示迁移至FPID后客户的ID值在两次访问之间更新的图表](/help/collection/js/assets/identity/tracking/visits.png)

| 访问 | 描述 |
| --- | --- |
| 首次访问 | 假设您尚未开始设置FPID Cookie。 [AMCV Cookie](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8)中包含的ECID是用于识别访客的标识符。 |
| 第二次访问 | 已开始推出FPID解决方案。 现有的ECID仍然存在，并且仍然是访客识别的主要标识符。 |
| 第三次访问 | 在第二次访问和第三次访问之间，经过了足够长的时间，即由于浏览器策略而删除了ECID。 但是，由于FPID是使用DNS `A`记录设置的，因此FPID仍然存在。 FPID现在被视为主ID，用于种子化ECID，然后将其写入最终用户设备。 该用户现在在Adobe Experience Platform和Experience Cloud解决方案中被视为新访客。 |
| 第四次访问 | 在第三次和第四次访问之间，由于浏览器策略而删除ECID已花费了足够多的时间。 与上次访问一样，FPID的设置方式仍然决定了它。 此时，会生成与上次访问相同的ECID。 在整个Adobe Experience Platform和Experience Cloud解决方案中，都会将该用户视为上次访问中的同一用户。 |
| 第五次访问 | 在第四次和第五次访问之间，最终用户清除浏览器中的所有Cookie。 将生成新的FPID，并使用它来创建新的ECID。 该用户现在在Adobe Experience Platform和Experience Cloud解决方案中被视为新访客。 |
