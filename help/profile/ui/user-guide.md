---
keywords: Experience Platform;用户档案；实时客户用户档案；疑难解答；API；统一用户档案；统一用户档案；统一用户档案;模式;rtcp；启用用户档案；启用用户档案;合并合并;用户档案合并;用户档案;
title: 实时客户用户档案UI指南
topic-legacy: guide
description: 实时客户用户档案可以为每位客户创建整体视图，将来自多个渠道（包括在线、离线、CRM和第三方数据）的数据组合在一起。 此文档可作为在Adobe Experience Platform用户界面中与实时客户用户档案交互的指南。
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 1%

---

# [!DNL Real-time Customer Profile] UI指南

[!DNL Real-time Customer Profile] 为每位客户创建全面的视图，将来自多个渠道（包括在线、离线、CRM和第三方数据）的数据组合在一起。此文档用作与Adobe Experience Platform用户界面(UI)中的[!DNL Real-time Customer Profile]数据交互的指南。

## 入门指南

本UI指南要求了解与管理[!DNL Real-time Customer Profiles]相关的各种[!DNL Experience Platform]服务。 在阅读本指南或在UI中工作之前，请查阅以下服务的文档：

* [[!DNL Real-time Customer Profile]](../home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。
* [[!DNL Identity Service]](../../identity-service/home.md):当不同 [!DNL Real-time Customer Profile] 的数据源被引入其中时，通过连接它们的身份来实现这一 [!DNL Platform]点。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):组织客户体验数 [!DNL Platform] 据的标准化框架。

## 概述

在Experience PlatformUI中，选择左侧导航中的&#x200B;**[!UICONTROL Profiles]**&#x200B;以打开&#x200B;**[!UICONTROL Overview]**&#x200B;选项卡。 此选项卡提供文档和视频链接，帮助您理解和开始使用用户档案。

![](../images/user-guide/profiles-overview.png)

### (Alpha)用户档案仪表板

>[!IMPORTANT]
>
>仪表板功能当前位于alpha中，并且并非所有用户都可用。 文档和功能可能会发生变化。

对于某些用户，在左侧导航中选择&#x200B;**[!UICONTROL Profiles]**&#x200B;并打开&#x200B;**[!UICONTROL Overview]**&#x200B;选项卡时会提供一个仪表板，概述与用户档案数据相关的关键量度。

要了解更多信息，请访问[用户档案仪表板指南](profile-dashboard.md)。

## 浏览

选择&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡，按标识浏览用户档案。

![](../images/user-guide/profiles-browse.png)

### 用户档案量度{#profile-metrics}

