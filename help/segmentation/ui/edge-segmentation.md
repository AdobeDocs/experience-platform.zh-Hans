---
keywords: Experience Platform；主页；热门主题；边缘分割；分割；分割服务；分割服务；用户界面指南；流边缘；
solution: Experience Platform
title: 边缘分段UI指南
topic: ui指南
description: 边缘细分是指在Platform中即时评估边缘区段的能力，支持相同页面和下一页个性化使用案例。
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
translation-type: tm+mt
source-git-commit: 36169a42c7f6a73ca9cc165cd338d6a1cf245bfc
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 4%

---

# 边缘分段UI指南（测试版）

>[!NOTE]
>
>边缘分段当前为测试版。 文档和功能可能会发生变化。

边缘细分是指在边缘即时评估Adobe Experience Platform中的细分，支持相同页面和下一页个性化使用案例。

## 边缘分割查询类型

如果查询满足以下任一条件，则可以使用边缘分割来评估该数据：

| 查询类型 | 详细信息 | 示例 |
| ---------- | ------- | ------- |
| 传入点击 | 任何区段定义，指没有时间限制的单个传入事件。 | ![](../images/ui/edge-segmentation/incoming-hit.png) |
| 指用户档案的传入点击 | 引用单个传入事件（无时间限制）和一个或多个用户档案属性的任何区段定义。 | ![](../images/ui/edge-segmentation/profile-hit.png) |
| 频率查询 | 指发生至少特定次数的事件的任何区段定义。 |  |
| 引用查询的频率用户档案 | 任何区段定义，指发生至少特定次数的事件，并具有一个或多个用户档案属性。 |  |

如果查询与上述任何查询类型匹配，则可以通过打开&#x200B;**[!UICONTROL Evaluate as streaming segment on the edge]**&#x200B;切换来启用边缘分割。

![](../images/ui/edge-segmentation/mark-on-edge.png)

以下查询类型&#x200B;**当前不**&#x200B;用于边缘分割：

| 查询类型 | 详细信息 |
| ---------- | ------- |
| 相对时间窗口 | 如果查询引用时间窗口，则无法使用边缘分割来评估该窗口。 |
| 取反 | 如果查询包含取反，则无法使用边缘分段对其进行计算。 |
| 多个事件 | 如果查询包含多个事件，则无法使用边缘分割对其进行评估。 |

## 后续步骤

本用户指南介绍如何在Adobe Experience Platform上使用边缘分段来评估区段。

要了解有关使用Adobe Experience Platform用户界面的更多信息，请阅读[分段用户指南](./overview.md)。 要了解如何使用Adobe Experience Platform用户界面执行类似操作和处理区段，请访问[边缘分段API指南](../api/edge-segmentation.md)。
