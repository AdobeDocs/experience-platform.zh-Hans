---
keywords: Experience Platform；配置文件；实时客户配置文件；故障诊断；API；统一配置文件；统一配置文件；配置文件；rtcp；启用配置文件；启用配置文件；联合架构；联合配置文件；联合配置文件
title: Real-time Customer Profile UI指南
topic-legacy: guide
description: 实时客户资料可整合来自多个渠道的数据（包括在线、离线、CRM和第三方数据），从而创建每个客户的整体视图。 本文档是在Adobe Experience Platform用户界面中与实时客户资料进行交互的指南。
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: 2791c32abe582d51d05d4bf0488ba82dfadfd053
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] UI指南

[!DNL Real-time Customer Profile] 通过整合来自多个渠道（包括在线、离线、CRM和第三方数据）的数据，创建每个客户的整体视图。本文档是与Adobe Experience Platform用户界面(UI)中的[!DNL Real-time Customer Profile]数据交互的指南。

## 快速入门

本UI指南要求您了解管理[!DNL Real-time Customer Profiles]涉及的各种[!DNL Experience Platform]服务。 在阅读本指南或在UI中工作之前，请查阅以下服务的文档：

* [[!DNL Real-time Customer Profile]](../home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。
* [[!DNL Identity Service]](../../identity-service/home.md):通过在 [!DNL Real-time Customer Profile] 将不同数据源摄取到时桥接其身份，从而实现了 [!DNL Platform]这一点。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):用于组织客户体验数 [!DNL Platform] 据的标准化框架。

## 概述

在Experience PlatformUI中，选择左侧导航中的&#x200B;**[!UICONTROL Profiles]**&#x200B;以打开显示[!UICONTROL Profiles]功能板的&#x200B;**[!UICONTROL Overview]**&#x200B;选项卡。

>[!NOTE]
>
>如果贵组织是Platform的新用户，但尚未创建活动的配置文件数据集或合并策略，则[!UICONTROL Profiles]功能板将不可见。 相反， [!UICONTROL 概述]选项卡会显示可帮助您开始使用实时客户资料的链接和文档。

###  用户档案仪表板  {#profile-dashboard}

**[!UICONTROL Profiles]**&#x200B;功能板概述了与贵组织的Profile数据相关的关键量度。

要了解更多信息，请访问[配置文件仪表板指南](../../dashboards/guides/profiles.md)。

![](../../dashboards/images/profiles/dashboard-overview.png)

## 浏览

选择&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡，以按身份浏览用户档案。

![](../images/user-guide/profiles-browse.png)

### 配置文件量度{#profile-metrics}

