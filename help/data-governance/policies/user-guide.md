---
keywords: Experience Platform;home;popular topics;data governance;data usage policy user guide
solution: Experience Platform
title: 数据使用策略用户指南
topic: policies
description: Adobe Experience Platform数据管理提供了一个用户界面，允许您创建和管理数据使用策略。 此文档概述了在Experience Platform用户界面的“策略”工作区中可以执行的操作。
translation-type: tm+mt
source-git-commit: 43d568a401732a753553847dee1b4a924fcc24fd
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 0%

---


# 数据使用策略用户指南

Adobe Experience Platform [!DNL Data Governance] 提供一个用户界面，允许您创建和管理数据使用策略。 此文档概述了在用户界面的“策略”工 _作区_ 中可执行 [!DNL Experience Platform] 的操作。

>[!IMPORTANT]
>
>默认情况下，所有数据使用策略(包括Adobe提供的核心策略)都处于禁用状态。 要考虑实施单个策略，必须手动启用该策略。 有关如何在UI [中执行](#enable) 此操作的步骤，请参阅启用策略一节。

## 先决条件

本指南需要对以下概念有充分的 [!DNL Experience Platform] 了解：

- [[!DNL数据管理]](../home.md)
- [数据使用策略](./overview.md)

## 视图数据使用策略 {#view-policies}

在UI中 [!DNL Experience Platform] ，单击“策 **[!UICONTROL 略]** ”以打开“策 *[!UICONTROL 略]* ”工作区。 在“浏 **[!UICONTROL 览]** ”选项卡中，您可以看到可用策略的列表，包括其关联的标签、营销操作和状态。

![](../images/policies/browse-policies.png)

单击列出的策略以视图其描述和类型。 如果选择了自定义策略，则会显示用于编辑、删除或启用／禁 [用该策略的其他控件](#enable)。

![](../images/policies/policy-details.png)

## 创建自定义数据使用策略 {#create-policy}

要创建新的自定义数据使用策略，请 **[!UICONTROL 单击]** “策略”工作区中“浏览”选 **[!UICONTROL 项卡右]** 上角的 *[!UICONTROL “创建]* 策略”。

![](../images/policies/create-policy-button.png)

将显 *[!UICONTROL 示创建策略]* 工作流。 开始，为新策略提供名称和说明。

![](../images/policies/create-policy-description.png)

接下来，选择策略将基于的数据使用标签。 在选择多个标签时，您可以选择数据应包含所有标签还是只包含其中一个标签，以便应用策略。 完成后，单击&#x200B;**[!UICONTROL 下一步]**。

![](../images/policies/add-labels.png)

此时将 *[!UICONTROL 显示选择营销]* 操作步骤。 从提供的列表中选择适当的营销操作，然后单 **[!UICONTROL 击下]** 一步继续。

>[!NOTE]
>
>选择多个营销活动时，策略会将其解释为“OR”规则。 换言之，如果执行了任 _何选定_ 的营销操作，则此策略适用。

![](../images/policies/add-marketing-actions.png)

此时 *[!UICONTROL 会显示]* “审阅”(Review)步骤，允许您在创建新策略之前查看其详细信息。 满意后，单击 **[!UICONTROL 完成]** 以创建策略。

![](../images/policies/policy-review.png)

“浏 *[!UICONTROL 览]* ”选项卡将重新显示，该选项卡现在将新创建的策略列表为“草稿”状态。 要启用策略，请参阅下一节。

![](../images/policies/created-policy.png)

## 启用或禁用数据使用策略 {#enable}

默认情况下，所有数据使用策略(包括Adobe提供的核心策略)都处于禁用状态。 要考虑实施单个策略，必须通过API或UI手动启用该策略。

您可以从“策略”工作区的“浏 *[!UICONTROL 览]* ”选项卡中启用或禁用 *[!UICONTROL 策略]* 。 从列表中选择自定义策略，在右侧显示其详细信息。 在“ *[!UICONTROL 状态]*”下，选择切换按钮以启用或禁用策略。

![](../images/policies/enable-policy.png)

## 视图营销行动 {#view-marketing-actions}

在“策 **[!UICONTROL 略]** ”工作区中，选择“ **[!UICONTROL 营销操作]** ”选项卡，以视图由Adobe和您自己的组织定义的一列表可用的营销操作。

![](../images/policies/marketing-actions.png)

## 创建营销操作 {#create-marketing-action}

要创建新的自定义营销操作，请单 **[!UICONTROL 击“策略]** ”工作区中“营销操作”选 **[!UICONTROL 项卡右上角的]** “创建营 *[!UICONTROL 销操作]* ”。

![](../images/policies/create-marketing-action.png)

此时将 *[!UICONTROL 显示创建营销]* 操作对话框。 输入营销活动的名称和说明，然后单击 **[!UICONTROL 创建]**。

![](../images/policies/create-marketing-action-details.png)

新创建的操作会显示在“营销 *[!UICONTROL 操作”选]* 项卡中。 您现在可以在创建新数据使用策 [略时使用营销操作](#create-policy)。

![](../images/policies/created-marketing-action.png)

## 编辑或删除营销操作 {#edit-delete-marketing-action}

>[!NOTE]
>
>只能编辑您的组织定义的自定义营销操作。 不能更改或删除由Adobe定义的营销活动。

在“策 **[!UICONTROL 略]** ”工作区中，选择“ **[!UICONTROL 营销操作]** ”选项卡，以视图由Adobe和您自己的组织定义的一列表可用的营销操作。 从列表中选择自定义营销操作，然后使用右侧部分中提供的字段编辑营销操作的详细信息。

![](../images/policies/edit-marketing-action.png)

如果任何现有的使用策略未使用营销活动，则可以单击删除营 **[!UICONTROL 销活动来删除它]**。

>[!NOTE]
>
>尝试删除现有策略正在使用的营销操作将导致显示错误消息，指示删除尝试失败。

![](../images/policies/delete-marketing-action.png)

## 后续步骤

此文档概述了如何在UI中管理数据使用策 [!DNL Experience Platform] 略。 有关如何使用DULE Policy API管理策略的步骤，请参阅开发 [人员指南](../api/getting-started.md)。 有关如何实施数据使用策略的信息，请参阅策 [略实施概述](../enforcement/overview.md)。

以下视频演示了如何在UI中使用使用策 [!DNL Experience Platform] 略：

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)