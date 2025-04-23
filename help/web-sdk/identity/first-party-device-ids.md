---
title: 在Web SDK中使用第一方设备ID
description: 了解如何在Adobe Experience Platform Web SDK中配置第一方设备ID (FPID)。
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: c7be2fff2cd94677b745e6ed095454bc46f8a37b
workflow-type: tm+mt
source-wordcount: '2181'
ht-degree: 0%

---


# 在Web SDK中使用第一方设备ID

Adobe Experience Platform Web SDK使用Cookie为网站访客分配[Adobe Experience Cloud ID (ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html)以跟踪用户行为。 要消除浏览器对Cookie有效期的限制，您可以设置和管理自己的设备标识符，称为第一方设备ID (FPID)。

>[!NOTE]
>
>仅当通过Web SDK向Experience Platform Edge Network发送数据时，才支持第一方设备ID。

>[!IMPORTANT]
>
>第一方设备ID与Web SDK中的[第三方Cookie](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#identity)功能不兼容。 您可以使用第一方设备ID或第三方Cookie，但不能同时使用两者。

## 先决条件 {#prerequisites}

在开始之前，请确保您熟悉身份数据在Web SDK中的工作方式，包括ECID和`identityMap`。 有关详细信息，请参阅Web SDK](./overview.md)中有关[身份数据的概述。

## 第一方设备ID格式要求 {#formatting-requirements}

Edge Network仅接受符合[UUIDv4格式](https://datatracker.ietf.org/doc/html/rfc4122)的ID。 将拒绝不采用UUIDv4格式的设备ID。

* [!DNL UUIDs]是唯一的、随机的，发生冲突的概率可以忽略不计。
* 无法使用IP地址或任何其他个人身份信息(PII)为[!DNL UUIDv4]设定种子。
* 用于生成[!DNL UUIDs]的库可用于每种编程语言。

## 使用您自己的服务器设置[!DNL FPID] Cookie {#set-cookie-server}

通过您自己的服务器设置Cookie时，您可以使用各种方法防止Cookie因浏览器策略而受到限制：

* 使用服务器端脚本语言生成Cookie
* 设置Cookie以响应对子域或网站上的其他端点发出的API请求
* 使用[!DNL CMS]生成Cookie
* 使用[!DNL CDN]生成Cookie

此外，您应始终在域的`A`记录下设置FPID Cookie。

>[!IMPORTANT]
>
>使用JavaScript的`document.cookie`方法设置的Cookie几乎永远不会受到浏览器策略的保护，这些策略会限制Cookie的持续时间。

### 何时设置Cookie {#when-to-set-cookie}

最好在向Edge Network发出任何请求之前设置[!DNL FPID] Cookie。 但是，在无法实现的情况下，[!DNL ECID]仍将使用现有方法生成，并充当主要标识符，前提是Cookie存在。

假设[!DNL ECID]最终受到浏览器删除策略的影响，但[!DNL FPID]未受到影响，则[!DNL FPID]将在下次访问时成为主要标识符，并用于在每次后续访问时为[!DNL ECID]设定种子。

### 设置Cookie的过期时间 {#set-expiration}

在实施[!DNL FPID]功能时，应仔细考虑设置Cookie的过期时间。 在做出决定时，您应该考虑贵组织运营的国家或地区以及其中每个地区的法律和政策。

作为此决策的一部分，您可能希望采用全公司Cookie设置策略，或根据您运营的每个区域设置中的用户而有所不同。

无论您为Cookie的初始过期时间选择的设置如何，都必须确保包含每次发生对网站的新访问时都会延长Cookie过期时间的逻辑。

## Cookie标记的影响 {#cookie-flag-impact}

有各种Cookie标记会影响Cookie在不同浏览器中的处理方式：

* [&#39;HTTPOnly&#39;](#http-only)
* [&#39;安全&#39;](#secure)
* [&#39;SameSite&#39;](#same-site)

### `HTTPOnly` {#http-only}

无法使用客户端脚本访问使用`HTTPOnly`标志设置的Cookie。 这意味着，如果在设置[!DNL FPID]时设置了`HTTPOnly`标记，则必须使用服务器端脚本语言来读取包含在`identityMap`中的Cookie值。

如果您选择让Edge Network读取[!DNL FPID] Cookie的值，则设置`HTTPOnly`标志可确保任何客户端脚本均无法访问该值，但不会对Edge Network读取Cookie的能力产生任何负面影响。

>[!NOTE]
>
>使用`HTTPOnly`标记不会影响可能会限制Cookie生命周期的Cookie策略。 但是，在设置并读取[!DNL FPID]的值时，您仍应考虑它。

### `Secure` {#secure}

使用`Secure`属性设置的Cookie仅通过[!DNL HTTPS]协议以加密请求发送到服务器。 使用此标记有助于确保中间人攻击者无法轻松访问Cookie的值。 如果可能，最好设置`Secure`标志。

### `SameSite` {#same-site}

`SameSite`属性允许服务器确定是否随跨站点请求一起发送Cookie。 属性提供了一些针对跨站点伪造攻击的保护。 存在三个可能的值： `Strict`、`Lax`和`None`。 请咨询您的内部团队，确定适合您组织的设置。

如果未指定`SameSite`特性，则某些浏览器的默认设置现在为`SameSite=Lax`。

## ID层次结构 {#id-hierarchy}

当[!DNL ECID]和[!DNL FPID]都存在时，将优先考虑[!DNL ECID]来标识用户。 这样可以确保当浏览器Cookie存储中存在现有的[!DNL ECID]时，它仍然是主要标识符，并且现有访客计数不会受到影响。 对于现有用户，在[!DNL ECID]过期或因浏览器策略或手动过程而被删除之前，[!DNL FPID]不会成为主标识。

身份按以下顺序排定优先级：

1. [!DNL ECID]包含在`identityMap`中
1. [!DNL ECID]存储在Cookie中
1. [!DNL FPID]包含在`identityMap`中
1. [!DNL FPID]存储在Cookie中


## 迁移到第一方设备ID {#migrating-to-fpid}

如果您从以前的实施迁移到第一方设备ID，则可能很难在低级别上直观显示过渡情况。

为了帮助说明此过程，请考虑一个涉及以前访问过您网站的客户的情形，以及[!DNL FPID]迁移将如何影响在Adobe解决方案中识别该客户。

![显示迁移至FPID后客户的ID值在两次访问之间更新的图表](../assets/identity/tracking/visits.png)

>[!IMPORTANT]
>
>`ECID` Cookie的优先级始终高于`FPID`。

| 前往 | 描述 |
| --- | --- |
| 首次访问 | 假设您尚未开始设置[!DNL FPID] Cookie。 [AMCV Cookie](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8)中包含的[!DNL ECID]将是用于识别访客的标识符。 |
| 第二次访问 | [!DNL FPID]解决方案的转出已开始。 现有[!DNL ECID]仍然存在，并且仍然是访客标识的主要标识符。 |
| 第三次访问 | 在第二次和第三次访问之间，由于浏览器策略，已经过了足够的时间删除[!DNL ECID]。 但是，由于[!DNL FPID]是使用[!DNL DNS] [!DNL A]记录设置的，因此[!DNL FPID]仍然存在。 [!DNL FPID]现在被视为主ID，用于为写入最终用户设备的[!DNL ECID]提供种子。 该用户现在在Adobe Experience Platform和Experience Cloud解决方案中将被视为新访客。 |
| 第四次访问 | 在第三次和第四次访问之间，经过了足够长的时间，由于浏览器策略，[!DNL ECID]已被删除。 与上次访问一样，[!DNL FPID]仍因设置方式而异。 此时，将生成与上次访问相同的[!DNL ECID]。 整个Experience Platform和Experience Cloud解决方案中都会将该用户视为上次访问中的同一用户。 |
| 第五次访问 | 在第四次和第五次访问之间，最终用户清除了其浏览器中的所有Cookie。 已生成新[!DNL FPID]，并用它来创建新[!DNL ECID]。 该用户现在在Adobe Experience Platform和Experience Cloud解决方案中将被视为新访客。 |

{style="table-layout:auto"}

## 使用第一方设备ID (FPID) {#using-fpid}

第一方设备ID ([!DNL FPIDs])使用第一方Cookie跟踪访客。 当使用使用DNS [A记录](https://datatracker.ietf.org/doc/html/rfc1035)（对于IPv4）或[AAAA记录](https://datatracker.ietf.org/doc/html/rfc3596)（对于IPv6）而不是DNS [!DNL CNAME]或[!DNL JavaScript]代码的服务器设置第一方Cookie时，它们最有效。

>[!IMPORTANT]
>
>仅支持[!DNL A]或[!DNL AAAA]记录来设置和跟踪Cookie。 数据收集的主要方法是通过[!DNL DNS CNAME]。 [!DNL FPIDs]是使用[!DNL A]或[!DNL AAAA]记录设置的，并使用[!DNL CNAME]发送到Adobe。
>
>第一方数据收集还支持[Adobe管理的证书计划](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program)。

设置[!DNL FPID] Cookie后，在收集事件数据时，可以获取其值并将其发送到Adobe。 收集的[!DNL FPIDs]用于生成[!DNL ECIDs]，它们是Adobe Experience Cloud应用程序中的主要标识符。

您可以通过两种方式使用[!DNL FPIDs]：

* **[方法1](#setting-cookie-datastreams)**：为您的Web SDK调用配置[!DNL CNAME]，并在数据流配置中包含[!DNL FPID] Cookie的名称。
* **[方法2](#identityMap)**：在标识映射中包含[!DNL FPID]。 有关详细信息，请参阅本文档中有关在`identityMap`](#identityMap)中使用FPID的[的更详细部分。

### 方法1：为Web SDK调用配置CNAME，并在数据流中设置第一方ID Cookie {#setting-cookie-datastreams}

要从您自己的域设置[!DNL FPID] Cookie，您需要为Web SDK调用配置您自己的[!DNL CNAME] （规范名称），然后在数据流配置中启用[!DNL First Party ID Cookie]功能。

**步骤 1. 为Web SDK部署域**&#x200B;配置CNAME

DNS中的[!DNL CNAME]记录允许您创建一个域名之间的别名。 这有助于使第三方服务看起来像是您自己的域的一部分，从而使其Cookie看起来像第一方Cookie。

**示例**

假设您想在网站`mywebsite.com`上实施Web SDK。 Web SDK将数据发送到`edge.adobedc.net`域的Edge Network。

| 不带[!DNL CNAME] | 与[!DNL CNAME] |
|---------|----------|
| <ul><li>您的网站`mywebsite.com`使用Web SDK域`edge.adobedc.net`将数据发送到Edge Network。</li><li>由`edge.adobedc.net`设置的Cookie被视为第三方Cookie，因为它们并非来自您的`mywebsite.com`域。 根据您的用户浏览器，第三方Cookie可能会被阻止，并且您的数据无法访问Edge Network。</li></ul> | <ul><li>创建一个部署Web SDK的子域，如`metrics.mywebsite.com`。</li><li>您在DNS系统中设置了[!DNL CNAME]记录，以便`metrics.mywebsite.com`指向`edge.adobedc.net`。</li><li>当您的网站通过`metrics.mywebsite.com`设置Cookie到浏览器时，它们将显示为来自`mywebsite.com` （第一方）而不是`edge.adobedc.net` （第三方）。 这降低了第一方ID Cookie被阻止的可能性，从而确保更准确的数据收集。</li></ul> |

使用[!DNL CNAME]启用第一方数据收集后，将对向数据收集端点发出的请求发送您域的所有Cookie。

要使用此功能，您需要在域的顶级设置[!DNL FPID] Cookie，而不是在特定的子域设置。 如果您在子域中设置它，则Cookie值将不会发送到Edge Network，[!DNL FPID]解决方案将不会按预期工作。

>[!IMPORTANT]
>
>此功能要求您启用[第一方数据收集](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=en)。

**步骤 2. 为您的数据流启用**[!UICONTROL &#x200B;第一方ID Cookie ]**功能**

配置CNAME后，必须为数据流启用&#x200B;**[!UICONTROL 第一方ID Cookie]**&#x200B;选项。 此设置会告知Edge Network在查找第一方设备ID时引用指定的Cookie，而不是在[标识映射](#identityMap)中查找此值。

请参阅[数据流配置文档](../../datastreams/configure.md#advanced-options)以了解如何设置数据流。

有关第一方Cookie如何与Adobe Experience Cloud配合使用的更多详细信息，请参阅有关[第一方Cookie](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=zh-Hans)的文档。

![平台UI图像，该图像显示了突出显示第一方ID Cookie设置的数据流配置](../assets/first-party-id-datastreams.png)

在启用此设置时，必须提供预期存储[!DNL FPID]的Cookie的名称。

>[!NOTE]
>
>使用第一方ID时，无法执行第三方ID同步。 第三方ID同步依赖于[!DNL Visitor ID]服务以及该服务生成的`UUID`。 使用第一方ID功能时，生成[!DNL ECID]时未使用[!DNL Visitor ID]服务，这会导致无法同步第三方ID。
><br> 当您使用第一方ID时，由于Audience Manager合作伙伴ID同步主要基于`UUIDs`或`DIDs`，因此不支持在合作伙伴平台中激活的[Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager)功能。 从第一方ID派生的[!DNL ECID]未链接到`UUID`，使其不可寻址。

## 方法2：在`identityMap`中使用FPID {#identityMap}

作为将[!DNL FPID]存储在您自己的Cookie中的替代方法，您可以通过身份映射将[!DNL FPID]发送到Edge Network。

以下是如何在`identityMap`中设置[!DNL FPID]的示例：

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

与其他标识类型一样，您可以在`identityMap`中包含[!DNL FPID]和其他标识。 以下是经过身份验证的[!DNL CRM ID]所包含的[!DNL FPID]的示例：

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
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

如果启用第一方数据收集时，如果[!DNL FPID]包含在Edge Network正在读取的Cookie中，则应当仅捕获经过身份验证的[!DNL CRM ID]：

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

以下`identityMap`将导致来自Edge Network的错误响应，因为它缺少[!DNL FPID]的`primary`指示器。 `identityMap`中存在的ID中至少有一个必须标记为`primary`。

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

在这种情况下，Edge Network返回的错误响应将类似于以下内容：

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

## 常见问题解答 {#faq}

以下是有关第一方设备ID的常见问题解答列表。

### 植入ID与仅生成ID有何不同？

种子设定的概念是唯一的，因为传递到Adobe Experience Cloud的[!DNL FPID]使用确定性算法转换为[!DNL ECID]。 每次将相同的[!DNL FPID]发送到Edge Network时，相同的[!DNL ECID]都是从[!DNL FPID]中植入的。

### 何时应生成第一方设备ID？

为了减少潜在的访客虚增，应在使用Web SDK发出您的第一个请求之前生成[!DNL FPID]。 但是，如果您无法执行此操作，仍将为该用户生成[!DNL ECID]，并将用作主要标识符。 在[!DNL ECID]不再存在之前，生成的[!DNL FPID]不会成为主标识符。

### 哪些数据收集方法支持第一方设备ID？

当前仅Web SDK支持第一方设备ID。

### 第一方设备ID是否存储在任何Platform或Experience Cloud解决方案上？

使用[!DNL FPID]为[!DNL ECID]设定种子后，它将从`identityMap`中删除，并替换为已生成的[!DNL ECID]。 [!DNL FPID]未存储在任何Adobe Experience Platform或Experience Cloud解决方案中。
