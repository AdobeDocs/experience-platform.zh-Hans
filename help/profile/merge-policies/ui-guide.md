---
title: 合并策略UI指南
type: Documentation
description: 了解如何使用Adobe Experience Platform用户界面处理合并策略。
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2334'
ht-degree: 2%

---


# 合并策略 UI 指南

Adobe Experience Platform允许您从多个来源将数据片段整合在一起并组合它们，以便查看每个客户的完整视图。 在汇总此数据时，合并策略是[!DNL Experience Platform]用于确定数据优先顺序的规则以及将合并哪些数据以创建统一视图。

使用RESTful API或用户界面，您可以创建新的合并策略、管理现有策略以及为组织设置默认合并策略。 本指南提供了使用Adobe Experience Platform用户界面(UI)处理合并策略的分步说明。

要了解有关合并策略及其在Experience Platform中所扮演角色的更多信息，请从阅读[合并策略概述](overview.md)开始。

## 快速入门

本指南要求您实际了解几项重要的[!DNL Experience Platform]功能。 在遵循本指南之前，请查看以下服务的文档：

* [实时客户个人资料](../home.md)：根据来自多个来源的汇总数据提供统一的实时客户个人资料。
* [Adobe Experience Platform Identity Service](../../identity-service/home.md)：通过桥接从被摄取到[!DNL Experience Platform]中的不同数据源的标识来启用Real-time Customer Profile。
* [体验数据模型(XDM)](../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。

## 查看合并策略 {#view-merge-policies}

>[!CONTEXTUALHELP]
>id="platform_errors_uplib_101221_404"
>title="未找到合并策略"
>abstract="这意味着 Experience Platform 找不到所请求的合并策略。要解决此错误，请尝试以下解决方案之一：<ul><li>确保 URL 中列出了正确的合并策略 ID。</li><li>确保您尝试访问的合并策略具有正确的组织和沙盒组合。</li></ul>"

在[!DNL Experience Platform] UI中，您可以通过选择左侧导航中的&#x200B;**[!UICONTROL Profiles]**，然后选择&#x200B;**[!UICONTROL Merge Policies]**&#x200B;选项卡来开始使用合并策略。

此选项卡包含贵组织的所有现有合并策略的列表，以及每个合并策略的详细信息，包括策略名称、合并策略是否为默认合并策略以及合并策略相关的架构类。

![将显示合并策略浏览页。](../images/merge-policies/landing.png)

要选择显示哪些详细信息，或向显示添加其他列，请选择![列设置图标](../../images/icons/column-settings.png)并选择列名称以将其添加或从视图删除。

![显示自定义合并策略浏览页的可用选项。](../images/merge-policies/adjust-view.png)

## 创建合并策略 {#create-a-merge-policy}

要创建新的合并策略，请在“合并策略”选项卡上选择&#x200B;**[!UICONTROL Create merge policy]**&#x200B;以输入新的合并策略工作流。

![突出显示创建按钮的合并策略登陆页面。](../images/merge-policies/create-new.png)

**[!UICONTROL New merge policy]**&#x200B;工作流要求您通过一系列引导式步骤为新合并策略提供重要信息。 以下各节概述了这些步骤。

![新的合并策略工作流。](../images/merge-policies/create.png)

## [!UICONTROL Configure] {#configure}

工作流中的第一步允许您通过提供基本信息配置合并策略。 此信息包括：

* **[!UICONTROL Name]**：合并策略的名称应是描述性但简洁的。
* **[!UICONTROL Schema class]**：与合并策略关联的XDM架构类。 这会指定为其创建此合并策略的架构类。 组织可以为每个架构类创建多个合并策略。 当前UI中只有[!UICONTROL XDM Individual Profile]类可用。 您可以通过选择&#x200B;**[!UICONTROL View Union Schema]**&#x200B;预览架构类的合并架构。 有关详细信息，请参阅后面有关[查看合并架构](#view-union-schema)的部分。
* **[!UICONTROL ID stitching]**：此字段定义如何确定客户的相关标识。 身份拼接有两个可能的值，了解您选择的身份拼接类型将如何影响您的数据非常重要。 若要了解更多信息，请参阅[合并策略概述](overview.md)。
   * **[!UICONTROL None]**：不执行身份拼接。
   * **[!UICONTROL Private Graph]**：根据您的个人身份图执行身份拼合。
* **[!UICONTROL Default merge policy]**：一个切换按钮，允许您选择此合并策略是否为贵组织的默认合并策略。 如果打开了选择器，系统会显示一条警告，要求您确认是否希望更改组织的默认合并策略。 请参阅[合并策略概述](overview.md)，了解有关默认合并策略的更多信息。
  ![一个弹出窗口，说明将合并策略设置为默认合并策略时发生的情况。](../images/merge-policies/create-make-default.png)
* **[!UICONTROL Active-On-Edge Merge Policy]**：一个切换按钮，允许您选择此合并策略在Edge上是否处于活动状态。 要确保所有配置文件使用者在边缘上使用相同的视图，可以将合并策略标记为在边缘上处于活动状态。 为了在Edge上激活受众（标记为Edge受众），必须将其绑定到在Edge上标记为“活动”的合并策略。 如果受众未与在Edge上标记为“活动”的合并策略绑定&#x200B;**&#x200B;**，则该受众不会在Edge上标记为“活动”，而是会标记为流式受众。 此外，组织中的每个沙盒只能具有Edge上活动的&#x200B;**一个**&#x200B;合并策略。

必填字段完成后，您可以选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续工作流。

![突出显示了“下一步”按钮的已完成“配置”屏幕。](../images/merge-policies/create-complete.png)

## [!UICONTROL View Union Schema] {#view-union-schema}

创建或编辑合并策略时，您可以通过选择&#x200B;**[!UICONTROL View Union Schema]**&#x200B;来查看所选架构类的合并架构。

![新建合并策略工作流中突出显示“查看合并架构”按钮。](../images/merge-policies/view-union-schema.png)

这将打开[!UICONTROL View Union Schema]对话框，其中显示与合并架构关联的所有参与架构、标识和关系。 您可以使用该对话框以与访问Experience Platform UI [!UICONTROL Union Schema]部分中的[!UICONTROL Profiles]选项卡相同的方式浏览合并架构。

有关合并架构的详细信息，包括如何在合并策略工作流中显示的[!UICONTROL Union Schema]选项卡或[!UICONTROL View Union Schema]对话框中与其交互，请访问[合并架构UI指南](../ui/union-schema.md)。

![视图合并架构对话框。](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL Select Profile datasets] {#select-profile-datasets}

在&#x200B;**[!UICONTROL Select Profile datasets]**&#x200B;屏幕上，您必须选择要用于合并策略的&#x200B;**[!UICONTROL Merge method]**。 屏幕上还显示贵组织中与上一个屏幕上选择的架构类相关的[!UICONTROL Profile datasets]的总数。

根据您选择的合并方法，所有配置文件数据集都将按上次更新的顺序（对时间戳排序）合并，否则您需要选择要包含在合并策略中的配置文件数据集以及合并它们的顺序（数据集优先级）。

有关合并方法的详细信息，请参阅[合并策略概述](overview.md)。

>[!BEGINTABS]

>[!TAB 已排序的时间戳]

选择&#x200B;**[!UICONTROL Timestamp ordered]**&#x200B;作为合并方法意味着最近更新数据集的属性将优先。 这适用于所有配置文件数据集。

>[!NOTE]
>
>**[!UICONTROL Profile datasets]**&#x200B;旁边的括号中的数字（例如，所显示图像中的`(37)`）显示将包含的配置文件数据集的总数。

![显示所选时间戳顺序合并方法的图像。](../images/merge-policies/timestamp-ordered.png)

>[!TAB 数据集优先级]

选择&#x200B;**[!UICONTROL Dataset precedence]**&#x200B;作为合并方法需要您选择配置文件数据集并手动排列其优先级。 列出的每个数据集还包含上次摄取批次的状态，或显示未将批次摄取到该数据集的通知。

您可以从数据集列表中选择最多50个要包含在合并策略中的数据集。

>[!NOTE]
>
>**[!UICONTROL Profile datasets]**&#x200B;旁边的括号中的数字（例如，所显示图像中的`(37)`）显示可供选择的配置文件数据集总数。

选择数据集后，这些数据集将添加到&#x200B;**[!UICONTROL Select datasets]**&#x200B;部分，允许您拖放数据集并根据所需的优先级对其进行排序。 当在列表中调整数据集时，数据集旁边的序数（1、2、3等）将更新，显示优先级（1被赋予最高优先级，然后2，然后继续）。

选择数据集也会更新&#x200B;**[!UICONTROL Union schema]**&#x200B;部分，显示每个数据集贡献数据的合并架构中的字段。 有关合并架构的更多信息，包括如何与UI中的可视化进行交互，请参阅[合并架构UI指南](../ui/union-schema.md)

![显示已选择数据集优先级的图像，以及您需要选择是否选择该选项的相应设置。](../images/merge-policies/dataset-precedence.png)

>[!ENDTABS]

## [!UICONTROL Select ExperienceEvent datasets] {#select-experienceevent-datasets}

工作流中的下一步要求您选择ExperienceEvent数据集。 此屏幕受您在[[!UICONTROL Select Profile datasets]](#select-profile-datasets)屏幕上选择的合并方法影响。

>[!BEGINTABS]

>[!TAB 已排序的时间戳]

如果您选择&#x200B;**[!UICONTROL Timestamp ordered]**&#x200B;作为配置文件数据集的合并方法，则最近更新的ExperienceEvent数据集的属性也将在此处优先。

>[!NOTE]
>
>**[!UICONTROL ExperienceEvent datasets]**&#x200B;旁边的括号中的数字（例如，图中的`(1)`）显示您的组织创建的、与您在合并策略配置屏幕中选择的架构类相关的ExperienceEvent数据集总数。

![显示可与架构类相关的ExperienceEvent数据集总数。](../images/merge-policies/timestamp-experienceevent.png)

>[!TAB 数据集优先级]

如果您选择&#x200B;**[!UICONTROL Dataset precedence]**&#x200B;作为配置文件数据集的合并方法，则需要选择要包含的ExperienceEvent数据集。 您可以从数据集列表中选择最多50个ExperienceEvent数据集。

>[!NOTE]
>
>**[!UICONTROL ExperienceEvent datasets]**&#x200B;旁边的括号中的数字（例如，图中的`(1)`）显示您的组织创建的、与您在合并策略配置屏幕中选择的架构类相关的ExperienceEvent数据集总数。

选择数据集后，它们会显示在[!UICONTROL Select datasets]部分中。

ExperienceEvent数据集无法手动排序，相反，如果ExperienceEvent数据集中的属性属于同一配置文件片段，则将其附加到配置文件数据集。

与选择用户档案数据集类似，选择ExperienceEvent数据集也会更新&#x200B;**[!UICONTROL Union schema]**&#x200B;部分，显示每个数据集贡献数据的合并架构中的字段。 有关合并架构的更多信息，包括如何与UI中的可视化进行交互，请参阅[合并架构UI指南](../ui/union-schema.md)。

![显示可选的ExperienceEvent数据集。](../images/merge-policies/dataset-precedence-experienceevent.png)

>[!ENDTABS]

## [!UICONTROL Review] {#review}

工作流的最后一步是审查合并策略。 **[!UICONTROL Review]**&#x200B;屏幕显示有关合并策略的信息，包括选定的ID拼接方法、选定的合并方法和包含的数据集。 （要查看包含的所有配置文件或ExperienceEvent数据集，请选择要展开下拉列表的数据集数量。）

审阅屏幕上还包含一个&#x200B;**[!UICONTROL Preview data]**&#x200B;表，该表显示了使用合并策略的示例配置文件记录。 这使您可以在保存合并策略之前预览客户配置文件的外观。

在选择&#x200B;**[!UICONTROL Finish]**&#x200B;以完成创建工作流之前，请确保仔细查看合并策略配置并预览数据。

>[!BEGINTABS]

>[!TAB 已排序的时间戳]

如果您选择&#x200B;**[!UICONTROL Timestamp ordered]**&#x200B;作为合并策略的合并方法，配置文件数据集列表将按时间戳顺序包含贵组织创建的所有与架构类相关的数据集。 ExperienceEvent数据集的列表包含贵组织为所选架构类创建的所有数据集，并将附加到配置文件数据集。

**[!UICONTROL Preview data]**&#x200B;表根据数据集的时间戳顺序显示样本配置文件记录。 这使您可以在保存合并策略之前预览客户配置文件的外观。

选择&#x200B;**[!UICONTROL Finish]**&#x200B;以创建新的合并策略。

![将显示“审阅”页。 此页允许您查看新创建的合并策略的详细信息。](../images/merge-policies/timestamp-review.png)

>[!TAB 数据集优先级]

如果选择&#x200B;**[!UICONTROL Dataset precedence]**&#x200B;作为合并策略的合并方法，则Profile和ExperienceEvent数据集的列表将分别包含在创建工作流期间选择的Profile和ExperienceEvent数据集。 用户档案数据集的顺序应与您在创建期间指定的优先级匹配。 如果不适用，请使用[!UICONTROL Back]按钮返回至之前的工作流步骤并调整优先级。

**[!UICONTROL Preview data]**&#x200B;表显示使用选定数据集的示例配置文件记录。 这使您可以在保存合并策略之前预览客户配置文件的外观。

选择&#x200B;**[!UICONTROL Finish]**&#x200B;以创建新的合并策略。

![将显示“审阅”页。 此页允许您查看新创建的合并策略的详细信息。](../images/merge-policies/dataset-precedence-review.png)

>[!ENDTABS]

## 编辑合并策略 {#edit}

在[!UICONTROL Merge Policies]选项卡中，您可以通过为要编辑的合并策略选择[!DNL XDM Individual Profile]来修改为&#x200B;**[!UICONTROL Policy name]**&#x200B;类创建的现有合并策略。

显示&#x200B;**[!UICONTROL Edit merge policy]**&#x200B;屏幕时，您可以更改名称和[!UICONTROL ID stitching]方法，以及更改此策略是否为贵组织的默认合并策略。

选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续通过合并策略工作流更新合并策略中包含的合并方法和数据集。

![将显示编辑合并策略工作流。](../images/merge-policies/edit-screen.png)

进行必要的更改后，查看合并策略并选择&#x200B;**[!UICONTROL Finish]**&#x200B;以保存更改并返回[!UICONTROL Merge policies]选项卡。

>[!WARNING]
>
>更改合并策略可能会影响分段和配置文件结果，因为它将改变解决数据冲突的方式。 在保存合并策略之前，请务必仔细查看对合并策略所做的更改。

![将显示编辑策略工作流的审核页面。](../images/merge-policies/edit-review.png)

## 数据治理策略违规

创建或更新合并策略时，将执行检查以确定合并策略是否违反了由您的组织定义的任何数据使用策略。 数据使用策略是Adobe Experience Platform数据管理的一部分，是描述允许或限制您对特定[!DNL Experience Platform]数据执行的营销操作类型的规则。

例如，如果使用合并策略创建激活到第三方目标的受众，并且贵组织具有阻止将特定数据导出到第三方的数据使用策略，则在尝试保存合并策略时，您将收到&#x200B;**[!UICONTROL Data governance policy violation detected]**&#x200B;通知。

此通知包括已违反的数据使用策略列表，允许您通过从列表中选择策略来查看违规的详细资料。 在选择违反的策略时，**[!UICONTROL Data lineage]**&#x200B;选项卡会提供违规的原因以及受影响的激活，每个选项卡都会提供有关如何违反数据使用策略的更多详细信息。

要了解有关如何在Adobe Experience Platform中执行数据管理的更多信息，请从阅读[数据管理概述](../../data-governance/home.md)开始。

## 后续步骤

现在您已经为组织创建并配置了合并策略，接下来可以使用这些策略调整Experience Platform中客户配置文件的视图，并根据配置文件数据创建受众。 有关如何使用[用户界面和API创建和使用受众的更多信息，请参阅](../../segmentation/home.md)分段概述[!DNL Experience Platform]。
