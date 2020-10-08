---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment builder;Segment builder
solution: Experience Platform
title: 分段服务区段生成器更改指南
topic: ui guide
description: '区段生成器提供丰富的工作区，允许您与用户档案数据元素交互。 工作区提供用于构建和编辑规则的直观控件，如用于表示数据属性的拖放拼贴。 '
translation-type: tm+mt
source-git-commit: beacce03136e1620ff57fb549f335d2199bb6001
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---


# 时间约束重分解

Adobe Experience Platform2020年10月版本对Adobe Experience Platform分段服务引入了性能更改，这为OR和AND逻辑运算符的使用增加了新的限制。 这些更改将影响使用区段生成器用户界面创建的新创建或编辑的区段。 本指南介绍如何减轻这些更改。

在2020年10月发布之前，所有规则级、组级和事件级时间约束都重复引用同一时间戳。 为了澄清时间约束的使用，已删除规则级和组级时间约束。 要适应此更改，必须将所有时间约束重写为事件级时间约束。

以前，单个事件可能附加多个时间约束规则。

![](../images/ui/segment-refactoring/former-time-constraint.png)

如您所见，此区段在规则级别上有两个限制：一个是“[!UICONTROL 今]天”，另一个是“[!UICONTROL 昨天]”。

上一个段等效于以下段——两个事件级时间约束都已使用AND运算符连接。 第一个事件级时间约束引用名称等于“Training”的单击事件，而第二个事件级时间约束引用名称等于“Pets”的单击事件，该是昨天发生的。

![](../images/ui/segment-refactoring/time-constraint-1.png) ![](../images/ui/segment-refactoring/time-constraint-2.png)

时间约束的这种重构还影响使用OR运算符连接的时间约束。