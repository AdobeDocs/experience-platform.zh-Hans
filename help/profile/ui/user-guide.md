---
keywords: Experience Platform；配置文件；实时客户配置文件；故障诊断；API；统一配置文件；统一配置文件；配置文件；rtcp；启用配置文件；启用配置文件；联合架构；联合配置文件；联合配置文件
title: Real-Time Customer Profile UI指南
description: 实时客户资料可整合来自多个渠道的数据（包括在线、离线、CRM和第三方数据），从而全面了解您的每位客户。 本文档是在Adobe Experience Platform用户界面中与实时客户资料进行交互的指南。
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1951'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] UI指南

[!DNL Real-Time Customer Profile] 通过整合来自多个渠道（包括在线、离线、CRM和第三方数据）的数据，创建每个客户的整体视图。 本文档是与交互的指南 [!DNL Real-Time Customer Profile] Adobe Experience Platform用户界面(UI)中的数据。

## 快速入门

此UI指南需要了解 [!DNL Experience Platform] 管理涉及的服务 [!DNL Real-Time Customer Profiles]. 在阅读本指南或在UI中工作之前，请查阅以下服务的文档：

* [[!DNL Real-Time Customer Profile] 概述](../home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
* [[!DNL Identity Service]](../../identity-service/home.md):启用 [!DNL Real-Time Customer Profile] 通过在引入时桥接来自不同数据源的身份 [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):标准化框架， [!DNL Platform] 组织客户体验数据。

## [!UICONTROL 概述]

在Experience PlatformUI中，选择 **[!UICONTROL 用户档案]** 在左侧导航中打开 **[!UICONTROL 概述]** 选项卡，其中显示了用户档案功能板。

>[!NOTE]
>
>如果贵组织是Platform的新用户，并且尚未创建活动的配置文件数据集或合并策略，则 [!UICONTROL 用户档案] 功能板不可见。 相反， [!UICONTROL 概述] 选项卡会显示可帮助您开始使用实时客户配置文件的链接和文档。

### 用户档案仪表板 {#profile-dashboard}

配置文件功能板概述了与贵组织的配置文件数据相关的关键量度。

要了解更多信息，请访问 [配置文件仪表板指南](../../dashboards/guides/profiles.md).

![随即会显示“配置文件”功能板。](../../dashboards/images/profiles/dashboard-overview.png)

## [!UICONTROL 浏览] 选项卡量度

选择 **[!UICONTROL 浏览]** 选项卡，以显示与贵组织的配置文件数据相关的多个量度。 您还可以使用此选项卡使用合并策略或标识浏览配置文件存储，如本指南下一节中所述。

在的右侧 **[!UICONTROL 浏览]** 选项卡 [配置文件计数](#profile-count) 以及 [按命名空间划分的配置文件](#profiles-by-namespace).

>[!NOTE]
>
>这些配置文件量度可能与 [配置文件仪表板](#profile-dashboard) 因为它们是使用您组织的默认合并策略评估的。 有关使用合并策略（包括如何定义默认合并策略）的更多信息，请参阅 [合并策略概述](../merge-policies/overview.md).

除了这些量度之外，此部分还提供上次更新的日期和时间，以显示上次评估量度的时间。

![此时会显示并突出显示配置文件量度。](../images/user-guide/browse-metrics.png)

### 用户档案计数 {#profile-count}

配置文件计数可显示贵组织在Experience Platform内拥有的配置文件总数，当贵组织的默认合并策略已合并到配置文件片段以为每个单独的客户形成单个配置文件后。 换言之，贵组织可能有多个配置文件片段与跨不同渠道与您的品牌进行交互的单个客户相关，但这些片段将合并在一起（根据默认合并策略），并将返回“1”个配置文件计数，因为它们都与同一个人相关。

用户档案计数还包含具有属性（记录数据）的用户档案，以及仅包含时间系列（事件）数据的用户档案，如Adobe Analytics用户档案。 系统会定期刷新用户档案计数，以提供Platform中最新的用户档案总数。

#### 更新用户档案计数量度

将记录摄取到 [!DNL Profile] 存储会增加或减少计数5%以上，则会触发作业以更新计数。 对于流数据工作流，每小时进行一次检查，以确定是否满足5%的增加或减少阈值。 如果已执行，则会自动触发作业以更新用户档案计数。 对于批量摄取，在将批次成功摄取到用户档案存储的15分钟内，如果满足5%的增加或减少阈值，则会运行一个作业以更新用户档案计数。

### [!UICONTROL 按命名空间划分的配置文件] {#profiles-by-namespace}

的 **[!UICONTROL 按命名空间划分的配置文件]** 量度显示配置文件存储区中所有合并配置文件中命名空间的总数和划分。 按命名空间划分的配置文件总数（即，将每个命名空间显示的值相加）将始终高于配置文件计数量度，因为一个配置文件可能具有与其关联的多个命名空间。 例如，如果客户在多个渠道上与您的品牌进行交互，则多个命名空间将与该个别客户关联。

#### 更新 [!UICONTROL 按命名空间划分的配置文件] 量度

与 [配置文件计数](#profile-count) 量度，将记录摄取到 [!DNL Profile] 存储会增加或减少计数5%以上，则会触发作业以更新命名空间量度。 对于流数据工作流，每小时进行一次检查，以确定是否满足5%的增加或减少阈值。 如果已执行，则会自动触发作业以更新用户档案计数。 对于批量摄取，在成功将批摄取到 [!DNL Profile] 存储，如果满足5%的增加或减少阈值，则运行作业以更新量度。

## 使用 [!UICONTROL 浏览] 选项卡以查看用户档案

在 **[!UICONTROL 浏览]** 选项卡，您可以使用合并策略查看示例配置文件，或使用身份命名空间和值查找特定配置文件。

![此时会显示属于组织的用户档案。](../images/user-guide/none-selected.png)

### 浏览者 [!UICONTROL 合并策略]

的 **[!UICONTROL 浏览]** 选项卡默认设置为组织的默认合并策略。 要选择其他合并策略，请选择 `X` ，然后使用选择器打开 **[!UICONTROL 选择合并策略]** 对话框。

>[!NOTE]
>
>如果未选择合并策略，请使用 **[!UICONTROL 合并策略]** 字段以打开选择对话框。

![合并策略选择器会突出显示。](../images/user-guide/browse-by-merge-policy.png)

从 **[!UICONTROL 选择合并策略]** 对话框中，选择策略名称旁边的单选按钮，然后使用 **[!UICONTROL 选择]** 返回 [!UICONTROL 浏览] 选项卡。 然后，您可以选择 **[!UICONTROL 查看]** 刷新示例用户档案，并查看应用了新合并策略的用户档案采样。

![此时将显示一个对话框，您可以在其中选择要筛选的合并策略。](../images/user-guide/select-merge-policy.png)

显示的用户档案表示在应用所选合并策略后，您组织的用户档案存储中最多有20个用户档案的样例。 将新数据添加到贵组织的配置文件存储区后，将刷新选定合并策略的示例配置文件。

要查看其中一个示例用户档案的详细信息，请选择 **[!UICONTROL 配置文件ID]**. 有关更多信息，请参阅本指南后面部分的 [查看配置文件详细信息](#profile-detail).

![将显示与合并策略匹配的示例用户档案。](../images/user-guide/sample-profiles.png)

要进一步了解合并策略及其在Platform中的角色，请参阅 [合并策略概述](../merge-policies/overview.md).

### 浏览者 [!UICONTROL 身份] {#browse-identity}

在 **[!UICONTROL 浏览]** 选项卡中，您可以使用标识命名空间来按标识值查找特定的配置文件。 按身份浏览需要您提供合并策略、身份命名空间和身份值。

![合并策略选择器会突出显示。](../images/user-guide/browse-by-merge-policy.png)

如有必要，请使用 **[!UICONTROL 合并策略]** 用于打开的选择器 **[!UICONTROL 选择合并策略]** 对话框，然后选择要使用的合并策略。

![此时将显示一个对话框，您可以在其中选择要筛选的合并策略。](../images/user-guide/select-merge-policy.png)

然后，使用 **[!UICONTROL 身份命名空间]** 用于打开的选择器 **[!UICONTROL 选择身份命名空间]** 对话框，然后选择要搜索的命名空间。 如果贵组织具有多个命名空间，则可以使用对话框中的搜索栏开始键入命名空间的名称。

您可以选择命名空间以查看其他详细信息，或选择单选按钮以选择命名空间。 然后，您可以使用 **[!UICONTROL 选择]** 继续。

![此时将显示一个对话框，您可以在其中选择要筛选的身份命名空间。](../images/user-guide/select-identity-namespace.png)

选择 [!UICONTROL 身份命名空间] 然后回到 [!UICONTROL 浏览] 选项卡，您可以输入 **[!UICONTROL 标识值]** 与您选择的命名空间相关。

>[!NOTE]
>
>此值特定于单个客户配置文件，并且必须是提供的命名空间的有效条目。 例如，选择身份命名空间“Email”将需要有效电子邮件地址形式的身份值。

![要过滤的标识值会突出显示。](../images/user-guide/filter-identity-value.png)

输入值后，选择 **[!UICONTROL 查看]** 并返回与值匹配的单个用户档案。 选择 **[!UICONTROL 配置文件ID]** 查看配置文件详细信息。

![与标识值匹配的配置文件会突出显示。](../images/user-guide/filtered-identity-value.png)

## 查看配置文件详细信息 {#profile-detail}

选择 **[!UICONTROL 配置文件ID]**, **[!UICONTROL 详细信息]** 选项卡。 在 **[!UICONTROL 详细信息]** 选项卡已从多个配置文件片段合并到一起，以形成单个客户的单个视图。 这包括客户详细信息，如基本属性、链接的身份和渠道首选项。

显示的默认字段也可以在组织级别更改，以显示首选的用户档案属性。 要了解有关自定义这些字段的更多信息，包括有关添加和删除属性以及调整功能板面板大小的分步说明，请阅读 [配置文件详细自定义指南](profile-customization.md).

![“详细信息”(Details)选项卡突出显示。 此时会显示配置文件详细信息。](../images/user-guide/profile-detail.png)

您可以通过选择其他可用选项卡，查看与单个客户用户档案相关的其他信息。 这些选项卡包括属性、事件和区段成员资格选项卡，用于显示配置文件当前符合条件的区段。

### “属性”选项卡

的 **[!UICONTROL 属性]** 选项卡提供了一个列表视图，其中汇总了在应用指定的合并策略后与单个配置文件相关的所有属性。

通过选择 **[!UICONTROL 查看JSON]**. 对于希望更好地了解如何将配置文件属性摄取到平台的任何用户而言，此功能非常有用。

![“属性”选项卡会突出显示。 此时会显示配置文件属性。](../images/user-guide/attributes.png)

### “事件”选项卡

的 **[!UICONTROL 事件]** 选项卡包含与客户关联的100个最新ExperienceEvent中的数据。 此数据可能包括电子邮件打开次数、购物车活动和页面查看次数。 选择 **[!UICONTROL 查看全部]** 对于任何单个事件，都会提供作为事件一部分的附加字段和值捕获。

通过选择 **[!UICONTROL 查看JSON]**. 这有助于了解如何在平台中捕获事件。

![“事件”选项卡会突出显示。 将显示用户档案事件。](../images/user-guide/events.png)

### “区段成员资格”选项卡

的 **[!UICONTROL 区段成员资格]** 选项卡会显示一个列表，其中包含单个客户配置文件当前所属的区段的名称和描述。 当配置文件符合区段条件或过期时，此列表会自动更新。 用户档案当前符合条件的区段总数会显示在选项卡的右侧。

有关Experience Platform中分段的更多信息，请参阅 [AdobeExperience Platform分段服务文档](../../segmentation/home.md).

![区段成员资格选项卡会突出显示。 此时会显示配置文件区段成员资格详细信息。](../images/user-guide/segment-membership.png)

## 合并策略

从主 **[!UICONTROL 用户档案]** 菜单，选择 **[!UICONTROL 合并策略]** 选项卡，查看属于贵组织的合并策略列表。 列出的每个策略都会显示其名称（无论是否是默认合并策略）以及它所应用的架构类。

有关合并策略的更多信息，请参阅 [合并策略概述](../merge-policies/overview.md).

![“合并策略”选项卡会突出显示。 将显示属于组织的合并策略。](../images/user-guide/merge-policies.png)

## 并集模式 {#union-schema}

从主 **[!UICONTROL 用户档案]** 菜单，选择 **[!UICONTROL 并集架构]** 选项卡，以查看所摄取数据的可用合并架构。 联盟模式是所有 [!DNL Experience Data Model] (XDM)同一类下的字段，其架构已启用以供在中使用 [!DNL Real-Time Customer Profile].

有关合并模式的更多信息，请访问 [并集架构UI指南](union-schema.md).

![“并集架构”选项卡突出显示。 将显示属于组织的并集架构。](../images/user-guide/union-schema.png)

## 后续步骤

通过阅读本指南，您了解如何使用Experience PlatformUI查看和管理组织的用户档案数据。 有关如何使用Experience PlatformAPI处理用户档案数据的信息，请参阅 [实时客户资料API指南](../api/overview.md).
