---
title: Cloud Connector扩展概述
description: 了解Adobe Experience Platform中的Cloud Connector事件转发扩展。
exl-id: f3713652-ac32-4171-8dda-127c8c235849
source-git-commit: e832694fed5dbb86b5ed544473d6a79e500a6222
workflow-type: tm+mt
source-wordcount: '1716'
ht-degree: 68%

---

# Cloud Connector扩展概述

>[!NOTE]
>
>经过品牌重塑，Adobe Experience Platform Launch 已变为 Adobe Experience Platform 中的一套数据收集技术。因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

Cloud Connector事件转发扩展允许您创建自定义HTTP请求，以将数据发送到目的地或从目的地检索数据。 云连接器扩展类似于在 Adobe Experience Platform Edge Network 上部署了邮递员，可用来将数据发送到尚未具备专用扩展的端点。

使用本参考可了解有关使用此扩展构建规则时可用的选项的信息。

## 云连接器扩展操作类型

这部分介绍在 Adobe Experience Platform 云连接器扩展中可用的“发送数据”操作类型。

### 请求类型

要选择终结点所需的请求类型，请在[!UICONTROL 请求类型]下拉列表下选择相应的类型。

| 方法 | 描述 |
|---|---|
| [GET](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/GET) | 请求指定资源的表示形式。使用 GET 的请求只能检索数据。 |
| [POST](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/POST) | 将实体提交到指定的资源，通常会导致服务器的状态发生变化或产生副作用。 |
| [PUT](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/PUT) | 将目标资源的所有当前表示形式替换为请求负载。 |
| [PATCH](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/PATCH) | 对资源施加部分修改。 |
| [DELETE](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/DELETE) | 删除指定的资源。 |

### 端点 URL

在“Request Type”下拉菜单旁边的文本字段中，可输入您要向其发送数据的端点的 URL。

### 查询参数、标头和正文配置

使用这些选项卡（Query Params、Headers 和 Body Data Elements）中的每一个，可以控制要将哪些数据发送到既定端点。

#### 查询参数

为每一个要作为查询字符串参数发送的键值对定义键和值。要手动输入数据元素，请使用大括号数据元素标记进行事件转发。 要将名为“siteSection”的数据元素的值引用为键或值，请输入 `{{siteSection}}`。或者，通过在下拉菜单中选择数据元素来选择以前创建的数据元素。

要添加更多查询参数，请选择&#x200B;**[!UICONTROL 添加其他]**。

#### 标头

为每一个要作为标头发送的键值对定义键和值。要手动输入数据元素，请使用大括号数据元素标记进行事件转发。 要将名为“pageName”的数据元素的值引用为键或值，请输入 `{{pageName}}`。或者，通过在下拉菜单中选择数据元素来选择以前创建的数据元素。

要添加更多标头，请选择&#x200B;**[!UICONTROL 添加其他]**。

下表列出了预定义的标头。您不仅可以使用这些标头，而且还可以根据需要添加您自己的自定义标头，但是这些标头应出于为您带来方便的目的而添加。

>[!NOTE]
>
>有关这些标头的更多详细信息，请访问 [https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers)。

