---
keywords: Experience Platform；主页；热门主题；边缘分段；分段；分段服务；分段服务；UI指南；流式边缘；
solution: Experience Platform
title: 边缘分段UI指南
topic-legacy: ui guide
description: 边缘分段功能可以即时评估Platform中的边缘区段，从而实现同一页面和下一页面个性化用例。
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 75583d9688f0c5ee0fe4627ce64b5436ca621aa1
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---

# 边缘分段UI指南

>[!NOTE]
>
>现在，边缘分段通常可供所有Platform用户使用。 如果您在测试期间创建了边缘区段，则这些区段将继续可操作。

边缘分段能够即时评估Adobe Experience Platform中的区段 [边缘](../../edge/home.md)，启用同一页面和下一页个性化用例。

>[!IMPORTANT]
>
> 边缘数据将存储在与收集位置最接近的边缘服务器位置，并且可能存储在指定为中心（或主体）Adobe Experience Platform数据中心的位置以外的位置。
>
> 此外，边缘分段引擎将仅执行存在的边缘上的请求 **one** 主标记标识，与非基于边缘的主标识一致。

## 边缘分段查询类型

目前，只能通过边缘分段来评估选定的查询类型。 以下各节提供了一系列查询类型，这些类型可通过边缘分段进行评估，而这些类型当前不受支持。

### 支持的查询类型 {#query-types}

如果查询符合下表中所述的任何标准，则可以使用边缘分段来评估查询。

>[!NOTE]
>
>如果查询与下表中的任意查询类型匹配，则将使用边缘分段自动评估该查询。 系统会根据查询表达式自动确定此功能。

| 查询类型 | 详细信息 | 示例 | PQL示例 |
| ---------- | ------- | ------- | ----------- |
| 单个事件 | 任何引用无时间限制的单个传入事件的区段定义。 | 向购物车中添加了商品的用户。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| 单个用户档案 | 任何引用单个仅限用户档案属性的区段定义 | 住在美国的人。 | `homeAddress.countryCode = "US"` |
| 引用用户档案的单个事件 | 引用一个或多个用户档案属性以及无时间限制的单个传入事件的任何区段定义。 | 访问主页的美国人。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| 使用配置文件属性否定单个事件 | 任何引用否定的单个传入事件和一个或多个用户档案属性的区段定义 | 在美国生活并拥有 **not** 访问主页。 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| 一个时间范围内的单个事件 | 引用指定时间段内单个传入事件的任何区段定义。 | 过去24小时内访问主页的人员。 | `chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)])` |
| 时间窗口内具有配置文件属性的单个事件 | 引用一个或多个用户档案属性以及设置时间段内单个传入事件的任何区段定义。 | 过去24小时内访问主页的美国人。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)])` |
| 在时间窗口内使用配置文件属性否定单个事件 | 指一段时间内一个或多个用户档案属性以及否定的单个传入事件的任何区段定义。 | 在美国生活并拥有 **not** 在过去24小时内访问了主页。 | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)]))` |
| 24小时时间范围内的频度事件 | 任何区段定义，指在24小时内发生一定次数的事件。 | 访问主页的人员 **至少** 过去24小时里五次。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 在24小时时间范围内具有用户档案属性的频率事件 | 任何区段定义，指一个或多个用户档案属性以及在24小时内发生一定次数的事件。 | 访问主页的美国人 **至少** 过去24小时里五次。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 在24小时的时间范围内使用用户档案否定频率事件 | 任何区段定义，指一个或多个用户档案属性以及在24小时的时间范围内发生一定次数的否定事件。 | 未访问主页的人员 **更多** 超过5次。 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| 在24小时的时间配置文件内多次传入的点击 | 指在24小时内发生的多个事件的任何区段定义。 | 访问主页的人员 **或** 在过去24小时内访问了结帐页面。 | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 在24小时的时间范围内使用用户档案进行多个事件 | 任何区段定义，指在24小时内发生的一个或多个用户档案属性和多个事件。 | 访问主页的美国人 **和** 在过去24小时内访问了结帐页面。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 区段 | 包含一个或多个批处理或流式处理区段的任何区段定义。 | 居住在美国且位于区段“现有区段”中的人员。 | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| 引用映射的查询 | 引用属性映射的任何区段定义。 | 基于外部区段数据添加到购物车的人员。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

## 后续步骤

本指南介绍如何在Adobe Experience Platform上使用边缘分段来评估区段。 要了解有关使用Experience Platform用户界面的更多信息，请阅读 [分段用户指南](./overview.md). 要了解如何使用Experience PlatformAPI执行类似操作和处理区段，请访问 [边缘分段API指南](../api/edge-segmentation.md).
