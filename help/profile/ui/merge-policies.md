---
keywords: Experience Platform;用户档案；实时客户用户档案；合并策略；UI；用户界面；时间戳排序；数据集优先级
title: 合并策略UI指南
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform使您能够将来自多个来源的数据片段整合在一起，并将它们合并在一起，以全面视图每位客户。 整合这些数据时，合并策略是平台用来确定如何对数据进行优先级排序以及将哪些数据合并以创建统一视图的规则。
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '2879'
ht-degree: 0%

---

# 合并策略UI指南

Adobe Experience Platform使您能够将来自多个来源的数据片段整合在一起，并将它们合并在一起，以全面视图每位客户。 合并策略是[!DNL Platform]用来确定如何对数据进行优先级排序以及将哪些数据合并以创建统一视图的规则。

例如，如果一个渠道跨多个用户档案与您的品牌互动，则您的组织将在多个数据集中显示与该单个客户相关的多个片段。 当这些片段被收录到平台中时，它们会合并在一起，以便为该客户创建单一用户档案。 当来自多个来源的列表发生冲突(例如，一个片段将客户为“单一”，而其他片段将客户列表为“已婚”)时，合并策略将确定要包含在个人用户档案中的信息。

使用REST风格的API或用户界面，您可以创建新的合并策略、管理现有策略并为组织设置默认的合并策略。 本指南提供使用Adobe Experience Platform用户界面(UI)处理合并策略的分步说明。

如果您希望使用[!DNL Real-time Customer Profile] API来使用合并策略，请按照[合并策略API指南](../api/merge-policies.md)中概述的说明进行操作。

## 入门指南

本指南要求对几个重要的[!DNL Experience Platform]功能进行有效的了解。 在遵循本指南或使用用户档案 API之前，请查看以下服务的文档：

