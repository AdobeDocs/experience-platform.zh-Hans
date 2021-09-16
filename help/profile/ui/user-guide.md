---
keywords: Experience Platform；配置文件；实时客户配置文件；故障诊断；API；统一配置文件；统一配置文件；配置文件；rtcp；启用配置文件；启用配置文件；联合架构；联合配置文件；联合配置文件
title: Real-time Customer Profile UI指南
topic-legacy: guide
description: 实时客户资料可整合来自多个渠道的数据（包括在线、离线、CRM和第三方数据），从而创建每个客户的整体视图。 本文档是在Adobe Experience Platform用户界面中与实时客户资料进行交互的指南。
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: b5e6376b54fe8b53fbabf85a2909293cebd93ccc
workflow-type: tm+mt
source-wordcount: '1568'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] UI指南

[!DNL Real-time Customer Profile] 通过整合来自多个渠道（包括在线、离线、CRM和第三方数据）的数据，创建每个客户的整体视图。本文档是与Adobe Experience Platform用户界面(UI)中的[!DNL Real-time Customer Profile]数据交互的指南。

## 快速入门

本UI指南要求您了解管理[!DNL Real-time Customer Profiles]涉及的各种[!DNL Experience Platform]服务。 在阅读本指南或在UI中工作之前，请查阅以下服务的文档：

* [[!DNL Real-time Customer Profile] 概述](../home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
* [[!DNL Identity Service]](../../identity-service/home.md):通过在 [!DNL Real-time Customer Profile] 将不同数据源摄取到时桥接其身份，从而实现了 [!DNL Platform]这一点。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):用于组织客户体验数 [!DNL Platform] 据的标准化框架。

## [!UICONTROL 概述]

在Experience PlatformUI中，选择左侧导航中的&#x200B;**[!UICONTROL Profiles]** ，以打开显示配置文件仪表板的&#x200B;**[!UICONTROL Overview]**&#x200B;选项卡。

>[!NOTE]
>
>如果贵组织是Platform的新用户，但尚未创建活动的配置文件数据集或合并策略，则[!UICONTROL Profiles]功能板将不可见。 相反， [!UICONTROL 概述]选项卡会显示可帮助您开始使用实时客户资料的链接和文档。

### 用户档案仪表板 {#profile-dashboard}

配置文件功能板概述了与贵组织的配置文件数据相关的关键量度。

要了解更多信息，请访问[配置文件仪表板指南](../../dashboards/guides/profiles.md)。

![](../../dashboards/images/profiles/dashboard-overview.png)

##  Browsetab量度

选择&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡以显示与贵组织的配置文件数据相关的多个量度。 您还可以使用此选项卡使用合并策略或标识浏览配置文件存储，如本指南下一节中所述。

