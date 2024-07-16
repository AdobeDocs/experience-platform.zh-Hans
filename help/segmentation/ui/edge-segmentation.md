---
solution: Experience Platform
title: Edge Segmentation UI指南
description: 了解如何使用边缘分段在边缘即时评估Platform中的区段定义，启用同一页面和下一页面个性化用例。
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: c14c6b8037993b3696b4a99633c80c6ee9679399
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 0%

---

# 边缘分段 UI 指南

>[!NOTE]
>
>Edge分段现在通常可供所有Platform用户使用。 如果您在测试版中创建了边缘区段定义，则这些区段定义将继续有效。

Edge分段功能能够在边缘](../../web-sdk/home.md)上即时评估Adobe Experience Platform中的区段[，从而启用同一页面和下一页面个性化用例。

>[!IMPORTANT]
>
> 边缘数据将存储在距离收集位置最近的边缘服务器位置，并且可能会存储在指定为Adobe Experience Platform数据中心中心（或主体）的位置以外的位置。
>
> 此外，边缘分段引擎将仅在具有&#x200B;**一个**&#x200B;主标记身份的边缘上处理请求，这与不基于边缘的主身份一致。

## Edge分段查询类型 {#query-types}

当前只有选定的查询类型可使用边缘分段进行评估。 以下部分提供了可通过边缘分段评估的查询类型以及当前不支持的查询类型列表。

如果查询符合下表列出的任何标准，则可以使用边缘分段进行评估。

>[!NOTE]
>
>如果查询与下表中的任何查询类型匹配，则将使用边缘分段自动评估该查询。 系统会根据查询表达式自动确定此功能。

| 查询类型 | 详细信息 | 示例 | PQL示例 |
| ---------- | ------- | ------- | ----------- |
| 单个事件 | 任何引用没有时间限制的单个传入事件的区段定义。 | 将项目添加到购物车的人员。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| 单个配置文件 | 任何引用单个纯配置文件属性的区段定义 | 住在美国的人。 | `homeAddress.countryCode = "US"` |
| 引用用户档案的单个事件 | 任何引用一个或多个用户档案属性和单个传入事件的区段定义，无时间限制。 | 在美国居住的人访问了该主页。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")])` |
| 否定了具有配置文件属性的单个事件 | 任何引用带反义的单个传入事件和一个或多个用户档案属性的区段定义 | 居住在美国且&#x200B;**未**&#x200B;访问过主页的人。 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| 时间范围内的单个事件 | 任何引用一段时间内单个传入事件的区段定义。 | 过去24小时内访问过主页的人。 | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)])` |
| 在相对时间范围小于24小时内的配置文件属性为单个事件 | 任何涉及单个传入事件（具有一个或多个用户档案属性）且发生在小于24小时的相对时间范围内的区段定义。 | 居住在美国的人在过去24小时内访问了该主页。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)])` |
| 在一个时间范围内否定了具有配置文件属性的单个事件 | 任何引用一段时间内一个或多个用户档案属性和否定单个传入事件的区段定义。 | 居住在美国且&#x200B;**不**&#x200B;的人在过去24小时内访问了主页。 | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]))` |
| 24小时时间范围内的频率事件 | 任何涉及在24小时的时间范围内发生特定次数的事件的区段定义。 | 过去24小时内访问过主页&#x200B;**至少**&#x200B;五次的用户。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 在24小时时间范围内具有配置文件属性的频率事件 | 任何区段定义，它是指一个或多个用户档案属性以及在24小时的时间范围内发生特定次数的事件。 | 过去24小时内访问过主页&#x200B;**至少**&#x200B;五次的美国人。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 在24小时时间范围内具有配置文件的否定频率事件 | 任何引用一个或多个用户档案属性的区段定义，以及在24小时的时间范围内发生特定次数的否定事件。 | 过去24小时内未访问过主页&#x200B;**超过**&#x200B;五次的用户。 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| 24小时时间配置文件内的多个传入点击 | 任何涉及在24小时的时间范围内发生的多个事件的区段定义。 | 访问主页&#x200B;**或**&#x200B;的人在过去24小时内访问了结账页面。 | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 一个配置文件在24小时时间范围内的多个事件 | 任何区段定义，它是指在24小时的时间范围内发生的一个或多个用户档案属性和多个事件。 | 美国人在过去24小时内访问了主页&#x200B;**和**&#x200B;并访问了结帐页面。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 区段划分 | 包含一个或多个批次或流式客户细分的任何客户细分定义。 | 居住在美国、属于“现有区段”的人群。 | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| 引用映射的查询 | 任何引用属性映射的区段定义。 | 根据外部区段数据添加到购物车的人员。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

在以下方案中，将&#x200B;**不**&#x200B;为边缘分段启用区段定义：

- 区段定义包含单个事件和`inSegment`事件的组合。
   - 但是，如果`inSegment`事件中包含的区段定义仅为配置文件，则区段定义&#x200B;**将**&#x200B;启用边缘分段。
- 区段定义使用“忽略年份”作为其时间限制的一部分。

## 后续步骤

本指南介绍如何在Adobe Experience Platform上使用Edge Segmentation评估区段定义。 若要了解有关使用Experience Platform用户界面的更多信息，请阅读[分段用户指南](./overview.md)。 要了解如何使用Experience PlatformAPI执行类似操作和使用区段定义，请访问[边缘分段API指南](../api/edge-segmentation.md)。

## 附录

以下部分列出了有关边缘分段的常见问题解答：

### 区段定义需要多久才能在Edge Network上可用？

区段定义在Edge Network上可用最多需要一小时。
