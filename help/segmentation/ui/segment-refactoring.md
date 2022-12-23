---
keywords: Experience Platform；主页；热门主题；分段；区段生成器；区段生成器
solution: Experience Platform
title: 重构的分段时间约束UI指南
topic-legacy: ui guide
description: 区段生成器提供了丰富的工作区，允许您与配置文件数据元素进行交互。 工作区提供了用于构建和编辑规则的直观控件，例如用于表示数据属性的拖放图块。
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: 681418b4198c2b1303fda937c3ffc60dad21b672
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# 时间约束重分解

2020年10月版的Adobe Experience Platform对Adobe Experience Platform分段服务进行了性能更改，为使用OR和AND逻辑运算符添加了新限制。 这些更改将影响使用区段生成器UI新创建或编辑的区段。 本指南介绍如何缓解这些更改。

在2020年10月版之前，所有规则级别、组级别和事件级别的时间限制都重复引用了相同的时间戳。 为了阐明时间约束的使用，已删除规则级和组级时间约束。 要适应此更改，所有时间约束都必须重写为事件级时间约束。

以前，单个事件可能会附加多个时间约束规则。

![区段生成器中会突出显示以前的时间约束样式。](../images/ui/segment-refactoring/former-time-constraint.png)

如您所见，此区段在规则级别有两个限制：一个表示“[!UICONTROL 今天]“ ”和“ ”的另一个[!UICONTROL 昨天]&quot;

上一个区段等同于以下区段 — 已使用AND运算符连接两个事件级时间约束。 第一个事件级时间约束引用名称等于“Training”且今天发生的点击事件，而第二个事件级时间约束引用名称等于“Pets”且昨天发生的点击事件。

![区段生成器中会突出显示新的时间限制样式。](../images/ui/segment-refactoring/time-constraint-1.png) ![区段生成器中会突出显示新的时间限制样式。](../images/ui/segment-refactoring/time-constraint-2.png)

时间约束的这种重构还会影响使用OR运算符连接的时间约束。