在&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡的右侧，有几个与配置文件数据相关的重要量度，包括配置文件总数[](#profile-count)以及按命名空间](#profiles-by-namespace)列出的[配置文件。

这些配置文件量度将使用您组织的默认合并策略进行评估。 有关使用合并策略（包括如何定义默认合并策略）的更多信息，请参阅[合并策略概述](../merge-policies/overview.md)。

除了这些量度之外，配置文件量度部分还提供了上次更新的日期和时间，以显示上次评估量度的时间。

![](../images/user-guide/profiles-profile-metrics.png)

### 配置文件计数{#profile-count}

配置文件计数显示在组织的默认合并策略将配置文件片段合并到一起以为每个单独的客户形成单个配置文件后，您的组织在[!DNL Experience Platform]中拥有的配置文件总数。 换言之，贵组织可能有多个配置文件片段与跨不同渠道与您的品牌进行交互的单个客户相关，但这些片段将合并在一起（根据默认合并策略），并将返回“1”个配置文件计数，因为它们都与同一个人相关。

用户档案计数还包含具有属性（记录数据）的用户档案，以及仅包含时间系列（事件）数据的用户档案，如Adobe Analytics用户档案。 系统会定期刷新用户档案计数，以提供Platform中最新的用户档案总数。

当将记录摄取到[!DNL Profile]存储中时，计数增加或减少5%以上时，将触发一个作业来更新计数。 对于流数据工作流，每小时进行一次检查，以确定是否满足5%的增加或减少阈值。 如果已执行，则会自动触发作业以更新用户档案计数。 对于批量摄取，在将批次成功摄取到用户档案存储的15分钟内，如果满足5%的增加或减少阈值，则会运行一个作业以更新用户档案计数。

### 按命名空间{#profiles-by-namespace}的配置文件

**[!UICONTROL 按命名空间划分的配置文件]**&#x200B;量度显示配置文件存储区中所有合并配置文件中命名空间的总计数和划分。 按命名空间划分的配置文件总数（即，将每个命名空间显示的值相加）将始终高于配置文件计数量度，因为一个配置文件可能具有与其关联的多个命名空间。 例如，如果客户在多个渠道上与您的品牌交互，则多个命名空间将与该个别客户关联。

与[配置文件计数](#profile-count)量度类似，当将记录摄取到[!DNL Profile]存储中时，计数增加或减少5%以上时，将触发一个作业以更新命名空间量度。 对于流数据工作流，每小时进行一次检查，以确定是否满足5%的增加或减少阈值。 如果已执行，则会自动触发作业以更新用户档案计数。 对于批量摄取，在成功将批摄取到[!DNL Profile]存储的15分钟内，如果满足5%的增加或减少阈值，则运行作业以更新量度。

### 合并策略

**[!UICONTROL 合并策略]**&#x200B;选择器会自动为您的组织选择默认的合并策略。 如果您不希望使用该合并策略，则可以选择默认合并策略旁边的`X`以打开&#x200B;**[!UICONTROL 选择合并策略]**&#x200B;对话框，您可以在该对话框中选择其他合并策略。

要详细了解合并策略及其在Platform中的角色，请参阅[合并策略概述](../merge-policies/overview.md)。

![](../images/user-guide/profiles-search-merge-policy.png)

### 身份命名空间

**[!UICONTROL 身份命名空间]**&#x200B;选择器会打开一个对话框，您可以在该对话框中选择要搜索的身份命名空间，并且可以通过选择过滤器图标并选择要添加或删除的属性来自定义在搜索中显示的属性。

![](../images/user-guide/profiles-search-filter.png)

从&#x200B;**[!UICONTROL 选择标识命名空间]**&#x200B;对话框中，选择要搜索的命名空间，或使用对话框中的搜索栏开始键入命名空间的名称。 您可以选择一个命名空间来查看其他详细信息，找到要使用的命名空间后，可以选择单选按钮，然后按&#x200B;**[!UICONTROL Select]**&#x200B;以继续。

![](../images/user-guide/profiles-select-identity-namespace.png)

### 标识值

选择身份命名空间后，返回到&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡，您可以在该选项卡中输入&#x200B;**[!UICONTROL 标识值]**。 此值特定于单个客户配置文件，并且必须是提供的命名空间的有效条目。 例如，选择身份命名空间“Email”将需要有效电子邮件地址形式的身份值。

![](../images/user-guide/profiles-show-profile.png)

输入值后，选择&#x200B;**[!UICONTROL 显示配置文件]** ，并返回与该值匹配的单个配置文件。 选择&#x200B;**[!UICONTROL 配置文件ID]**&#x200B;以查看配置文件详细信息。

![](../images/user-guide/profiles-display-profile.png)

### 配置文件详细信息{#profile-detail}

选择&#x200B;**[!UICONTROL 配置文件ID]**&#x200B;后，将打开&#x200B;**[!UICONTROL 详细信息]**&#x200B;选项卡。 **[!UICONTROL Detail]**&#x200B;选项卡中显示的配置文件信息已从多个配置文件片段合并到一起，以形成单个客户的单个视图。 这包括客户详细信息，如基本属性、链接的身份和渠道首选项。 显示的默认字段也可以在组织级别更改，以显示首选的用户档案属性。 要了解有关自定义这些字段的更多信息，包括关于添加和删除属性以及调整功能板大小的分步说明，请阅读[配置文件详细信息自定义指南](profile-customization.md)。

![](../images/user-guide/profiles-profile-detail.png)

您可以通过选择其他可用选项卡来查看与单个配置文件相关的其他信息。 这些选项卡包括属性、事件和区段成员资格，它们显示配置文件当前符合条件的区段。

![](../images/user-guide/profiles-attributes-events-segments.png)

## 合并策略

从主&#x200B;**[!UICONTROL 配置文件]**&#x200B;菜单中，选择&#x200B;**[!UICONTROL 合并策略]**&#x200B;选项卡，以查看属于贵组织的合并策略列表。 列出的每个策略都会显示其名称（无论是否是默认合并策略）以及它所应用的架构类。

有关合并策略的更多信息，请参阅[合并策略概述](../merge-policies/overview.md)。

![](../images/user-guide/profiles-merge-policies.png)

## 并集架构{#union-schema}

从主&#x200B;**[!UICONTROL Profiles]**&#x200B;菜单中，选择&#x200B;**[!UICONTROL 合并架构]**&#x200B;选项卡，以查看所摄取数据的可用合并架构。 并集架构是同一类下所有[!DNL Experience Data Model](XDM)字段的合并，该类的架构已启用以供在[!DNL Real-time Customer Profile]中使用。

有关并集架构的更多信息，请访问[并集架构UI指南](union-schema.md)。

![](../images/user-guide/profiles-union-schema.png)

## 后续步骤

通过阅读本指南，您现在知道如何使用[!DNL Experience Platform] UI查看和管理[!DNL Profile]数据。 有关如何使用实时客户配置文件API处理配置文件数据的信息，请参阅[配置文件开发人员指南](../api/overview.md)。
