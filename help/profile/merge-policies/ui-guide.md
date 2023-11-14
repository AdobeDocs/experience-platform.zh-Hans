---
keywords: Experience Platform；配置文件；实时客户配置文件；合并策略；UI；用户界面；已排序时间戳；数据集优先级
title: 合并策略UI指南
type: Documentation
description: 在Experience Platform中将来自多个源的数据汇总在一起时，合并策略是Platform用来确定数据优先顺序以及哪些数据将合并以创建统一视图的规则。 本指南提供了有关使用Adobe Experience Platform用户界面处理合并策略的分步说明。
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '2320'
ht-degree: 0%

---


# 合并策略UI指南

Adobe Experience Platform允许您从多个来源将数据片段整合在一起并组合它们，以便查看每个客户的完整视图。 在汇总此数据时，合并策略是指 [!DNL Platform] 使用确定数据的优先级以及将合并哪些数据以创建统一视图。

使用RESTful API或用户界面，您可以创建新的合并策略、管理现有策略以及为组织设置默认合并策略。 本指南提供了使用Adobe Experience Platform用户界面(UI)处理合并策略的分步说明。

要了解有关合并策略及其在Experience Platform中所发挥作用的更多信息，请先阅读 [合并策略概述](overview.md).

## 快速入门

本指南需要您实际了解几项重要内容 [!DNL Experience Platform] 功能。 在遵循本指南之前，请查看以下服务的文档：

