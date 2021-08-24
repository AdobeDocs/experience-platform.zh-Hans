---
keywords: Experience Platform；主页；热门主题；边缘分段；分段；分段服务；分段服务；UI指南；流式边缘；
solution: Experience Platform
title: 边缘分段UI指南
topic-legacy: ui guide
description: 边缘分段功能可以即时评估Platform中的边缘区段，从而实现同一页面和下一页面个性化用例。
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 8f2540902cdcff99627393429424dbfe1de2d3da
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 3%

---

# 边缘分段UI指南（测试版）

>[!NOTE]
>
>边缘分段当前为测试版。 文档和功能可能会发生变化。

边缘分段功能可以即时在边缘上评估Adobe Experience Platform中的区段，从而实现同一页面和下一页面的个性化用例。

## 边缘分段查询类型

如果查询满足以下任一条件，则可以使用边缘分段来评估该查询：

| 查询类型 | 详细信息 | 示例 |
| ---------- | ------- | ------- |
| 传入点击 | 任何引用无时间限制的单个传入事件的区段定义。 | ![](../images/ui/edge-segmentation/incoming-hit.png) |
| 引用用户档案的传入点击 | 任何引用单个传入事件（无时间限制）和一个或多个用户档案属性的区段定义。 | ![](../images/ui/edge-segmentation/profile-hit.png) |
| 时间窗口为24小时的传入点击 | 在24小时内引用单个传入事件的任何区段定义 |  |
| 引用时间窗口为24小时的用户档案的传入点击 | 在24小时内引用单个传入事件以及一个或多个用户档案属性的任何区段定义 |  |

如果查询与上述任何查询类型匹配，则将使用边缘分段自动评估该查询。

以下查询类型是当前支持边缘分段的&#x200B;**not**:

| 查询类型 | 详细信息 |
| ---------- | ------- |
| 多个事件 | 如果查询包含多个事件，则无法使用边缘分段来评估该查询。 |
| 频度查询 | 任何区段定义，指发生至少特定次数的事件。 |  |
| 引用用户档案的频率查询 | 任何区段定义，指发生至少特定次数且具有一个或多个用户档案属性的事件。 |  |

## 后续步骤

本用户指南介绍如何在Adobe Experience Platform上使用边缘分段来评估区段。

要了解有关使用Adobe Experience Platform用户界面的更多信息，请阅读[分段用户指南](./overview.md)。 要了解如何使用Adobe Experience Platform用户界面执行类似操作和处理区段，请访问[边缘分段API指南](../api/edge-segmentation.md)。
