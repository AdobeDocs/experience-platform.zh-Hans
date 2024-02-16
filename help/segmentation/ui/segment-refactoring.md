---
solution: Experience Platform
title: 重构的分段时间约束UI指南
description: 区段生成器提供了一个丰富的工作区，允许您与配置文件数据元素进行交互。 工作区为构建和编辑规则提供了直观的控件，例如用于表示数据属性的拖放图块。
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: 665bbd1904e857336a4fb677230389d7977f6b60
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 9%

---

# 时间限制重构 {#refactorization}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_constraints"
>title="时间限制重构"
>abstract="已删除规则级别和组级别的时间限制以阐明时间限制的用法。请将您的限制重写为画布级别或信息卡级别的时间限制。"

Adobe Experience Platform 2024年1月版对Adobe Experience Platform分段服务进行了更改，在可以定义时间限制的位置添加了新限制。 这些更改会影响使用区段生成器UI新建或编辑的区段。 本指南介绍如何缓解这些更改。

在2024年1月版之前，所有规则级别、组级别和画布级别的时间约束都冗余地引用同一时间戳。 为了明确时间约束的使用，已移除规则级和组级时间约束。 为了适应此更改，所有时间限制 **必须** 被重写为 **画布级别** 或 **卡片级别** 时间限制。

以前，单个事件可以有多个时间限制规则附加到该事件。 通过最近更新，尝试向规则添加时间限制将导致 **错误**.

![规则级时间限制会突出显示。 随后发生的错误也会突出显示。 ](../images/ui/segment-refactoring/rule-time-constraint.png)

时间限制现在只能在画布级别或卡片级别应用。

在画布级别应用时间限制时，您仍然可以选择所有可用的时间限制。

>[!NOTE]
>
>如果只有 **一** 卡片，将时间限制应用于卡片是 **等效** 在画布级别应用时间限制。
>
>如果有 **多个** 中的卡片，将时间约束应用于画布级别会将该时间约束应用于 **所有** 在画布上画牌。

![画布级别的时间限制会突出显示。](../images/ui/segment-refactoring/canvas-time-constraint.png)

要在卡片级别应用时间限制，请选择要对其应用时间限制的特定卡片。 此 **[!UICONTROL 事件规则]** 容器出现。 您现在可以选择要应用于卡的时间限制。

![卡片级别的时间限制会突出显示。](../images/ui/segment-refactoring/card-time-constraint.png)
