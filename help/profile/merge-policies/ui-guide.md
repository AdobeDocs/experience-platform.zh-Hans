---
keywords: Experience Platform；配置文件；实时客户配置文件；合并策略；UI；用户界面；按时间戳排序；数据集优先级
title: 合并策略UI指南
type: Documentation
description: 在Experience Platform中将来自多个源的数据汇集在一起时，合并策略是Platform用来确定数据优先级和合并哪些数据以创建统一视图的规则。 本指南提供了使用Adobe Experience Platform用户界面使用合并策略的分步说明。
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: e94756254a24ecadd7359589cd14cfb0745c789c
workflow-type: tm+mt
source-wordcount: '2321'
ht-degree: 0%

---


# 合并策略UI指南

Adobe Experience Platform允许您从多个来源将数据片段合并在一起，以便查看各个客户的完整视图。 将此数据整合在一起时，合并策略是 [!DNL Platform] 用于确定数据的优先级以及将合并哪些数据来创建统一视图。

使用RESTful API或用户界面，您可以创建新的合并策略、管理现有策略，并为您的组织设置默认的合并策略。 本指南提供了使用Adobe Experience Platform用户界面(UI)处理合并策略的分步说明。

要进一步了解合并策略以及它们在Experience Platform中的角色，请首先阅读 [合并策略概述](overview.md).

## 快速入门

本指南需要对以下几个重要事项有充分的了解 [!DNL Experience Platform] 功能。 在阅读本指南之前，请查阅以下服务的文档：