在&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡的右侧，有几个与用户档案数据相关的重要量度，包括您的总用户档案数[](#profile-count)以及按命名空间](#profiles-by-namespace)列出的[用户档案。

这些用户档案量度是使用您组织的默认合并策略评估的。 有关使用合并策略（包括如何定义默认合并策略）的详细信息，请参阅[合并策略用户指南](merge-policies.md)。

除了这些量度外，用户档案量度部分还提供上次更新的日期和时间，显示上次评估量度的时间。

![](../images/user-guide/profiles-profile-metrics.png)

### 用户档案计数{#profile-count}

用户档案计数显示组织在[!DNL Experience Platform]中的用户档案总数，此时您的组织的默认合并策略已合并到用户档案片段，以便为每个客户组成单个用户档案。 换句话说，您的组织可能有多个用户档案片段与跨不同渠道与您的品牌进行交互的单个客户相关，但这些片段将合并在一起（根据默认合并策略），并将返回“1”个用户档案计数，因为它们都与同一个人相关。

用户档案计数还包括具有属性（记录数据）的用户档案和仅包含时间序列(事件)数据的用户档案，如Adobe Analytics用户档案。 用户档案计数会定期刷新，以提供平台内最新的用户档案总数。

当将记录引入[!DNL Profile]存储中时，将计数增加或减少5%以上，将触发作业以更新计数。 对于流式数据工作流，每小时检查以确定是否达到5%的增加或减少阈值。 如果已触发，则会自动触发作业以更新用户档案计数。 对于批摄取，在成功将批摄入用户档案存储的15分钟内，如果达到5%增加或减少阈值，则运行一个作业以更新用户档案计数。

### 用户档案(按命名空间{#profiles-by-namespace})

**[!UICONTROL Profiles by namespace]**&#x200B;量度显示用户档案商店中所有合并用户档案的命名空间总数和细分。 按命名空间划分的用户档案总数(换句话说，将每个命名空间显示的值加在一起)将始终高于用户档案计数量度，因为一个用户档案可能有多个命名空间与其关联。 例如，如果一个客户在多个渠道上与您的品牌互动，则多个命名空间将与该个别客户关联。

与[用户档案计数](#profile-count)量度类似，当将记录引入到[!DNL Profile]存储中使计数增加或减少5%以上时，触发作业以更新命名空间量度。 对于流式数据工作流，每小时检查以确定是否达到5%的增加或减少阈值。 如果已触发，则会自动触发作业以更新用户档案计数。 对于批摄取，在成功将批摄入[!DNL Profile]存储区的15分钟内，如果达到5%的增加或减少阈值，则运行一个作业以更新量度。

### 合并策略

**[!UICONTROL Merge policy]**&#x200B;选择器将自动选择您组织的默认合并策略。 如果您不希望使用该合并策略，可以选择默认合并策略旁边的`X`以打开&#x200B;**[!UICONTROL Select merge policy]**&#x200B;对话框，在该对话框中可以选择其他合并策略。

要了解有关合并策略及其在平台中的角色的更多信息，请参阅[合并策略UI指南](merge-policies.md)。

![](../images/user-guide/profiles-search-merge-policy.png)

### 身份命名空间

**[!UICONTROL Identity namespace]**&#x200B;选择器会打开一个对话框，您可以在其中选择要搜索的标识命名空间，还可以通过选择过滤器图标并选择要添加或删除的属性来自定义搜索中显示的属性。

![](../images/user-guide/profiles-search-filter.png)

从&#x200B;**[!UICONTROL Select identity namespace]**&#x200B;对话框中，选择要搜索的命名空间，或使用对话框中的搜索栏开始键入命名空间的名称。 您可以选择命名空间来视图其他详细信息，找到要使用的命名空间后，可以选择单选按钮并按&#x200B;**[!UICONTROL Select]**&#x200B;继续。

![](../images/user-guide/profiles-select-identity-namespace.png)

### 标识值

选择标识命名空间后，您返回到&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡，在该选项卡中可以输入&#x200B;**[!UICONTROL Identity value]**。 此值特定于单个客户用户档案，并且必须为提供的命名空间的有效条目。 例如，选择标识命名空间“Email”需要有效电子邮件地址形式的标识值。

![](../images/user-guide/profiles-show-profile.png)

输入值后，选择&#x200B;**[!UICONTROL Show profile]**&#x200B;并返回与值匹配的单个用户档案。 选择&#x200B;**[!UICONTROL Profile ID]**&#x200B;以视图用户档案详细信息。

![](../images/user-guide/profiles-display-profile.png)

### 用户档案详细信息{#profile-detail}

选择&#x200B;**[!UICONTROL Profile ID]**&#x200B;后，将打开&#x200B;**[!UICONTROL Detail]**&#x200B;选项卡。 **[!UICONTROL Detail]**&#x200B;选项卡上显示的用户档案信息已从多个用户档案片段合并到一起，以形成单个客户的视图。 这包括客户详细信息，如基本属性、链接身份和渠道首选项。 在组织级别也可以更改显示的默认字段，以显示首选用户档案属性。 要了解有关自定义这些字段的详细信息，包括有关添加和删除属性以及调整仪表板面板大小的分步说明，请阅读[用户档案详细自定义指南](profile-customization.md)。

![](../images/user-guide/profiles-profile-detail.png)

您可以通过选择其他可用选项卡来视图与单个用户档案相关的其他信息。 这些选项卡包括属性、事件和区段成员关系，它们显示了用户档案当前限定的区段。

![](../images/user-guide/profiles-attributes-events-segments.png)

## 合并策略

从主&#x200B;**[!UICONTROL Profiles]**&#x200B;菜单中，选择&#x200B;**[!UICONTROL Merge Policies]**&#x200B;选项卡，以视图属于您组织的合并策略列表。 每个列出的策略都显示其名称，无论是否为默认合并策略，以及它所应用的模式类。

有关合并策略的详细信息，请参阅[合并策略UI指南](merge-policies.md)。

要了解有关使用实时客户用户档案API处理合并策略的更多信息，请参阅[合并策略终结点指南](../api/merge-policies.md)。

![](../images/user-guide/profiles-merge-policies.png)

## 合并模式{#union-schema}

从主&#x200B;**[!UICONTROL Profiles]**&#x200B;菜单中，选择&#x200B;**[!UICONTROL Union Schema]**&#x200B;选项卡，以视图所摄取数据的可用合并模式。 合并模式是同一类下所有[!DNL Experience Data Model](XDM)字段的合并，该类的模式已被允许在[!DNL Real-time Customer Profile]中使用。

有关合并模式的详细信息，请访问[合并模式UI指南](union-schema.md)。

![](../images/user-guide/profiles-union-schema.png)

## 后续步骤

通过阅读本指南，您现在了解如何使用[!DNL Experience Platform] UI视图和管理[!DNL Profile]数据。 有关如何使用实时用户档案API处理用户档案数据的信息，请参阅[用户档案开发人员指南](../api/overview.md)。