| 标头 | 描述 |
|---|---|
| [A-IM](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Accept) | |
| [Accept](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Accept) | |
| [Accept-Charset](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Accept-Charset) | |
| [Accept-Encoding](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Accept-Encoding) | |
| [Accept-Language](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Accept-Language) | |
| [Accept-Datetime](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Accept) | 由用户代理传输，旨在表明它需要访问原始资源的过去状态。为了实现这个目的，应当在发出的 HTTP 请求中，根据原始资源的 TimeGate 传递 `Accept-Datetime` 标头，该标头的值用来表明所希望获得的原始资源过去状态的日期时间。 |
| Access-Control-Request-Headers | 在发出[预检请求](https://developer.mozilla.org/zh-CN/docs/Glossary/preflight_request)时浏览器使用的标头，旨在告知服务器当生成真正的请求时将会使用的 [HTTP 标头](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers)。 |
| Access-Control-Request-Method | 在发出[预检请求](https://developer.mozilla.org/zh-CN/docs/Glossary/preflight_request)时浏览器使用的标头，旨在告知服务器当生成真正的请求时将会使用的 [HTTP 方法](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods)。这是必需的标头，因为预检请求始终是一种 [OPTION](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/OPTIONS) 方法，与实际请求使用的方法不同。 |
| Authorization | 包含用于验证服务器用户代理的凭据。 |
| [Cache-Control](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Cache-Control) | 用于缓存请求和响应机制的指令。 |
| [Connection](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Connection) | 控制在当前事务完成后是否将网络连接保持打开状态。 |
| [Content-Length](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Length) | 以十进制字节数表示的资源大小。 |
| [Content-Type](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Type) | 指示资源的媒体类型。 |
| Cookie | 包含服务器此前使用 [`Set-Cookie`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Set-Cookie) 标头发送的、且存储在 [HTTP Cookie](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Cookies) 中的内容。 |
| Date | 常规 HTTP 标头，其中包含发起消息时的日期和时间。 |
| [DNT](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/DNT) | 表示用户的跟踪首选项。 |
| Expect | 表明一些期望，指出为了正确处理请求，需要由服务器来执行。 |
| Forwarded | 包含来自[反向代理服务器](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Proxy_servers_and_tunneling)的信息，当请求路径中涉及代理时，该信息会发生更改或丢失。 |
| From | 包含人工用户的 Internet 电子邮件地址，该用户可控制如何申请用户代理。 |
| Host | 指定请求所发往的服务器的主机和端口号。 |
| If-Match | |
| If-Modified-Since | |
| [If-None-Match](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/If-None-Match) | |
| [If-Range](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/If-Range) | |
| [If-Unmodified-Since](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/If-Unmodified-Since) | |
| [Max-Forwards](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/If-Unmodified-Since) | |
| [Origin](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Origin) | |
| [Pragma](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Pragma) | 特定于实施的标头，可能会在请求-响应链的任意阶段产生各种影响。由于 HTTP/1.0 高速缓存尚无 Cache-Control 标头，因此为了与之保持向后兼容性而使用该标头。 | |
| [Proxy-Authorization](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Proxy-Authorization) |
| [Range](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Range) | 指示服务器应返回的部分文档。 | |
| [Referer](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Referer) | 上一个网页的地址；正是通过该网页，跟踪了一个指向当前申请页面的链接。 | |
| TE | 指定用户代理愿意接受的传输编码。（为了更加直观，您可以将其随意命名为 `Accept-Transfer-Encoding`）。 |
| Upgrade | [`Upgrade` 标头字段的相关 RFC 文档为 RFC 7230，具体内容位于第 6.7 部分](https://tools.ietf.org/html/rfc7230#section-6.7)。该标准设立了有关在当前客户端、服务器、传输协议连接方面升级或更改为不同协议的规则。例如，此标头标准允许客户端从 HTTP 1.1 更改为 HTTP 2.0，前提是服务器决定确认并实施 `Upgrade` 标头字段。客户端和服务器均不必接受 `Upgrade` 标头字段中指定的条款。它可以用在客户端和服务器标头中。如果指定了 `Upgrade` 标头字段，那么发送方还必须发送一个指定了 `upgrade` 选项的 `Connection` 标头字段。 | |
| [User-Agent](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/User-Agent) | 包含一个特征字符串，该字符串允许网络协议对等方围绕请求软件用户代理，识别其应用程序类型、操作系统、软件供应商或软件版本。 |
| [Via](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Via) | 由正向代理和反向代理添加，并且可以显示在请求标头和响应标头中。 |
| [Warning](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Warning) | 关于可能会出现的问题的一般警告信息。 |
| X-CSRF-Token | |
| X-Requested-With | |

#### 以 JSON 格式显示正文

为每一个要在请求正文中发送的键值对定义键和值。要手动输入数据元素，请使用大括号数据元素标记进行事件转发。 要将名为“appSection”的数据元素的值引用为键或值，请输入 `{{appSection}}`。或者，通过在下拉菜单中选择数据元素来选择以前创建的数据元素。

要添加其他键值对，请选择&#x200B;**[!UICONTROL 添加其他]**。

#### 以 Raw 格式显示正文

为每一个要在请求正文中发送的键值对定义键和值。要手动输入数据元素，请使用大括号数据元素标记进行事件转发。 要将名为“appSection”的数据元素的值引用为键或值，请输入 `{{appSection}}`。或者，通过在下拉菜单中选择数据元素来选择以前创建的数据元素。您可以添加一个或多个数据元素。

### 高级

事件转发中规则内的操作按顺序执行。 在某些情况下，您需要检索的数据可能来自客户端传入事件上一个并不存在的外部源，那么系统在进行响应时，会将该数据转换或发送至单个规则中某个后续操作的最终目的地。高级部分中的“Save the request response”可启用此功能。

要保存来自端点的响应正文，请选中&#x200B;**[!UICONTROL 保存请求响应]**&#x200B;框并在文本字段中定义响应键。

如果将响应键定义为 `productDetails`，请在数据元素中引用此数据，然后在同一规则的后续操作中引用此数据元素。要创建引用 `productDetail` 的数据元素，请创建一个类型为 `path` 的数据元素并输入以下路径：

```Json
arc.ruleStash.[EXTENSION-NAME-HERE].responses.[RESPONSE-KEY-HERE] 

arc.ruleStash.adobe-cloud-connector.reponses.productDetails 
```

## 将相互传输层安全性([!DNL mTLS])规则添加到事件转发库 {#mtls-rules}

[!DNL mTLS]证书是数字凭据，用于证明安全通信中服务器或客户端的身份。 当您使用[!DNL mTLS]服务API时，这些证书可帮助您验证并加密与Adobe Experience Platform事件转发的交互。 此过程不仅可以保护您的数据，还可以确保每个连接都来自可信合作伙伴。

### 安装Adobe云连接器扩展 {#install}

若要安装该扩展，请[创建事件转发属性](../../../ui/event-forwarding/overview.md#properties)或选择现有属性进行编辑。

在左侧面板中选择&#x200B;**[!UICONTROL 扩展]**。 在&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡中，选择&#x200B;**[!UICONTROL Adobe Cloud Connector]**&#x200B;卡，然后选择&#x200B;**[!UICONTROL 安装]**。

![扩展目录显示[!DNL Adobe Cloud Connector]扩展卡突出显示安装。](../../../images/extensions/server/cloud-connector/install-extension.png)

### 配置事件转发规则 {#rule}

>[!NOTE]
>
>要将规则配置为使用[!DNL mTLS]，您必须安装Adobe Cloud Connector版本1.2.4或更高版本。

安装该扩展后，您可以创建一个使用[!DNL mTLS]的事件转发规则，并将其添加到库中。

在事件转发属性中创建新事件转发[规则](../../../ui/managing-resources/rules.md)。 提供规则的名称，然后在&#x200B;**[!UICONTROL 操作]**&#x200B;下添加新操作并将扩展设置为&#x200B;**[!UICONTROL Adobe Cloud Connector]**。 接下来，为&#x200B;**[!UICONTROL 操作类型]**&#x200B;选择&#x200B;**[!UICONTROL 提取调用]**。

![事件转发属性规则视图，突出显示添加事件转发规则操作配置所需的字段。](../../../images/extensions/server/cloud-connector/event-action.png)

作出选择后，将显示其他控件，以配置[!DNL mTLS]请求的方法和目标。 若要在环境中启用使用活动证书，请选择&#x200B;**[!UICONTROL 在[!DNL mTLS]]**&#x200B;中启用，然后选择&#x200B;**[!UICONTROL 保留更改]**&#x200B;以保存规则。

![Event Forwarding Property Rules视图，带有其他控制字段并保持突出显示的更改。](../../../images/extensions/server/cloud-connector/save-rule.png)

您的新规则现已准备就绪。 选择&#x200B;**[!UICONTROL 保存到库]**，然后选择&#x200B;**[!UICONTROL 生成]**&#x200B;以部署它。 [!DNL mTLS]请求现在处于活动状态，并可在库中找到。

![突出显示了save to library and build的事件转发规则。](../../../images/extensions/server/cloud-connector/save-build.png)

## 后续步骤

本指南介绍了如何在事件转发中设置mTLS规则。 有关为环境设置mTLS的详细信息，请参阅[相互传输层安全性([!DNL mTLS])指南](../cloud-connector/mtls.md)。

有关Experience Platform中事件转发功能的更多信息，请参阅[事件转发概述](../../../ui/event-forwarding/overview.md)。
