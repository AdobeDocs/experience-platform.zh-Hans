---
keywords: Experience Platform；主页；热门主题；边缘分段；分段；分段服务；分段服务；ui指南；流式边缘；
solution: Experience Platform
title: 边缘分段UI指南
description: 边缘分段是在边缘上即时评估Platform中的区段的能力，从而启用同一页面和下一页面个性化用例。
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---

# 边缘分段 UI 指南

>[!NOTE]
>
>现在，所有Platform用户均可正常使用边缘分段。 如果您在Beta版期间创建了Edge区段，则这些区段将继续正常运行。

边缘分段是一种在Adobe Experience Platform中即时评估区段的能力 [在边缘](../../edge/home.md)，启用同一页面和下一页面个性化用例。

>[!IMPORTANT]
>
> 边缘数据将存储在距离收集位置最近的边缘服务器位置，并且可能存储在指定为Adobe Experience Platform数据中心（或主体）以外的位置。
>
> 此外，边缘分段引擎将仅处理存在以下条件的边缘上的请求： **一** 主标记身份，与非基于边缘的主身份一致。

## 边缘分段查询类型 {#query-types}

当前只能使用边缘分段评估选定的查询类型。 以下部分提供了可通过边缘分段评估的查询类型以及当前不支持的查询类型列表。

如果查询符合下表中列出的任何条件，则可以使用边缘分段来评估查询。

>[!NOTE]
>
>如果查询与下表中的任何查询类型匹配，则将使用边缘分段自动评估该查询。 系统会根据查询表达式自动确定此功能。

| 查询类型 | 详细信息 | 示例 | PQL示例 |
| ---------- | ------- | ------- | ----------- |
| 单个事件 | 任何引用没有时间限制的单个传入事件的区段定义。 | 将商品添加到购物车的人员。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| 单个配置文件 | 任何引用单个仅配置文件属性的区段定义 | 住在美国的人。 | `homeAddress.countryCode = "US"` |
| 引用用户档案的单个事件 | 任何引用一个或多个配置文件属性和单个传入事件的区段定义，无时间限制。 | 居住在美国的人访问了该主页。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")])` |
| 否定了具有配置文件属性的单个事件 | 任何引用否定单个传入事件和一个或多个用户档案属性的区段定义 | 居住在美国并且有 **非** 浏览了主页。 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| 时间窗口内的单个事件 | 任何引用一段时间内单个传入事件的区段定义。 | 过去24小时内访问过主页的人。 | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)])` |
| 时间范围内具有配置文件属性的单个事件 | 任何引用一段时间内一个或多个用户档案属性和单个传入事件的区段定义。 | 居住在美国的人在过去24小时内访问了该主页。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)])` |
| 在一个时间范围内否定了具有配置文件属性的单个事件 | 任何引用一段时间内一个或多个用户档案属性和否定单个传入事件的区段定义。 | 居住在美国并且有 **非** 在过去24小时内访问了主页。 | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)]))` |
| 24小时时间范围内的频率事件 | 任何区段定义，它是指在24小时的时间范围内发生特定次数的事件。 | 访问过主页的人 **至少** 过去24小时内5次。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 在24小时时间范围内具有配置文件属性的频率事件 | 任何引用一个或多个用户档案属性的区段定义，以及在24小时时间范围内发生特定次数的事件。 | 访问主页的美国人 **至少** 过去24小时内5次。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 在24小时时间范围内具有用户档案的否定频率事件 | 任何引用一个或多个用户档案属性的区段定义，以及在24小时的时间范围内发生特定次数的否定事件。 | 未访问过主页的人 **更多** 超过5次了。 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| 24小时时间配置文件内的多个传入点击 | 任何涉及在24小时内发生的多次事件的区段定义。 | 访问过主页的人 **或** 在过去24小时内访问了“结帐”页面。 | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 在24小时时间范围内使用用户档案的多个事件 | 任何区段定义，它是指在24小时内发生的一个或多个配置文件属性和多个事件。 | 访问过该主页的美国人 **和** 在过去24小时内访问了“结帐”页面。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 区段分部 | 包含一个或多个批次或流区段的任何区段定义。 | 居住在美国且属于“现有区段”的人群。 | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| 引用映射的查询 | 任何引用属性映射的区段定义。 | 根据外部区段数据添加到购物车的人员。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

区段定义将 **非** 在以下情况下启用边缘分段：

- 区段定义包括单个事件和 `inSegment` 事件。
   - 然而，倘该分部包含在 `inSegment` 事件仅用于配置文件，区段定义 **将** 启用边缘分段。

## 后续步骤

本指南介绍如何在Adobe Experience Platform上使用边缘分段评估区段。 要了解有关使用Experience Platform用户界面的更多信息，请阅读 [分段用户指南](./overview.md). 要了解如何使用Experience PlatformAPI执行类似操作和使用区段，请访问 [edge segmentation API指南](../api/edge-segmentation.md).

## 附录

以下部分列出了有关边缘分段的常见问题解答：

### 区段在Edge Network上可用需要多长时间？

在Edge Network上可用区段最多需要一小时。