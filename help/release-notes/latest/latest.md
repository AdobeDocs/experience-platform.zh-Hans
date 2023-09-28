---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform 2023年9月版发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 2492651fb03e0bfc5c9f68a9b063689a1b9001a3
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 32%

---

# Adobe Experience Platform 发行说明

**发布日期：2023 年 9 月 28 日**

Adobe Experience Platform中的新增功能：

- [计算属性](#computed-attributes)

 Experience Platform 中现有功能的更新：

- [警报](#alerts)
- [数据收集](#data-collection)
- [身份服务](#identity-service)
- [Segmentation Service](#segmentation)
- [源](#sources)

## 计算属性 {#computed-attributes}

计算属性启用通过直观UI将事件数据轻松总结为配置文件属性的功能，以增强基于行为的分段、个性化和激活。 借助此功能，您可以以自助方式创建计算属性，管理这些属性，并在分段、Real-Time CDP目标或Adobe Journey Optimizer中使用这些属性。 此外，计算属性可简化分段和历程工作流，以帮助您无缝地提供相关体验。 要了解有关计算属性的更多信息，请阅读 [计算属性概述](../../profile/computed-attributes/overview.md).

## 警报 {#alerts}

Experience Platform允许您订阅各种Platform活动的基于事件的警报。 您可以通过订阅不同的警报规则 [!UICONTROL 警报] 选项卡中，并且可以选择在UI本身中或通过电子邮件通知接收警报消息。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| “警报历史记录”选项卡 | 警报 [!UICONTROL 历史记录] 选项卡现在将包括所有事件，包括延迟、开始、成功和失败。 阅读 [警报UI文档](../../observability/alerts/ui.md) 有关“历史记录”选项卡的详细信息。 |

{style="table-layout:auto"}

要了解有关警报的更多信息，请阅读 [[!DNL Observability Insights] 概述](../../observability/home.md).

## 数据收集 {#data-collection}

Adobe Experience Platform 提供一套技术，通过这些技术，可收集客户端客户体验数据，并将它发送到 Adobe Experience Platform Edge Network，从中可充实、转换数据和将数据分发到 Adobe 或非 Adobe 目标。

**新增功能或更新后的功能**

| 类型 | 功能 | 描述 |
| --- | --- | --- |
| 数据流 | 设备查找支持 | 在配置数据流时，您现在可以选择要收集的设备查找信息的级别。 设备查找信息包括有关用于与页面交互的设备、硬件、操作系统和浏览器的数据。 <br>  无法收集设备查找信息以及用户代理和客户端提示。 选择收集设备信息将禁用用户代理和客户端提示的收集，反之亦然。 所有设备查找信息都存储在 `xdm:device` 字段组。 从文档了解有关 [配置数据流](../../datastreams/configure.md#geolocation-device-lookup). |
| 扩展 | [!DNL TikTok] Web事件API扩展 | 此 [[!DNL TikTok] Web事件API](https://exchange.adobe.com/apps/ec/109834/tiktok-web-events-api) 通过扩展，您可以利用在Adobe Experience Platform Edge Network中捕获的数据并将其发送至 [!DNL TikTok] 以服务器端事件的形式使用 [!DNL TikTok] Web事件API。 |

{style="table-layout:auto"}

要了解有关数据收集的更多信息，请阅读 [数据收集概述](../../tags/home.md).

## 身份服务 {#identity-service}

Adobe Experience Platform 身份服务通过跨设备和系统桥接身份，使您能够全面了解您的客户及其行为，助您实时提供有影响力的个人数字体验。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| Identity Service UI增强功能 | 使用Experience PlatformUI中改进的自定义命名空间创建工具，更好地管理自定义命名空间及其相应的身份类型。 增强的Identity Service UI为您提供： <ul><li>上下文体验：视觉提示、清晰度，以及身份命名空间和身份类型的上下文。</li><li>准确性：更好地处理错误，不再有重复的标识名称。</li><li>可发现性：可在产品内对话框中访问文档。</li></ul> 有关详细信息，请阅读上的指南 [创建自定义命名空间](../../identity-service/namespaces.md#create-namespaces). |
| 标识图形限制的更改 | 标识图限制已从150个标识更改为50个标识。 将新身份摄取到完整图形中时，将删除基于摄取时间戳和身份类型的最旧身份。 Cookie标识类型按优先顺序删除。 Adobe如果您的生产沙盒包含： <ul><li>自定义命名空间，其中人员标识符（例如 CRM ID）会被配置为 cookie/设备标识类型。</li><li>自定义命名空间，其中 cookie/设备标识符会被配置为跨设备标识类型。</li></ul> Adobe 工程人员会手动处理这些请求。若要了解更多信息，请阅读[标识服务数据的护栏](../../identity-service/guardrails.md)。 |

{style="table-layout:auto"}

要了解有关Identity Service的更多信息，请阅读 [Identity服务概述](../../identity-service/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 允许您对存储在 [!DNL Experience Platform] 中的与个人（例如客户、潜在客户、用户或组织）相关的数据划分到受众区段中。您可以通过区段定义或其他源从 [!DNL Real-Time Customer Profile] 数据创建受众。这些受众在 [!DNL Platform] 上集中配置和维护，并且可以通过任何 Adobe 解决方案轻松访问。

**新增功能或更新后的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 可自定义的列 | 您现在可以使用可缩放的列来自定义受众门户的布局。 有关此功能的详细信息，请阅读 [分段UI指南](../../segmentation/ui/overview.md#customize). |
| 更新频率细分 | 您现在可以查看组织中受众更新频率的细分。 有关此功能的详细信息，请阅读 [分段UI指南](../../segmentation/ui/overview.md#browse). |

要了解有关来源的更多信息，请阅读 [源概述](../../sources/home.md).

要了解有关分段服务的更多信息，请阅读 [分段服务概述](../../segmentation/home.md).

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 的新参数 `offset` 自助源中的分页（批处理SDK） | 您现在可以指定 `endConditionName` 和 `endConditionValue` 使用时用于您的源 `offset` 分页。 利用这些参数，可指示将在下一个HTTP请求中结束分页循环的条件。 欲知更多信息，请参阅 [自助源分页指南（批处理SDK）](../../sources/sources-sdk/config/sourcespec.md#pagination). |

{style="table-layout:auto"}

要了解有关来源的更多信息，请阅读 [源概述](../../sources/home.md).