在&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡的右侧是[配置文件计数](#profile-count)以及按命名空间](#profiles-by-namespace)列出的[配置文件。

>[!NOTE]
>
>这些配置文件量度可能与[配置文件功能板](#profile-dashboard)上显示的量度有所不同，因为它们是使用您组织的默认合并策略评估的。 有关使用合并策略（包括如何定义默认合并策略）的更多信息，请参阅[合并策略概述](../merge-policies/overview.md)。

除了这些量度之外，此部分还提供上次更新的日期和时间，以显示上次评估量度的时间。

![](../images/user-guide/profiles-browse-metrics.png)

### 用户档案计数 {#profile-count}

配置文件计数可显示贵组织在Experience Platform内拥有的配置文件总数，当贵组织的默认合并策略已合并到配置文件片段以为每个单独的客户形成单个配置文件后。 换言之，贵组织可能有多个配置文件片段与跨不同渠道与您的品牌进行交互的单个客户相关，但这些片段将合并在一起（根据默认合并策略），并将返回“1”个配置文件计数，因为它们都与同一个人相关。

用户档案计数还包含具有属性（记录数据）的用户档案，以及仅包含时间系列（事件）数据的用户档案，如Adobe Analytics用户档案。 系统会定期刷新用户档案计数，以提供Platform中最新的用户档案总数。

#### 更新用户档案计数量度

当将记录摄取到[!DNL Profile]存储中时，计数增加或减少5%以上时，将触发一个作业来更新计数。 对于流数据工作流，每小时进行一次检查，以确定是否满足5%的增加或减少阈值。 如果已执行，则会自动触发作业以更新用户档案计数。 对于批量摄取，在将批次成功摄取到用户档案存储的15分钟内，如果满足5%的增加或减少阈值，则会运行一个作业以更新用户档案计数。

### [!UICONTROL 按命名空间划分的配置文件] {#profiles-by-namespace}

**[!UICONTROL 按命名空间划分的配置文件]**&#x200B;量度显示配置文件存储区中所有合并配置文件中命名空间的总计数和划分。 按命名空间划分的配置文件总数（即，将每个命名空间显示的值相加）将始终高于配置文件计数量度，因为一个配置文件可能具有与其关联的多个命名空间。 例如，如果客户在多个渠道上与您的品牌交互，则多个命名空间将与该个别客户关联。

#### 按命名空间]更新配置文件[!UICONTROL 

与[配置文件计数](#profile-count)量度类似，当将记录摄取到[!DNL Profile]存储中时，计数增加或减少5%以上时，将触发一个作业以更新命名空间量度。 对于流数据工作流，每小时进行一次检查，以确定是否满足5%的增加或减少阈值。 如果已执行，则会自动触发作业以更新用户档案计数。 对于批量摄取，在成功将批摄取到[!DNL Profile]存储的15分钟内，如果满足5%的增加或减少阈值，则运行作业以更新量度。

## 使用[!UICONTROL Browse]选项卡查看配置文件

在&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡上，您可以使用合并策略查看示例配置文件，或使用身份命名空间和值查找特定配置文件。

![](../images/user-guide/browse-by-none-selected.png)

### 按[!UICONTROL 合并策略]浏览

默认情况下， **[!UICONTROL Browse]**&#x200B;选项卡将设置为贵组织的默认合并策略。 要选择其他合并策略，请选择合并策略名称旁边的`X`，然后使用选择器打开&#x200B;**[!UICONTROL 选择合并策略]**&#x200B;对话框。

>[!NOTE]
>
>如果未选择合并策略，请使用&#x200B;**[!UICONTROL Merge policy]**&#x200B;字段旁边的选择器按钮打开选择对话框。

![](../images/user-guide/browse-by-merge-policy.png)

要从&#x200B;**[!UICONTROL 选择合并策略]**&#x200B;对话框中选择合并策略，请选择策略名称旁边的单选按钮，然后使用&#x200B;**[!UICONTROL 选择]**&#x200B;返回到[!UICONTROL 浏览]选项卡。 然后，您可以选择&#x200B;**[!UICONTROL View]**&#x200B;以刷新示例配置文件，并查看应用了新合并策略的配置文件采样。

![](../images/user-guide/select-merge-policy-dialog.png)

显示的用户档案表示在应用所选合并策略后，您组织的用户档案存储中最多有20个用户档案的样例。 将新数据添加到贵组织的配置文件存储区后，将刷新选定合并策略的示例配置文件。

要查看其中一个示例配置文件的详细信息，请选择&#x200B;**[!UICONTROL 配置文件ID]**。 有关详细信息，请参阅本指南后面关于[查看配置文件详细信息](#profile-detail)的部分。

![](../images/user-guide/sample-profiles.png)

要详细了解合并策略及其在Platform中的角色，请参阅[合并策略概述](../merge-policies/overview.md)。


### 按[!UICONTROL Identity]浏览

在&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡上，您可以使用身份命名空间来按身份值查找特定配置文件。 按身份浏览需要您提供合并策略、身份命名空间和身份值。

![](../images/user-guide/browse-by-identity.png)

如有必要，请使用&#x200B;**[!UICONTROL 合并策略]**&#x200B;选择器打开&#x200B;**[!UICONTROL 选择合并策略]**&#x200B;对话框，然后选择要使用的合并策略。

![](../images/user-guide/select-merge-policy-dialog.png)

然后，使用&#x200B;**[!UICONTROL 标识命名空间]**&#x200B;选择器打开&#x200B;**[!UICONTROL 选择标识命名空间]**&#x200B;对话框，并选择要搜索的命名空间。 如果贵组织具有多个命名空间，则可以使用对话框中的搜索栏开始键入命名空间的名称。

您可以选择命名空间以查看其他详细信息，也可以选择单选按钮以选择命名空间。 然后，可以使用&#x200B;**[!UICONTROL Select]**&#x200B;继续。

![](../images/user-guide/profiles-select-identity-namespace.png)

选择[!UICONTROL 标识命名空间]并返回到[!UICONTROL Browse]选项卡后，可以输入与您选择的命名空间相关的&#x200B;**[!UICONTROL 标识值]**。

>[!NOTE]
>
>此值特定于单个客户配置文件，并且必须是提供的命名空间的有效条目。 例如，选择身份命名空间“Email”将需要有效电子邮件地址形式的身份值。

![](../images/user-guide/browse-by-identity-values.png)

输入值后，选择&#x200B;**[!UICONTROL 查看]**，并返回与该值匹配的单个配置文件。 选择&#x200B;**[!UICONTROL 配置文件ID]**&#x200B;以查看配置文件详细信息。

![](../images/user-guide/browse-by-identity-profile.png)

## 查看配置文件详细信息 {#profile-detail}

选择&#x200B;**[!UICONTROL 配置文件ID]**&#x200B;后，将打开&#x200B;**[!UICONTROL 详细信息]**&#x200B;选项卡。 **[!UICONTROL Detail]**&#x200B;选项卡中显示的配置文件信息已从多个配置文件片段合并到一起，以形成单个客户的单个视图。 这包括客户详细信息，如基本属性、链接的身份和渠道首选项。

显示的默认字段也可以在组织级别更改，以显示首选的用户档案属性。 要了解有关自定义这些字段的更多信息，包括关于添加和删除属性以及调整功能板大小的分步说明，请阅读[配置文件详细信息自定义指南](profile-customization.md)。

![](../images/user-guide/profiles-profile-detail.png)

您可以通过选择其他可用选项卡来查看与单个配置文件相关的其他信息。 这些选项卡包括属性、事件和区段成员资格选项卡，用于显示配置文件当前符合条件的区段。

![](../images/user-guide/profiles-attributes-events-segments.png)

## 合并策略

从主&#x200B;**[!UICONTROL 配置文件]**&#x200B;菜单中，选择&#x200B;**[!UICONTROL 合并策略]**&#x200B;选项卡，以查看属于贵组织的合并策略列表。 列出的每个策略都会显示其名称（无论是否是默认合并策略）以及它所应用的架构类。

有关合并策略的更多信息，请参阅[合并策略概述](../merge-policies/overview.md)。

![](../images/user-guide/profiles-merge-policies.png)

## 并集模式 {#union-schema}

从主&#x200B;**[!UICONTROL Profiles]**&#x200B;菜单中，选择&#x200B;**[!UICONTROL 合并架构]**&#x200B;选项卡，以查看所摄取数据的可用合并架构。 并集架构是同一类下所有[!DNL Experience Data Model](XDM)字段的合并，该类的架构已启用以供在[!DNL Real-time Customer Profile]中使用。

有关并集架构的更多信息，请访问[并集架构UI指南](union-schema.md)。

![](../images/user-guide/profiles-union-schema.png)

## 后续步骤

通过阅读本指南，您了解如何使用Experience PlatformUI查看和管理组织的用户档案数据。 有关如何使用Experience PlatformAPI处理用户档案数据的信息，请参阅[实时客户档案API指南](../api/overview.md)。
