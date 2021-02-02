---
keywords: Experience Platform；主页；热门主题；数据管理；数据使用策略用户指南
solution: Experience Platform
title: 数据使用策略用户指南
topic: policies
description: Adobe Experience Platform数据管理提供了一个用户界面，允许您创建和管理数据使用策略。 此文档概述了在Experience Platform用户界面的“策略”工作区中可以执行的操作。
translation-type: tm+mt
source-git-commit: 00010d38a5d05800aeac9af8505093fee3593b45
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---


# 数据使用策略用户指南

Adobe Experience Platform[!DNL Data Governance]提供一个用户界面，允许您创建和管理数据使用策略。 此文档概述了在[!DNL Experience Platform]用户界面的&#x200B;**策略**&#x200B;工作区中可以执行的操作。

>[!IMPORTANT]
>
>默认情况下，所有数据使用策略(包括Adobe提供的核心策略)都处于禁用状态。 要考虑实施单个策略，必须手动启用该策略。 有关如何在UI中执行此操作的步骤，请参见[启用策略](#enable)一节。

## 先决条件

本指南需要对以下[!DNL Experience Platform]概念有充分的了解：

- [[!DNL Data Governance]](../home.md)
- [数据使用策略](./overview.md)

## 视图数据使用策略{#view-policies}

在[!DNL Experience Platform] UI中，选择&#x200B;**[!UICONTROL 策略]**&#x200B;以打开&#x200B;**[!UICONTROL 策略]**&#x200B;工作区。 在&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡中，您可以看到可用策略的列表，包括其关联的标签、营销操作和状态。

![](../images/policies/browse-policies.png)

选择列出的策略以视图其描述和类型。 如果选择了自定义策略，则显示其他控件以编辑、删除或[启用／禁用策略](#enable)。

![](../images/policies/policy-details.png)

## 创建自定义数据使用策略{#create-policy}

要创建新的自定义数据使用策略，请在&#x200B;**[!UICONTROL 策略]**&#x200B;工作区的&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡的右上角选择&#x200B;**[!UICONTROL 创建策略]**。

![](../images/policies/create-policy-button.png)

出现&#x200B;**[!UICONTROL 创建策略]**&#x200B;工作流。 开始，为新策略提供名称和说明。

![](../images/policies/create-policy-description.png)

接下来，选择策略将基于的数据使用标签。 在选择多个标签时，您可以选择数据应包含所有标签还是只包含其中一个标签，以便应用策略。 完成后，选择&#x200B;**[!UICONTROL Next]**。

![](../images/policies/add-labels.png)

将显示&#x200B;**[!UICONTROL 选择营销操作]**&#x200B;步骤。 从提供的列表中选择适当的营销操作，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;继续。

>[!NOTE]
>
>选择多个营销活动时，策略会将其解释为“OR”规则。 换句话说，如果执行了所选营销操作的&#x200B;**任何**，则此策略适用。

![](../images/policies/add-marketing-actions.png)

出现&#x200B;**[!UICONTROL 查看]**&#x200B;步骤，允许您在创建新策略之前查看其详细信息。 满意后，选择&#x200B;**[!UICONTROL 完成]**&#x200B;以创建策略。

![](../images/policies/policy-review.png)

将重新显示&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡，该选项卡现在将新创建的策略列表为“草稿”状态。 要启用策略，请参阅下一节。

![](../images/policies/created-policy.png)

## 启用或禁用数据使用策略{#enable}

默认情况下，所有数据使用策略(包括Adobe提供的核心策略)都处于禁用状态。 要考虑实施单个策略，必须通过API或UI手动启用该策略。

您可以从&#x200B;**[!UICONTROL 策略]**&#x200B;工作区的&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡中启用或禁用策略。 从列表中选择自定义策略，在右侧显示其详细信息。 在&#x200B;**[!UICONTROL 状态]**&#x200B;下，选择切换按钮以启用或禁用策略。

![](../images/policies/enable-policy.png)

## 视图营销操作{#view-marketing-actions}

在&#x200B;**[!UICONTROL 策略]**&#x200B;工作区中，选择&#x200B;**[!UICONTROL 营销操作]**&#x200B;选项卡，以视图由Adobe和您自己的组织定义的可用营销操作的列表。

![](../images/policies/marketing-actions.png)

## 创建营销操作{#create-marketing-action}

要创建新的自定义营销操作，请在&#x200B;**[!UICONTROL 策略]**&#x200B;工作区的&#x200B;**[!UICONTROL 营销操作]**&#x200B;选项卡的右上角选择&#x200B;**[!UICONTROL 创建营销操作]**。

![](../images/policies/create-marketing-action.png)

将显示&#x200B;**[!UICONTROL 创建营销操作]**&#x200B;对话框。 输入营销操作的名称和说明，然后选择&#x200B;**[!UICONTROL 创建]**。

![](../images/policies/create-marketing-action-details.png)

新创建的操作将显示在&#x200B;**[!UICONTROL 营销操作]**&#x200B;选项卡中。 现在，您可以在[创建新数据使用策略](#create-policy)时使用营销操作。

![](../images/policies/created-marketing-action.png)

## 编辑或删除营销操作{#edit-delete-marketing-action}

>[!NOTE]
>
>只能编辑您的组织定义的自定义营销操作。 不能更改或删除由Adobe定义的营销活动。

在&#x200B;**[!UICONTROL 策略]**&#x200B;工作区中，选择&#x200B;**[!UICONTROL 营销操作]**&#x200B;选项卡，以视图由Adobe和您自己的组织定义的可用营销操作的列表。 从列表中选择自定义营销操作，然后使用右侧部分中提供的字段编辑营销操作的详细信息。

![](../images/policies/edit-marketing-action.png)

如果任何现有的使用策略都未使用营销操作，则可以通过选择&#x200B;**[!UICONTROL 删除营销操作]**&#x200B;来删除该操作。

>[!NOTE]
>
>尝试删除现有策略正在使用的营销操作将导致显示错误消息，指示删除尝试失败。

![](../images/policies/delete-marketing-action.png)

## 后续步骤

此文档概述了如何在[!DNL Experience Platform] UI中管理数据使用策略。 有关如何使用[!DNL Policy Service API]管理策略的步骤，请参阅[开发人员指南](../api/getting-started.md)。 有关如何实施数据使用策略的信息，请参阅[策略实施概述](../enforcement/overview.md)。

以下视频演示了如何在[!DNL Experience Platform] UI中使用使用策略：

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)