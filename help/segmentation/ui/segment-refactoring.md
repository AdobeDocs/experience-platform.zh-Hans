---
keywords: Experience Platform；主页；热门主题；分段；分段；区段生成器；区段生成器
solution: Experience Platform
title: 重构的分段时间约束UI指南
topic-legacy: ui guide
description: 区段生成器提供丰富的工作区，允许您与用户档案数据元素交互。 工作区提供用于构建和编辑规则的直观控件，如用于表示数据属性的拖放拼贴。
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# 时间约束重因式分解

Adobe Experience Platform 2020年10月版本对Adobe Experience Platform分段服务引入了性能更改，为OR和AND逻辑运算符的使用增加了新的限制。 这些更改将影响使用区段生成器用户界面创建的新创建或编辑的区段。 本指南介绍如何减轻这些更改。

在2020年10月版本之前，所有规则级、组级和事件级时间限制都重复引用相同的时间戳。 为了澄清时间约束的使用情况，删除了规则级和组级时间约束。 要适应此更改，必须将所有时间约束重写为事件级时间约束。

以前，单个事件可能附加了多个时间约束规则。

![](../images/ui/segment-refactoring/former-time-constraint.png)

如您所见，此区段在规则级别上有两个限制：一个表示“[!UICONTROL Today]”，另一个表示“[!UICONTROL Yesterday]”。

上一段与以下段等效 — 两个事件级时间约束都已使用AND运算符连接。 第一个事件级时间约束引用名称等于“培训”的单击事件，而第二个事件级时间约束引用名称等于“Pets”且昨天发生的单击事件。

![](../images/ui/segment-refactoring/time-constraint-1.png) ![](../images/ui/segment-refactoring/time-constraint-2.png)

时间约束的重构还影响使用OR运算符连接的时间约束。