* [实时客户资料](../home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
* [Adobe Experience Platform Identity Service](../../identity-service/home.md):通过将来自不同数据源的身份桥接到中，从而支持实时客户资料 [!DNL Platform].
* [体验数据模型(XDM)](../../xdm/home.md):标准化框架， [!DNL Platform] 组织客户体验数据。

## 查看合并策略 {#view-merge-policies}

在 [!DNL Experience Platform] UI中，您可以通过选择 **[!UICONTROL 用户档案]** ，然后选择 **[!UICONTROL 合并策略]** 选项卡。 此选项卡包含贵组织的所有现有合并策略的列表，以及每个合并策略的详细信息，包括策略名称、合并策略是否是默认合并策略以及与合并策略相关的架构类。

![“合并策略”登录页](../images/merge-policies/landing.png)

要选择显示的详细信息，或向显示内容添加其他列，请选择 **[!UICONTROL 配置列]** ，然后单击列名称以在视图中添加或删除该列。

![](../images/merge-policies/adjust-view.png)

## 创建合并策略 {#create-a-merge-policy}

要创建新合并策略，请选择 **[!UICONTROL 创建合并策略]** 在合并策略选项卡上，输入新的合并策略工作流。

![“合并策略”登陆页面上突出显示了“创建”按钮。](../images/merge-policies/create-new.png)

的 **[!UICONTROL 新合并策略]** 工作流，要求您通过一系列引导式步骤为新合并策略提供重要信息。 以下各节概述了这些步骤。

![新的合并策略工作流。](../images/merge-policies/create.png)

## [!UICONTROL 配置] {#configure}

利用工作流中的第一步，可通过提供基本信息来配置合并策略。 此信息包括：

* **[!UICONTROL 名称]**:合并策略的名称应当具有描述性且应简洁明了。
* **[!UICONTROL 模式类]**:与合并策略关联的XDM架构类。 这会指定为其创建此合并策略的架构类。 组织可以为每个架构类创建多个合并策略。 当前仅 [!UICONTROL XDM个人配置文件] 类在UI中可用。 您可以通过选择 **[!UICONTROL 查看并集架构]**. 有关更多信息，请参阅 [查看并集架构](#view-union-schema) 接下来。
* **[!UICONTROL ID拼合]**:此字段定义如何确定客户的相关身份。 身份拼合有两个可能的值，请务必了解您选择的身份拼合类型将如何影响数据。 要了解更多信息，请参阅 [合并策略概述](overview.md).
   * **[!UICONTROL 无]**:不执行身份拼合。
   * **[!UICONTROL 专用图]**:根据您的专用身份图执行身份拼合。
* **[!UICONTROL 默认合并策略]**:一个切换按钮，用于选择此合并策略是否将是贵组织的默认策略。 如果选择器已打开，则会显示一条警告，要求您确认要更改组织的默认合并策略。 请参阅 [合并策略概述](overview.md) 了解有关默认合并策略的更多信息。
   ![](../images/merge-policies/create-make-default.png)
* **[!UICONTROL 边缘活动合并策略]**:用于选择此合并策略是否在边缘上处于活动状态的切换按钮。 为确保所有配置文件使用者在边缘上使用相同的视图，可以将合并策略标记为边缘上的活动策略。 要使区段在边缘上激活（标记为边缘区段），必须将其绑定到在边缘上标记为活动的合并策略。 如果区段为 **not** 绑定到在边缘上标记为活动的合并策略，该区段在边缘上不会标记为活动，并且将标记为流区段。 此外，组织中的每个沙箱只能 **one** 边缘上处于活动状态的合并策略。

填写必填字段后，您可以选择 **[!UICONTROL 下一个]** 以继续工作流。

![选中“Next（下一步）”按钮的完整“Configure（配置）”屏幕。](../images/merge-policies/create-complete.png)

## [!UICONTROL 查看并集架构] {#view-union-schema}

创建或编辑合并策略时，您可以通过选择 **[!UICONTROL 查看并集架构]**.

![](../images/merge-policies/view-union-schema.png)

这将打开 [!UICONTROL 查看并集架构] 对话框，显示与并集模式关联的所有参与模式、标识和关系。 您可以使用对话框以与访问 [!UICONTROL 并集架构] 选项卡 [!UICONTROL 用户档案] 部分。

有关并集模式的详细信息，包括如何在 [!UICONTROL 并集架构] 选项卡 [!UICONTROL 查看并集架构] “合并策略”工作流中显示的对话框，请访问 [并集架构UI指南](../ui/union-schema.md).

![](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL 选择配置文件数据集] {#select-profile-datasets}

在 **[!UICONTROL 选择配置文件数据集]** 屏幕，则必须选择 **[!UICONTROL 合并方法]** 用于合并策略的URL。 屏幕上还显示 [!UICONTROL 配置文件数据集] 与在上一屏幕中选择的架构类相关的组织中。

根据您选择的合并方法，所有配置文件数据集都将按上次更新的顺序（按时间戳排序）进行合并，或者您将需要选择要包含在合并策略中的配置文件数据集以及合并它们的顺序（数据集优先级）。

有关合并方法的更多信息，请参阅 [合并策略概述](overview.md).

### 已排序时间戳 {#timestamp-ordered-profile}

选择 **[!UICONTROL 已排序时间戳]** 因为合并方法意味着将优先使用最近更新数据集的属性。 这适用于所有配置文件数据集。

>[!NOTE]
>
>旁边括号中的数字 **[!UICONTROL 配置文件数据集]** (例如， `(37)` )显示将包含的配置文件数据集总数。

![](../images/merge-policies/timestamp-ordered.png)

### 数据集优先级 {#dataset-precedence-profile}

选择 **[!UICONTROL 数据集优先级]** 由于合并方法要求您选择配置文件数据集并手动排列其优先级。 列出的每个数据集还包含上次摄取的批次的状态，或显示一条通知，指示尚未将任何批次摄取到该数据集。

您可以从数据集列表中选择最多50个要包含在合并策略中的数据集。

>[!NOTE]
>
>旁边括号中的数字 **[!UICONTROL 配置文件数据集]** (例如， `(37)` )显示可供选择的配置文件数据集总数。

选择数据集后，会将它们添加到 **[!UICONTROL 选择数据集]** 区域，允许您拖放数据集并根据所需的优先级对它们进行排序。 随着数据集在列表中进行调整，数据集旁边的序数（1、2、3等）将会更新，并显示优先级（1个被赋予最高优先级，然后2个，等等）。

选择数据集也会更新 **[!UICONTROL 并集模式]** 部分，显示并集架构中每个数据集向其提供数据的字段。 有关并集模式（包括如何与UI中的可视化进行交互）的更多信息，请参阅 [并集架构UI指南](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence.png)

## [!UICONTROL 选择ExperienceEvent数据集] {#select-experienceevent-datasets}

工作流的下一步要求您选择ExperienceEvent数据集。 此屏幕受您在 [[!UICONTROL 选择配置文件数据集]](#select-profile-datasets) 屏幕。

### 已排序时间戳 {#timestamp-ordered-experienceevent}

如果已选择 **[!UICONTROL 已排序时间戳]** 作为用户档案数据集的合并方法，此处还将优先使用最近更新的ExperienceEvent数据集中的属性。

>[!NOTE]
>
>旁边括号中的数字 **[!UICONTROL ExperienceEvent数据集]** (例如， `(20)` （如图所示）显示由您的组织创建的与您在合并策略配置屏幕中选择的架构类相关的ExperienceEvent数据集总数。

![](../images/merge-policies/timestamp-experienceevent.png)

### 数据集优先级 {#dataset-precedence-experienceevent}

如果已选择 **[!UICONTROL 数据集优先级]** 作为用户档案数据集的合并方法，您将需要选择要包含的ExperienceEvent数据集。 您最多可以从数据集列表中选择50个ExperienceEvent数据集。

>[!NOTE]
>
>旁边括号中的数字 **[!UICONTROL ExperienceEvent数据集]** (例如， `(20)` （如图所示）显示由您的组织创建的与您在合并策略配置屏幕中选择的架构类相关的ExperienceEvent数据集总数。

选择数据集后，它们会显示在 [!UICONTROL 选择数据集] 中。

无法手动对ExperienceEvent数据集进行排序，相反，如果ExperienceEvent数据集中的属性属于同一配置文件片段，则这些属性会附加到配置文件数据集。

与选择用户档案数据集类似，选择ExperienceEvent数据集也会更新 **[!UICONTROL 并集模式]** 部分，显示并集架构中每个数据集向其提供数据的字段。 有关并集模式（包括如何与UI中的可视化进行交互）的更多信息，请参阅 [并集架构UI指南](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence-experienceevent.png)

## [!UICONTROL 审阅] {#review}

工作流的最后一步是查看合并策略。 的 **[!UICONTROL 审阅]** 屏幕显示有关合并策略的信息，包括选择的ID拼合方法、选择的合并方法以及包含的数据集。 （要查看包含的所有配置文件或ExperienceEvent数据集，请选择要展开下拉列表的数据集数。）

审阅屏幕中还包含 **[!UICONTROL 预览数据]** 显示使用合并策略的示例配置文件记录的表。 这样，您就可以在保存合并策略之前预览客户配置文件的外观。

在选择 **[!UICONTROL 完成]** 以完成创建工作流。

### 已排序时间戳 {#timestamp-ordered-review}

如果已选择 **[!UICONTROL 已排序时间戳]** 作为合并策略的合并方法，配置文件数据集列表按时间戳顺序包含由贵组织创建的与架构类相关的所有数据集。 ExperienceEvent数据集列表包含您的组织为所选架构类创建的所有数据集，这些数据集将附加到配置文件数据集。

的 **[!UICONTROL 预览数据]** 表格根据数据集的时间戳顺序显示示例配置文件记录。 这样，您就可以在保存合并策略之前预览客户配置文件的外观。

![](../images/merge-policies/timestamp-review.png)

### 数据集优先级 {#dataset-precedence-review}

如果已选择 **[!UICONTROL 数据集优先级]** 作为合并策略的合并方法，配置文件数据集和ExperienceEvent数据集列表仅包含您在创建工作流中选择的配置文件数据集和ExperienceEvent数据集。 配置文件数据集的顺序应与创建期间指定的优先级匹配。 如果没有，请使用 [!UICONTROL 返回] 按钮以返回到之前的工作流步骤并调整优先级。

的 **[!UICONTROL 预览数据]** 表格显示使用选定数据集的样例配置文件记录。 这样，您就可以在保存合并策略之前预览客户配置文件的外观。

![](../images/merge-policies/dataset-precedence-review.png)

### 更新了合并策略列表 {#updated-list}

完成创建新合并策略的工作流后，您将返回到 **[!UICONTROL 合并策略]** 选项卡。 现在，贵组织的合并策略列表应包含刚刚创建的合并策略。

![](../images/merge-policies/new-merge-policy-created.png)

## 编辑合并策略

从 [!UICONTROL 合并策略] 选项卡，您可以修改为 [!DNL XDM Individual Profile] 类 **[!UICONTROL 策略名称]** 对于要编辑的合并策略。

![“合并策略”登录页](../images/merge-policies/select-edit.png)

当 **[!UICONTROL 编辑合并策略]** 屏幕中，您可以对名称和 [!UICONTROL ID拼合] 方法，并更改此策略是否是贵组织的默认合并策略。

选择 **[!UICONTROL 下一个]** 继续执行合并策略工作流，以更新合并策略中包含的合并方法和数据集。

![](../images/merge-policies/edit-screen.png)

进行必要更改后，请查看合并策略并选择 **[!UICONTROL 完成]** ，以保存所做的更改并返回到 [!UICONTROL 合并策略] 选项卡。

>[!WARNING]
>
>更改合并策略可能会影响分段和配置文件结果，因为它会更改解决数据冲突的方式。 在保存合并策略之前，请务必仔细查看对其所做的更改。

![](../images/merge-policies/edit-review.png)

## 违反数据管理策略

创建或更新合并策略时，会执行一项检查，以确定合并策略是否违反了您的组织定义的任何数据使用策略。 数据使用策略是Adobe Experience Platform数据管理的一部分，它是描述您允许或限制在特定环境中执行的营销操作类型的规则 [!DNL Platform] 数据。 例如，如果使用合并策略创建一个激活到第三方目标的区段，并且您的组织有一个数据使用策略阻止将特定数据导出到第三方，则您将收到 **[!UICONTROL 检测到数据管理策略违规]** 通知。

此通知包含违反的数据使用策略列表，允许您通过从列表中选择策略来查看违规的详细信息。 选择违反的策略后， **[!UICONTROL 数据谱系]** 选项卡提供了违规原因和受影响的激活，每个选项卡都提供了有关如何违反数据使用策略的详细信息。

要详细了解如何在Adobe Experience Platform中执行数据管理，请首先阅读 [数据管理概述](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## 后续步骤

现在，您已为组织创建和配置合并策略，接下来可以使用这些策略来调整Platform中客户用户档案的视图，并根据用户档案数据创建受众区段。 请参阅 [分段概述](../../segmentation/home.md) 有关如何使用 [!DNL Experience Platform] UI和API。