* [实时客户用户档案](../home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。
* [Adobe Experience Platform Identity Service](../../identity-service/home.md):通过连接来自不同数据源的身份并融入其中，实现实时客户用户档案 [!DNL Platform]。
* [体验数据模型(XDM)](../../xdm/home.md):组织客户体验数 [!DNL Platform] 据的标准化框架。

## 合并方法{#merge-methods}

每个用户档案片段包含个人可能存在的身份总数中只有一个身份的信息。 当将这些数据合并到一起以形成客户用户档案时，可能会导致该信息发生冲突，并且必须指定优先级。 通过选择合并方法，可以指定在数据集之间发生合并冲突时要排定优先级的数据集属性。

合并策略有两种可能的合并方法。 以下各种方法都进行了概述，并在以下各节中提供了更多详细信息：

* **[!UICONTROL Timestamp ordered]:** 在冲突事件中，优先级被赋予最近更新的用户档案片段。
   * **自定义时间戳：** [!UICONTROL Timestamp ordered] 还支持自定义时间戳，当合并同一数据集（多个身份）或跨数据集的数据时，这些时间戳优先于系统时间戳。要了解详细信息，请参阅关于使用自定义时间戳](#custom-timestamps)的部分。[
* **[!UICONTROL Dataset precedence]:** 在冲突事件中，根据冲突产生的数据集优先用户档案片段。选择此选项时，必须选择相关数据集及其优先级顺序。

### 按顺序{#timestamp-ordered}排列的时间戳

当用户档案记录被摄入Experience Platform时，在摄取时获得系统时间戳并添加到记录。 当选择&#x200B;**[!UICONTROL Timestamp ordered]**&#x200B;作为合并策略的合并方法时，将基于系统时间戳合并用户档案。 换句话说，合并是根据将记录引入平台的时间戳完成的。

#### 使用自定义时间戳{#custom-timestamps}

有时，在某些用例中，需要提供自定义时间戳并使合并策略遵守自定义时间戳而不是系统时间戳。 这包括回填数据或确保在记录摄取不顺序时事件的正确顺序。

要使用自定义时间戳，必须将&#x200B;**[!UICONTROL External Source System Audit Details]模式字段组**&#x200B;添加到用户档案模式。 添加后，可以使用`lastUpdatedDate`字段填充自定义时间戳。 在摄取记录时填充`lastUpdatedDate`字段，Experience Platform将使用该字段跨数据集合并记录。 如果`lastUpdatedDate`不存在或未填充，平台将继续使用系统时间戳。

>[!NOTE]
>
>必须确保在同一记录上引入更新时填充`lastUpdatedDate`时间戳。

以下屏幕截图显示[!UICONTROL External Source System Audit Details]字段组中的字段。 有关使用平台UI处理模式的分步说明(包括如何向模式添加字段组)，请访问[教程，了解如何使用UI](../../xdm/tutorials/create-schema-ui.md)创建模式。

![](../images/merge-policies/custom-timestamp-field-group.png)

要使用API使用自定义时间戳，请参阅[使用自定义时间戳](../api/merge-policies.md#custom-timestamps)的合并策略端点指南部分。

### 数据集优先级{#dataset-precedence}

选择&#x200B;**[!UICONTROL Dataset precedence]**&#x200B;作为合并策略的合并方法时，您可以根据用户档案片段来自的数据集为其指定优先级。 一个示例用例是，如果您的组织在一个数据集中存在信息，而该数据集中的数据优先或受信任，则该数据集中的数据优先或受信任。

要使用&#x200B;**[!UICONTROL Dataset precedence]**&#x200B;创建合并策略，必须选择包含的用户档案和ExperienceEvent数据集，然后可以手动对用户档案数据集进行优先级排序。 选择和排序数据集后，将优先级最高的数据集、第二个数据集等。

## [!UICONTROL ID stitching] {#id-stitching}

身份拼接([!UICONTROL ID stitching])是识别数据片段并将它们组合在一起以形成完整用户档案记录的过程。 为了说明不同的拼接行为，请考虑使用两个不同电子邮件地址与品牌互动的单个客户。

* **[!UICONTROL None]:** 选择此选项后，ID将不会拼接在一起。当发生分段时，可能属于同一人的身份将不会拼合在一起，而分段仅在确定客户是否有资格获得区段会员资格时才会考虑附加到每个单独ID的属性。 这可能导致一个客户具有多个用户档案，每个用户档案可能有资格访问不同的细分，从而向同一客户发送多个营销消息。
* **[!UICONTROL Private graph]:** 选择专用图时，与同一个人相关的多个身份将拼接在一起。这导致客户具有单个用户档案，并允许分段在确定区段资格时考虑来自多个相关身份的多个属性。 在此方案中，用户档案可能具有单一的客户，根据不同身份的属性组合有资格获得一个细分，并且只接收一条营销消息。

要进一步了解身份及其在生成用户档案和区段中的作用，请首先阅读[Identity Service概述](../../identity-service/home.md)。

## 默认合并策略{#default-merge-policy}

组织可以创建默认合并策略供其组织在合并用户档案片段时使用。 这样，用户在执行Experience Platform操作(如查看客户用户档案或创建区段)时可轻松选择默认策略。 在大多数情况下，除非指定其他合并策略，否则将使用默认的合并策略。

每个组织都可以创建与单个XDM模式类相关的多个合并策略，但每个类只能声明一个默认合并策略。 例如，您的组织可能具有与[!DNL XDM Individual Profile]类相关的默认合并策略和自定义构建的“产品库存”类的其他默认合并策略。

如果您新建了一个合并策略并将其设置为默认策略，则系统将自动更新以前的默认合并策略，使其不再是默认策略。

>[!WARNING]
>
>用户档案计数和具有现有关联默认合并策略的区段可能会受到影响。 应用了默认合并策略的任何区段都将更新为新的默认合并策略。

## 视图合并策略{#view-merge-policies}

在[!DNL Experience Platform] UI中，您可以开始使用合并策略，方法是在左侧导航中选择&#x200B;**[!UICONTROL Profiles]**，然后选择&#x200B;**[!UICONTROL Merge Policies]**&#x200B;选项卡。 此选项卡包含组织的所有现有合并策略的列表，以及每个合并策略的详细信息，包括策略名称、合并策略是否为默认合并策略以及合并策略所关联的模式类。

![合并策略登陆页](../images/merge-policies/landing.png)

要选择哪些详细信息可见，或要向显示屏添加其他列，请选择&#x200B;**[!UICONTROL Configure columns]**&#x200B;并单击列名以将其添加或从视图中删除。

![](../images/merge-policies/adjust-view.png)

## 创建合并策略{#create-a-merge-policy}

要创建新的合并策略，请在合并策略选项卡上选择&#x200B;**[!UICONTROL Create merge policy]**。

![合并策略登陆页，并突出显示创建按钮。](../images/merge-policies/create-new.png)

在&#x200B;**[!UICONTROL New merge policy]**&#x200B;工作流屏幕上，您可以通过一系列引导步骤提供新合并策略的重要信息。

![新的合并策略工作流。](../images/merge-policies/create.png)

### [!UICONTROL Configure] {#configure}

在工作流的第一步中，您可以通过提供基本信息来配置合并策略。 此信息包括：

* **[!UICONTROL Name]**:合并策略的名称应具有描述性，但应简明。
* **[!UICONTROL Schema class]**:与合并策略关联的XDM模式类。它指定为其创建此合并策略的模式类。 组织可以为每个模式类创建多个合并策略。 当前，UI中仅提供[!UICONTROL XDM Individual Profile]类。 可以通过选择&#x200B;**[!UICONTROL View Union Schema]**&#x200B;预览模式类的合并模式。 有关详细信息，请参阅关于[查看以下合并模式](#view-union-schema)的部分。
* **[!UICONTROL ID stitching]**:此字段定义如何确定客户的相关身份。请参阅本指南中前面关于[ID strunting](#id-stitching)的部分，以了解更多信息。 有两个可能的值：
   * **[!UICONTROL None]**:不执行身份拼接。
   * **[!UICONTROL Private Graph]**:根据您的个人身份图执行身份拼接。
* **[!UICONTROL Default merge policy]**:一个切换按钮，允许您选择此合并策略是否将是组织的默认策略。如果选择器已切换，则会显示一条警告，要求您确认要更改组织的默认合并策略。 请参阅本指南中前面关于[默认合并策略](#default-merge-policy)的部分以了解更多信息。
   ![](../images/merge-policies/create-make-default.png)

填写完所需字段后，您可以选择&#x200B;**[!UICONTROL Next]**&#x200B;继续工作流。

![高亮显示“下一步”按钮的完整“配置”屏幕。](../images/merge-policies/create-complete.png)

#### [!UICONTROL View Union Schema] {#view-union-schema}

在创建或编辑合并策略时，可以通过选择&#x200B;**[!UICONTROL View Union Schema]**&#x200B;来视图所选模式类的合并模式。

![](../images/merge-policies/view-union-schema.png)

这将打开[!UICONTROL View Union Schema]对话框，显示与合并模式关联的所有参与模式、身份和关系。 您可以使用该对话框浏览合并模式，方式与访问平台UI的[!UICONTROL Profiles]部分中的[!UICONTROL Union Schema]选项卡相同。

有关合并模式的详细信息，包括如何在[!UICONTROL Union Schema]选项卡或合并策略工作流中显示的[!UICONTROL View Union Schema]对话框中与它们进行交互，请访问[合并模式UI指南](union-schema.md)。

![](../images/merge-policies/view-union-schema-dialog.png)


### [!UICONTROL Select Profile datasets] {#select-profile-datasets}

在&#x200B;**[!UICONTROL Select Profile datasets]**&#x200B;屏幕上，必须选择要用于合并策略的&#x200B;**[!UICONTROL Merge method]**。 屏幕上还显示与上一个屏幕上选择的模式类相关的组织中的[!UICONTROL Profile datasets]总数。

根据您选择的合并方法，所有用户档案数据集将按上次更新的顺序进行合并（时间戳排序），或者您需要选择合并策略中要包含的用户档案数据集以及合并它们的顺序（数据集优先级）。 有关合并方法的详细信息，请查看本文档前面提供的[合并方法](#merge-methods)部分。

#### 按顺序{#timestamp-ordered-profile}排列的时间戳

选择&#x200B;**[!UICONTROL Timestamp ordered]**&#x200B;作为合并方法意味着将优先选择最近更新的数据集中的属性。 这适用于所有用户档案数据集。

![](../images/merge-policies/timestamp-ordered.png)

#### 数据集优先级{#dataset-precedence-profile}

选择&#x200B;**[!UICONTROL Dataset precedence]**&#x200B;作为合并方法需要您选择用户档案数据集并手动对它们进行优先级排序。 列出的每个数据集还包含上次摄取的批次的状态，或显示未将任何批次摄取到该数据集的通知。

您可以从数据集列表中选择最多50个数据集以包含在合并策略中。 在选择数据集时，这些数据集将添加到&#x200B;**[!UICONTROL Select datasets]**&#x200B;部分，这样您就可以拖放数据集并根据所需的优先级对它们进行排序。 在列表中调整数据集时，数据集旁边的序号（1、2、3等）将更新，并显示优先级（1被赋予最高优先级，然后是2和之后）。

选择合并集也会更新&#x200B;**[!UICONTROL Union schema]**&#x200B;部分，其中显示每个数据集向其提供数据的模式中的字段。 有关合并模式的详细信息（包括如何与UI中的可视化进行交互），请参阅[合并模式UI指南](union-schema.md)

![](../images/merge-policies/dataset-precedence.png)

### [!UICONTROL Select ExperienceEvent datasets] {#select-experienceevent-datasets}

工作流的下一步要求您选择ExperienceEvent数据集。 此屏幕受您在[[!UICONTROL Select Profile datasets]](#select-profile-datasets)屏幕上选择的合并方法的影响。

此屏幕上还显示您的组织创建的与您在合并策略配置屏幕上选择的模式类相关的&#x200B;**[!UICONTROL ExperienceEvent datasets]**&#x200B;总数。

#### 按顺序{#timestamp-ordered-experienceevent}排列的时间戳

如果您选择&#x200B;**[!UICONTROL Timestamp ordered]**&#x200B;作为用户档案数据集的合并方法，则此处还将优先选择最近更新的ExperienceEvent数据集的属性。

![](../images/merge-policies/timestamp-experienceevent.png)

#### 数据集优先级{#dataset-precedence-experienceevent}

如果您选择&#x200B;**[!UICONTROL Dataset precedence]**&#x200B;作为用户档案数据集的合并方法，则需要选择要包含的ExperienceEvent数据集。 您可以从数据集列表中最多选择50个ExperienceEvent数据集。 选择数据集后，它们会显示在[!UICONTROL Select datasets]部分中。

无法手动对ExperienceEvent数据集进行排序，而是将ExperienceEvent数据集中的属性附加到用户档案数据集(如果它们是同一用户档案片段的一部分)。

与选择用户档案数据集类似，选择ExperienceEvent数据集也会更新&#x200B;**[!UICONTROL Union schema]**&#x200B;部分，显示每个数据集向其提供合并模式中的字段。 有关合并模式的详细信息（包括如何与UI中的可视化进行交互），请参阅[合并模式UI指南](union-schema.md)

![](../images/merge-policies/dataset-precedence-experienceevent.png)

### [!UICONTROL Review] {#review}

工作流的最后一步是查看合并策略。 **[!UICONTROL Review]**&#x200B;屏幕显示新合并策略的名称、新合并策略所基于的模式类、您选择的[!UICONTROL ID stitching]选项以及合并方法和合并策略中包含的数据集。 要视图包含的所有用户档案或ExperienceEvent数据集，请选择要展开下拉列表列表的数据集数。

请确保在选择&#x200B;**[!UICONTROL Finish]**&#x200B;以完成创建工作流之前仔细查看合并策略。

#### 按顺序{#timestamp-ordered-review}排列的时间戳

如果您选择&#x200B;**[!UICONTROL Timestamp ordered]**&#x200B;作为合并策略的合并方法，则用户档案数据集的列表将按时间戳顺序包括由您的组织创建的与模式类相关的所有数据集。 ExperienceEvent数据集的列表包括您的组织为所选模式类创建的所有数据集，并将附加到用户档案数据集。

![](../images/merge-policies/timestamp-review.png)

#### 数据集优先级{#dataset-precedence-review}

如果您选择&#x200B;**[!UICONTROL Dataset precedence]**&#x200B;作为合并策略的合并方法，则用户档案和ExperienceEvent数据集的列表将分别仅包括您在创建工作流程中选择的用户档案和ExperienceEvent数据集。 用户档案数据集的顺序应与您在创建过程中指定的优先级相匹配。 如果没有，请使用[!UICONTROL Back]按钮返回到之前的工作流步骤并调整优先级。

![](../images/merge-policies/dataset-precedence-review.png)

### 更新了合并策略{#updated-list}的列表

完成创建新合并策略的工作流后，您将返回到&#x200B;**[!UICONTROL Merge Policies]**&#x200B;选项卡。 您组织的合并策略列表现在应包括您刚刚创建的合并策略。

![](../images/merge-policies/new-merge-policy-created.png)

## 编辑合并策略

在[!UICONTROL Merge Policies]选项卡中，您可以通过为要编辑的合并策略选择&#x200B;**[!UICONTROL Policy name]**，来修改为[!DNL XDM Individual Profile]类创建的现有合并策略。

![合并策略登陆页](../images/merge-policies/select-edit.png)

当出现&#x200B;**[!UICONTROL Edit merge policy]**&#x200B;屏幕时，您可以更改名称和[!UICONTROL ID stitching]，并更改此策略是否是组织的默认合并策略。

选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续执行合并策略工作流，以更新合并策略中包含的合并方法和数据集。

![](../images/merge-policies/edit-screen.png)

进行必要的更改后，请查看合并策略并选择&#x200B;**[!UICONTROL Finish]**&#x200B;以返回到&#x200B;**[!UICONTROL Merge policies]**&#x200B;选项卡。

>[!WARNING]
>
>更改合并策略可能会影响分段和用户档案结果，因为它会改变解决数据冲突的方式。

![](../images/merge-policies/edit-review.png)

## 违反数据治理政策

创建或更新合并策略时，将执行检查以确定合并策略是否违反了组织定义的任何数据使用策略。 数据使用策略是Adobe Experience Platform [!DNL Data Governance]的一部分，是描述允许或限制您对特定[!DNL Platform]数据执行的营销操作类型的规则。 例如，如果使用合并策略创建已激活到第三方目标的区段，而您的组织拥有阻止将特定数据导出到第三方的数据使用策略，则在尝试保存合并策略时，您将收到&#x200B;**[!UICONTROL Data governance policy violation detected]**&#x200B;通知。

此通知包括已违反的数据使用策略的列表，允许您通过从列表中选择策略来视图违规的详细信息。 选择违反的策略后，**[!UICONTROL Data lineage]**&#x200B;选项卡会提供违规原因和受影响的激活，每个选项卡都会提供更多有关违反数据使用策略的详细信息。

要进一步了解如何在Adobe Experience Platform中执行数据治理，请首先阅读[数据治理概述](../../data-governance/home.md)。

![](../images/merge-policies/policy-violation.png)

## 后续步骤

现在，您已经为您的组织创建和配置了合并策略，您可以使用这些策略来调整平台内客户用户档案的视图，并根据您的用户档案数据创建受众区段。 有关如何使用[!DNL Experience Platform] UI和API创建和使用区段的详细信息，请参阅[分段概述](../../segmentation/home.md)。