* [Real-time Customer Profile](../home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。
* [Adobe Experience Platform Identity服务](../../identity-service/home.md)：通过桥接从被摄取到的不同数据源的身份，实现实时客户档案 [!DNL Platform].
* [体验数据模型(XDM)](../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Platform] 组织客户体验数据。

## 查看合并策略 {#view-merge-policies}

在 [!DNL Experience Platform] 在UI中，您可以通过选择 **[!UICONTROL 配置文件]** 在左侧导航中，然后选择 **[!UICONTROL 合并策略]** 选项卡。 此选项卡包含贵组织的所有现有合并策略的列表，以及每个合并策略的详细信息，包括策略名称、合并策略是否为默认合并策略以及合并策略相关的架构类。

![合并策略登陆页面](../images/merge-policies/landing.png)

要选择显示哪些详细信息，或向显示添加其他列，请选择 **[!UICONTROL 配置列]** 并单击列名以将其添加或从视图中删除。

![](../images/merge-policies/adjust-view.png)

## 创建合并策略 {#create-a-merge-policy}

要创建新的合并策略，请选择 **[!UICONTROL 创建合并策略]** 在合并策略选项卡上，输入新的合并策略工作流。

![突出显示创建按钮的合并策略登陆页面。](../images/merge-policies/create-new.png)

此 **[!UICONTROL 新建合并策略]** 工作流，要求您通过一系列引导式步骤为新合并策略提供重要信息。 以下各节概述了这些步骤。

![新的合并策略工作流。](../images/merge-policies/create.png)

## [!UICONTROL 配置] {#configure}

工作流中的第一步允许您通过提供基本信息配置合并策略。 此信息包括：

* **[!UICONTROL 名称]**：合并策略的名称应当是描述性的，但应简洁。
* **[!UICONTROL 架构类]**：与合并策略关联的XDM架构类。 这会指定为其创建此合并策略的架构类。 组织可以为每个架构类创建多个合并策略。 当前仅 [!UICONTROL XDM个人资料] 类在UI中可用。 您可以通过选择来预览架构类的合并架构 **[!UICONTROL 查看合并架构]**. 有关更多信息，请参阅以下部分： [查看合并架构](#view-union-schema) 随之而来的是。
* **[!UICONTROL ID拼接]**：此字段定义如何确定客户的相关身份。 身份拼接有两个可能的值，了解您选择的身份拼接类型将如何影响您的数据非常重要。 欲了解详情，请参阅 [合并策略概述](overview.md).
   * **[!UICONTROL 无]**：不执行身份拼接。
   * **[!UICONTROL 专用图]**：根据专用身份图执行身份拼合。
* **[!UICONTROL 默认合并策略]**：一个切换按钮，允许您选择此合并策略是否为贵组织的默认合并策略。 如果打开了选择器，系统会显示一条警告，要求您确认是否希望更改组织的默认合并策略。 请参阅 [合并策略概述](overview.md) 了解有关默认合并策略的更多信息。
  ![](../images/merge-policies/create-make-default.png)
* **[!UICONTROL Active-On-Edge合并策略]**：一个切换按钮，允许您选择此合并策略是否在Edge上处于活动状态。 要确保所有配置文件使用者在边缘上使用相同的视图，可以将合并策略标记为在边缘上处于活动状态。 为了在Edge上激活受众（标记为Edge受众），必须将其绑定到在Edge上标记为“活动”的合并策略。 如果受众为 **非** 与在edge上标记为“活动”的合并策略绑定，该受众在edge上不会标记为“活动”，而是会标记为流式受众。 此外，组织中的每个沙盒只能具有 **一** 在Edge上处于活动状态的合并策略。

必填字段完成后，您可以选择 **[!UICONTROL 下一个]** 以继续执行工作流。

![一个完整的“Configure（配置）”屏幕，其中的“Next（下一步）”按钮突出显示。](../images/merge-policies/create-complete.png)

## [!UICONTROL 查看合并架构] {#view-union-schema}

创建或编辑合并策略时，您可以通过选择 **[!UICONTROL 查看合并架构]**.

![](../images/merge-policies/view-union-schema.png)

这将打开 [!UICONTROL 查看合并架构] 对话框，显示与合并架构关联的所有参与架构、身份和关系。 您可以使用对话框以与访问合并架构相同的方式探索合并架构。 [!UICONTROL 合并架构] 选项卡 [!UICONTROL 配置文件] Platform UI的部分。

有关合并架构的详细信息，包括如何在 [!UICONTROL 合并架构] 选项卡或 [!UICONTROL 查看合并架构] 合并策略工作流中显示的对话框，请访问 [合并架构UI指南](../ui/union-schema.md).

![](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL 选择配置文件数据集] {#select-profile-datasets}

在 **[!UICONTROL 选择配置文件数据集]** 屏幕上，您必须选择 **[!UICONTROL 合并方法]** 要用于合并策略的区段。 屏幕上还显示了 [!UICONTROL 配置文件数据集] 与上个屏幕中选择的架构类相关的活动。

根据您选择的合并方法，所有配置文件数据集都将按上次更新的顺序（对时间戳排序）合并，否则您需要选择要包含在合并策略中的配置文件数据集以及合并它们的顺序（数据集优先级）。

有关合并方法的更多信息，请参阅 [合并策略概述](overview.md).

### 已排序的时间戳 {#timestamp-ordered-profile}

选择 **[!UICONTROL 已排序的时间戳]** 因为合并方法意味着最近更新数据集的属性将优先。 这适用于所有配置文件数据集。

>[!NOTE]
>
>括号中的数字，在 **[!UICONTROL 配置文件数据集]** (例如， `(37)` （在图中）显示将包含的配置文件数据集总数。

![](../images/merge-policies/timestamp-ordered.png)

### 数据集优先级 {#dataset-precedence-profile}

选择 **[!UICONTROL 数据集优先级]** 因为合并方法要求您选择用户档案数据集并手动排列其优先级。 列出的每个数据集还包含上次摄取批次的状态，或显示未将批次摄取到该数据集的通知。

您可以从数据集列表中选择最多50个要包含在合并策略中的数据集。

>[!NOTE]
>
>括号中的数字，在 **[!UICONTROL 配置文件数据集]** (例如， `(37)` （在图中）显示可供选择的配置文件数据集总数。

选择数据集后，它们会被添加到 **[!UICONTROL 选择数据集]** 部分，允许您拖放数据集并根据所需的优先级对其进行排序。 当在列表中调整数据集时，数据集旁边的序数（1、2、3等）将更新，显示优先级（1被赋予最高优先级，然后2，然后继续）。

选择数据集也会更新 **[!UICONTROL 合并架构]** 部分，显示每个数据集为其贡献数据的合并架构中的字段。 有关合并架构的更多信息，包括如何与UI中的可视化进行交互，请参阅 [合并架构UI指南](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence.png)

## [!UICONTROL 选择ExperienceEvent数据集] {#select-experienceevent-datasets}

工作流中的下一步要求您选择ExperienceEvent数据集。 此屏幕受您在 [[!UICONTROL 选择配置文件数据集]](#select-profile-datasets) 屏幕。

### 已排序的时间戳 {#timestamp-ordered-experienceevent}

如果您选择 **[!UICONTROL 已排序的时间戳]** 作为配置文件数据集的合并方法，最近更新的ExperienceEvent数据集的属性也将在此处优先。

>[!NOTE]
>
>括号中的数字，在 **[!UICONTROL ExperienceEvent数据集]** (例如， `(20)` （在显示的图像中）显示您的组织创建的、与您在合并策略配置屏幕中选择的架构类相关的ExperienceEvent数据集总数。

![](../images/merge-policies/timestamp-experienceevent.png)

### 数据集优先级 {#dataset-precedence-experienceevent}

如果您选择 **[!UICONTROL 数据集优先级]** 作为配置文件数据集的合并方法，您需要选择要包含的ExperienceEvent数据集。 您可以从数据集列表中选择最多50个ExperienceEvent数据集。

>[!NOTE]
>
>括号中的数字，在 **[!UICONTROL ExperienceEvent数据集]** (例如， `(20)` （在显示的图像中）显示您的组织创建的、与您在合并策略配置屏幕中选择的架构类相关的ExperienceEvent数据集总数。

选择数据集后，它们会显示在 [!UICONTROL 选择数据集] 部分。

ExperienceEvent数据集无法手动排序，相反，如果ExperienceEvent数据集中的属性属于同一配置文件片段，则将其附加到配置文件数据集。

与选择用户档案数据集类似，选择ExperienceEvent数据集也会更新 **[!UICONTROL 合并架构]** 部分，显示每个数据集为其贡献数据的合并架构中的字段。 有关合并架构的更多信息，包括如何与UI中的可视化进行交互，请参阅 [合并架构UI指南](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence-experienceevent.png)

## [!UICONTROL 请查看] {#review}

工作流的最后一步是审查合并策略。 此 **[!UICONTROL 审核]** 屏幕可显示有关合并策略的信息，包括选定的ID拼接方法、选定的合并方法，以及包含的数据集。 （要查看包含的所有配置文件或ExperienceEvent数据集，请选择要展开下拉列表的数据集数量。）

审阅屏幕上还包含 **[!UICONTROL 预览数据]** 显示使用合并策略的示例配置文件记录的表。 这使您可以在保存合并策略之前预览客户配置文件的外观。

请确保您查看合并策略配置并仔细预览数据，然后再选择 **[!UICONTROL 完成]** 完成创建工作流。

### 已排序的时间戳 {#timestamp-ordered-review}

如果您选择 **[!UICONTROL 已排序的时间戳]** 作为合并策略的合并方法，配置文件数据集列表包含贵组织创建的所有与架构类相关的数据集，且按时间戳顺序排列。 ExperienceEvent数据集的列表包含贵组织为所选架构类创建的所有数据集，并将附加到配置文件数据集。

此 **[!UICONTROL 预览数据]** 该表显示基于数据集时间戳排序的示例配置文件记录。 这使您可以在保存合并策略之前预览客户配置文件的外观。

![](../images/merge-policies/timestamp-review.png)

### 数据集优先级 {#dataset-precedence-review}

如果您选择 **[!UICONTROL 数据集优先级]** 作为合并策略的合并方法，配置文件和ExperienceEvent数据集的列表分别包含在创建工作流期间选择的配置文件和ExperienceEvent数据集。 用户档案数据集的顺序应与您在创建期间指定的优先级匹配。 如果不能，请使用 [!UICONTROL 返回] 按钮以返回到之前的工作流步骤并调整优先级。

此 **[!UICONTROL 预览数据]** 该表显示了使用选定数据集的示例配置文件记录。 这使您可以在保存合并策略之前预览客户配置文件的外观。

![](../images/merge-policies/dataset-precedence-review.png)

### 更新了合并策略列表 {#updated-list}

完成工作流以创建新合并策略后，您将返回到 **[!UICONTROL 合并策略]** 选项卡。 现在，组织的合并策略列表应包含刚刚创建的合并策略。

![](../images/merge-policies/new-merge-policy-created.png)

## 编辑合并策略

从 [!UICONTROL 合并策略] 选项卡，您可以修改为创建的现有合并策略 [!DNL XDM Individual Profile] class ，方法是选择 **[!UICONTROL 策略名称]** （对于要编辑的合并策略）。

![合并策略登陆页面](../images/merge-policies/select-edit.png)

当 **[!UICONTROL 编辑合并策略]** 屏幕中，您可以对名称进行更改并 [!UICONTROL ID拼接] 方法，并更改此策略是否为贵组织的默认合并策略。

选择 **[!UICONTROL 下一个]** 继续通过合并策略工作流更新合并策略中包含的合并方法和数据集。

![](../images/merge-policies/edit-screen.png)

进行必要的更改后，查看合并策略并选择 **[!UICONTROL 完成]** 以保存更改并返回至 [!UICONTROL 合并策略] 选项卡。

>[!WARNING]
>
>更改合并策略可能会影响分段和配置文件结果，因为它将改变解决数据冲突的方式。 在保存合并策略之前，请务必仔细查看对合并策略所做的更改。

![](../images/merge-policies/edit-review.png)

## 数据治理策略违规

创建或更新合并策略时，将执行检查以确定合并策略是否违反了由您的组织定义的任何数据使用策略。 数据使用策略是Adobe Experience Platform数据管理的一部分，是描述您可以在特定页面上执行或限制执行的营销操作类型的规则 [!DNL Platform] 数据。 例如，如果使用合并策略创建激活到第三方目标的受众，并且您的组织具有阻止将特定数据导出到第三方的数据使用策略，则您将收到 **[!UICONTROL 检测到数据治理策略违规]** 通知。

此通知包括已违反的数据使用策略列表，允许您通过从列表中选择策略来查看违规的详细资料。 选择违反的策略时， **[!UICONTROL 数据族系]** 选项卡提供了违规的原因和受影响的激活，每个选项卡都提供了有关如何违反数据使用策略的更多详细信息。

要了解有关如何在Adobe Experience Platform中执行数据管理的更多信息，请从阅读 [数据管理概述](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## 后续步骤

现在，您已为组织创建和配置合并策略，可以使用这些策略在Platform中调整客户配置文件视图，并根据配置文件数据创建受众。 请参阅 [分段概述](../../segmentation/home.md) 有关如何使用创建和使用受众的更多信息 [!DNL Experience Platform] 用户界面和API。
