---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 合并策略用户指南
topic: guide
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '1104'
ht-degree: 0%

---


# 合并策略用户指南

Adobe Experience Platform使您能够将来自多个来源的数据整合在一起，并将其合并，以便了解每个客户的完整视图。 将数据整合在一起时，合并策略是确定 [!DNL Platform] 数据的优先级以及合并哪些数据以创建统一视图的规则。

使用REST风格的API或用户界面，您可以创建新的合并策略、管理现有策略并为组织设置默认的合并策略。 本指南提供使用Adobe Experience Platform用户界面处理合并策略的分步说明。

如果您希望使用API处理合并策略，请 [!DNL Real-time Customer Profile] 按照合并策略API教程中 [概述的说明操作](../api/merge-policies.md)。

## 入门指南

本指南要求对合并策略涉及的各 [!DNL Experience Platform] 种服务进行有效的了解。 在开始本教程之前，请查看以下服务的相关文档：

* [!DNL Real-time Customer Profile](../home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
* [!DNL Identity Service](../../identity-service/home.md): 通过将 [!DNL Real-time Customer Profile] 来自被引入的不同数据源的身份连接到其中，实现 [!DNL Platform]了。
* [!DNL Experience Data Model (XDM)](../../xdm/home.md): 组织客户体验数 [!DNL Platform] 据的标准化框架。

## 视图合并策略

在用 [!DNL Experience Platform] 户界面中，您可以开始使用合并策略，通过单击左边栏中的列表，然后选择合并策略选项卡，来查看组织现有合 **[!UICONTROL 并策]** 略的用户档案 **** 。

![合并策略登陆页](../images/merge-policies/landing.png)

在登陆页中可看到组织可用的每个合并策略的详细信息，包括 *[!UICONTROL 策略名称]*、 *[!UICONTROL 默认合并策略]*&#x200B;和 *[!UICONTROL 模式]*。

要选择可见的详细信息，或向显示屏添加其他列，请选择右侧的列选择器图标，然后单击列名称以将其添加或从视图中删除。

![](../images/merge-policies/adjust-view.png)

## 创建合并策略

要创建新的合并策略，请单 **[!UICONTROL 击“合并策略]** ”选项卡右上方的“ **[!UICONTROL 创建合并策略]** ”。

![合并策略登陆页](../images/merge-policies/create-new.png)

将出 **[!UICONTROL 现“创建合并策略]** ”屏幕，允许您为新的合并策略提供重要信息。

![](../images/merge-policies/create.png)

* **[!UICONTROL 名称]**: 合并策略的名称应具有描述性且简明。
* **[!UICONTROL 模式]**: 与合并策略关联的模式。 它指定为其创建此合并策略的XDM模式。 组织可以为每个模式创建多个合并策略。
* **[!UICONTROL ID拼接]**: 此字段定义如何确定客户的相关身份。 可能有两个值：
   * **[!UICONTROL 无]**: 不进行身份拼接。
   * **[!UICONTROL 专用图]**: 根据您的个人身份图执行身份拼接。
* **[!UICONTROL 属性合并]**: 用户档案片段是单个客户存在的身份列表中仅一个身份的用户档案信息。 当使用的标识图类型导致多个标识时，存在冲突用户档案属性值的可能性，必须指定优先级。 使用 *属性合并* ，可以指定在发生合并冲突时要排定优先级的数据集用户档案值。 可能有两个值：
   * **[!UICONTROL 排序的时间戳]**: 如果发生冲突，请优先考虑最近更新的用户档案。
   * **[!UICONTROL 数据集优先级]** : 根据用户档案片段的来源数据集优先处理这些片段。 选择此选项时，必须选择相关数据集及其优先级顺序。 有关详细信息，请 [参阅以下](#dataset-precedence) “数据集优先级”的详细信息。
* **[!UICONTROL 默认合并策略]**: 一个切换按钮，允许您选择此合并策略是否将是组织的默认策略。 如果选择器已切换并且保存了新策略，则之前的默认策略将自动更新为不再是默认策略。

### 数据集优先级 {#dataset-precedence}

在选择属 *[!UICONTROL 性合并]* 值时，您可以选择数 *[!UICONTROL 据集优先级]* ，这允许您根据用户档案片段的来源数据集为其优先级。

一个示例用例是，如果您的组织在一个数据集中存在信息，该数据集中的数据优先或受信任，而不是其他数据集中的数据。

选择数 *[!UICONTROL 据集优先级]*&#x200B;时，会打开一个单独的面板，要求您从可 *[!UICONTROL 用数据集中进行选择]* （或使用复选框选择所有数据集）。 然后，您可以将这些数据集拖放到“选 *[!UICONTROL 定的数据集]* ”面板中，并将它们拖入正确的优先级顺序。 优先级最高，次优优先，等等。

![](../images/merge-policies/dataset-precedence.png)

创建完合并策略后，单击 **[!UICONTROL 保存]** ，返回合 *[!UICONTROL 并策略选项]* 卡，新合并策略现在显示在策略列表中。

## 编辑合并策略

通过单击要编辑的合并策略的 *[!UICONTROL 策略名]* ，可以通过合并 *[!UICONTROL 策略选]* 项卡修改现有的合并策略。

![合并策略登陆页](../images/merge-policies/select-edit.png)

出现“编 *[!UICONTROL 辑合并策略]* ”屏幕时，您可以对“名称”、“模式”、“ID”类型、 ********** ”和“Prizting Type”属性以及类型、以及选择是否将此策略指定为是否将本策略转换为您组织的Default Merge Merge Policy。

>[!Note]
>您无法编辑合并策略ID，它显示在编辑屏幕顶部。 这是一个只读的、系统生成的ID，无法更改。

![](../images/merge-policies/edit-screen.png)

完成必要的更改后，单击保 **[!UICONTROL 存]** ，返回到 *[!UICONTROL 合并策略选项]* 卡，此时可以看到更新的合并策略信息。

![](../images/merge-policies/edited.png)

## 违反数据管理策略

创建或更新合并策略时，将执行检查以确定合并策略是否违反了组织定义的任何数据使用策略。 数据使用策略是Adobe Experience Platform的一 [!DNL Data Governance] 部分，是描述您允许或限制对特定数据执行的营销操作种类的 [!DNL Platform] 规则。 例如，如果合并策略用于创建已激活到第三方目标的区段，而您的组织拥有阻止特定数据导出到第三方的数据使用策略，则在尝试保存合并策略时，您将收到“检测到数据管理策略违规”通知。

此通知包括已违反的列表使用策略，并允许您通过从列表中选择策略来视图违规的详细信息。 选择违反的策略后，“数 *据世系* ”选项卡会提 *供违规原因和* 受影响的激活 **，每个都提供有关违反数据使用策略的更多详细信息。

要进一步了解如何在Adobe Experience Platform内执行数据管理，请首先阅读数据管 [理概述](../../data-governance/home.md)。

![](../images/merge-policies/policy-violation.png)

## 后续步骤

现在，您已经为IMS组织创建和配置了合并策略，您可以使用这些策略根据受众数据创建用户档案段。 有关如何 [使用](../../segmentation/home.md) 创建和使用区段的更多信息，请参阅分段概述 [!DNL Experience Platform]。