---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 数据使用策略用户指南
topic: policies
translation-type: tm+mt
source-git-commit: 304a84b81758b2f2a343977533f9120857a1fb33

---


# 数据使用策略用户指南

Adobe Experience Platform Data Governance提供了一个用户界面，允许您创建和管理数据使用策略。 此文档概述了您可以在Experience Platform UI的“策略”工 _作区中_ ，执行的操作。

## 先决条件

本指南需要对以下Experience Platform概念有充分的了解：

- [数据管理](../home.md)
- [数据使用策略](./overview.md)

## 视图数据使用策略

在Experience Platform UI中，单击以 **[!UICONTROL Policies]** 打开工作 *[!UICONTROL Policies]* 区。 在该选 **[!UICONTROL Browse]** 项卡中，您可以看到可用策略的列表，包括它们的关联标签、营销操作和状态。

![](../images/policies/browse-policies.png)

单击列出的策略以视图其描述和类型。 如果选择了自定义策略，则会显示用于编辑、删除或启用／禁 [用策略的其他控件](#enable)。

![](../images/policies/policy-details.png)

## 创建自定义数据使用策略

要创建新的自定义数据使用策略， **[!UICONTROL Create policy]** 请单击“策略”工作区右上 *角* 。

![](../images/policies/create-policy-button.png)

此时将 *[!UICONTROL Create policy]* 显示工作流。 开始，为新策略提供名称和说明。

![](../images/policies/create-policy-description.png)

接下来，选择策略将基于的数据使用标签。 在选择多个标签时，您可以选择数据应包含所有标签还是仅包含其中一个标签，以便应用策略。 完成后单击 **[!UICONTROL Next]**。

![](../images/policies/add-labels.png)

将出 *[!UICONTROL Select marketing actions]* 现该步骤。 从提供的列表中选择适当的营销操作，然后单击以 **[!UICONTROL Next]** 继续操作。

>[!NOTE] 选择多个营销操作时，策略会将其解释为“OR”规则。 换句话说，如果执行了任 _何选定_ 的营销操作，则此策略适用。

![](../images/policies/add-marketing-actions.png)

此时 *[!UICONTROL Review]* 会显示该步骤，允许您在创建新策略之前查看其详细信息。 满意后，单击以 **[!UICONTROL Finish]** 创建策略。

![](../images/policies/policy-review.png)

此时 *[!UICONTROL Browse]* 将重新显示选项卡，该选项卡现在将新创建的策略列表为“草稿”状态。 要启用策略，请参阅下一节。

![](../images/policies/created-policy.png)

## 启用或禁用数据使用策略 {#enable}

您可以在工作区的选项卡上启用或禁用自 *[!UICONTROL Browse]* 定义数据使用 *[!UICONTROL Policies]* 策略。 从列表中选择自定义策略，以在右侧显示其详细信息。 在下 *[!UICONTROL Status]*&#x200B;面，选择切换按钮以启用或禁用策略。

![](../images/policies/enable-policy.png)

## 后续步骤

本文档概述了如何在Experience Platform UI中管理数据使用策略。 有关如何使用DULE Policy API管理策略的步骤，请参阅 [API策略创建教程](./create.md)。 有关如何实施数据使用策略的信息，请参阅策 [略实施概述](../enforcement/overview.md)。