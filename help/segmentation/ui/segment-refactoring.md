---
solution: Experience Platform
title: 重构的分段时间约束UI指南
description: 区段生成器提供了一个丰富的工作区，允许您与配置文件数据元素进行交互。 工作区为构建和编辑规则提供了直观的控件，例如用于表示数据属性的拖放图块。
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# 时间约束重构

Adobe Experience Platform 2020年10月版对Adobe Experience Platform分段服务进行了性能更改，从而增加了使用OR和AND逻辑运算符的新限制。 这些更改将影响使用区段生成器UI新建或编辑的区段。 本指南介绍如何减轻这些变化。

在2020年10月版之前，所有规则级别、组级别和事件级别的时间约束都冗余地引用同一时间戳。 为了明确时间约束的使用，已删除规则级别和组级别的时间约束。 为了适应此更改，必须将所有时间约束重写为事件级别的时间约束。

以前，单个事件可以有多个时间限制规则附加到该事件。

![区段生成器中会突出显示以前的时间约束样式。](../images/ui/segment-refactoring/former-time-constraint.png)

如您所见，此区段在规则级别有两个限制：一个用于&quot;[!UICONTROL 今天]”和另一个为“[!UICONTROL 昨天]“。

上一个段相当于以下段 — 两个事件级时间约束均已使用AND运算符连接。 第一个事件级别时间约束引用名称等于“Training”且发生在今天的点击事件，而第二个事件级别时间约束引用名称等于“Pets”且发生在昨天的点击事件。

![区段生成器中会突出显示新的时间限制样式。](../images/ui/segment-refactoring/time-constraint-1.png) ![区段生成器中会突出显示新的时间限制样式。](../images/ui/segment-refactoring/time-constraint-2.png)

时间约束的这种重构也会影响使用OR运算符连接的时间约束。
