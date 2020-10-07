---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;unified profile;Unified Profile;unified;Profile;rtcp;enable profile;Enable profile;Union schema;UNION PROFILE;union profile
title: 实时客户用户档案用户指南
topic: guide
description: 实时客户用户档案可以为您的每位客户创建整体视图，将来自多个渠道（包括在线、离线、CRM和第三方数据）的数据相结合。 此文档可作为与Adobe Experience Platform用户界面中实时用户档案交互的指南。
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1292'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] 用户指南

[!DNL Real-time Customer Profile] 为每位客户创建全面视图，将来自多个渠道（包括在线、离线、CRM和第三方数据）的数据相结合。

此文档用作在Adobe Experience Platform用户界 [!DNL Real-time Customer Profile] 面中与数据交互的指南。

## 入门指南

本用户指南需要了解与管理相关 [!DNL Experience Platform] 的各种服务 [!DNL Real-time Customer Profiles]。 在阅读本用户指南之前，请查阅以下服务的文档：

* [[!DNL实时客户用户档案]](../home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
* [[!DNL标识服务]](../../identity-service/home.md):当 [!DNL Real-time Customer Profile] 不同数据源被引入时，通过连接它们的身份实现 [!DNL Platform]。
* [[!DNL Experience Data Model] (XDM)](../../xdm/home.md):组织客户体验数 [!DNL Platform] 据的标准化框架。

## 概述

在UI [[!DNL Experience Platform] 中](http://platform.adobe.com)，在左 **[!UICONTROL 侧导航]** 中选 **[!UICONTROL 择用户档案以打开]** 概述选项卡。 此选项卡提供文档和视频链接，帮助您理解并开始使用用户档案。

![](../images/user-guide/profiles-overview.png)

## 浏览

选择“ **[!UICONTROL 浏览]** ”选项卡，按标识浏览用户档案。

![](../images/user-guide/profiles-browse.png)

### 用户档案指标 {#profile-metrics}

在“浏览”选项卡的右侧 **[!UICONTROL 是与用户档案]** 相关的几个重要指标，包括您的总 [用户档案数](#profile-count) ，以及按命名空间 [列出用户档案](#profiles-by-namespace)。

这些用户档案量度是使用单位的默认合并策略评估的。 有关使用合并策略（包括如何定义默认合并策略）的详细信息，请参阅合 [并策略用户指南](merge-policies.md)。

除了这些指标外，用户档案指标部分还提供上次更新的日期和时间，显示上次评估指标的时间。

![](../images/user-guide/profiles-profile-metrics.png)

### 用户档案计数 {#profile-count}

用户档案计数显示组织在组织的默认合并策略 [!DNL Experience Platform]将用户档案片段合并到一起后，组织拥有的用户档案总数，以便为每个单独的客户组成一个用户档案。 换言之，您的组织可能有多个与跨不同渠道与您的品牌进行交互的单个客户相关的用户档案片段，但这些片段将合并在一起（根据默认合并策略），并将返回“1”个用户档案计数，因为它们都与同一个人相关。

用户档案计数还包括具有属性（记录数据）的用户档案以及仅包含时间序列(事件)数据的用户档案，如Adobe Analytics用户档案。 用户档案计数会定期刷新，以提供平台内最新的用户档案总数。

当将记录引入存储 [!DNL Profile] 区时，将计数增加或减少5%以上时，将触发作业以更新计数。 对于流数据工作流，每小时检查一次以确定是否达到5%的增加或减少阈值。 如果已激活，则会自动触发作业以更新用户档案计数。 对于批量摄取，在成功将批量摄入用户档案存储的15分钟内，如果达到5%增加或减少阈值，则运行作业以更新用户档案计数。

### 用户档案，按命名空间 {#profiles-by-namespace}

按 **[!UICONTROL 命名空间量度的用户档案]** ，显示您的用户档案商店中所有合并用户档案中命名空间的总计数和细分。 按命名空间划分的用户档案总数(换言之，将每个命名空间显示的值相加)将始终高于用户档案计数量度，因为一个用户档案可能有多个命名空间与其关联。 例如，如果客户在多个渠道上与您的品牌互动，则多个命名空间将与该个别客户关联。

与用户档案计 [数度量](#profile-count) 相似，当将记录引入存储 [!DNL Profile] 中会增加或减少计数超过5%时，将触发作业以更新命名空间度量。 对于流数据工作流，每小时检查一次以确定是否达到5%的增加或减少阈值。 如果已激活，则会自动触发作业以更新用户档案计数。 对于批处理摄取，在成功将批处理摄入存储的 [!DNL Profile] 15分钟内，如果达到5%的增加或减少阈值，则运行作业以更新度量。

### 合并策略

合并 **[!UICONTROL 策略选择器]** 会自动为您的组织选择默认的合并策略。 如果不想使用该合并策略，可以选择默认合 `X` 并策略旁边的，以打开“选择合并策略 **[!UICONTROL ”对话框]** ，在该对话框中可以选择其他合并策略。 要进一步了解合并策略及其在平台中的角色，请参阅合 [并策略用户指南](merge-policies.md)。

![](../images/user-guide/profiles-search-merge-policy.png)

### 身份命名空间

“标 **[!UICONTROL 识命名空间]** ”选择器打开一个对话框，您可以从中选择要搜索的标识命名空间，还可以通过选择筛选器图标并选择要添加或删除的属性来自定义搜索中显示的属性。

![](../images/user-guide/profiles-search-filter.png)

从“选 **[!UICONTROL 择身份命名空间]** ”对话框中，选择要搜索的命名空间，或使用对话框中的搜索栏开始键入命名空间的名称。 您可以选择命名空间来视图其他详细信息，找到要使用的命名空间后，可以选择单选按钮并按 **[!UICONTROL 选择]** 以继续。

![](../images/user-guide/profiles-select-identity-namespace.png)

### 标识值

选择身份命名空间后，您返回“浏 **[!UICONTROL 览]** ”选项卡，在该选项卡中可以 **[!UICONTROL 输入身份值]**。 此值特定于单个客户用户档案，且必须为提供的命名空间的有效条目。 例如，选择标识命名空间“电子邮件”将需要有效电子邮件地址形式的标识值。

![](../images/user-guide/profiles-show-profile.png)

输入值后，选择“显 **[!UICONTROL 示用户档案]** ”，并返回与值匹配的单个用户档案。 选择 **[!UICONTROL 用户档案ID]** ,视图用户档案详细信息。

![](../images/user-guide/profiles-display-profile.png)

### 用户档案详细信息 {#profile-detail}

选择用户档案 **[!UICONTROL ID后]**，将打 **[!UICONTROL 开“详细信]** 息”选项卡。 “详细信息”标签上显 **[!UICONTROL 示的用户档案]** 信息已从多个用户档案片段合并到一起，以形成单个客户的单个视图。 这包括客户详细信息，如基本属性、链接身份和渠道首选项。 显示的默认字段也可以在组织级别进行更改，以显示首选用户档案属性。 要进一步了解如何自定义这些字段，包括有关添加和删除属性以及调整仪表板面板大小的分步说明，请阅读 [用户档案详细信息自定义指南](profile-customization.md)。

![](../images/user-guide/profiles-profile-detail.png)

您可以通过选择其他可用选项卡来视图与单个用户档案相关的其他信息。 这些选项卡包括属性、事件和区段成员关系，这些选项卡显示了用户档案当前符合条件的区段。

![](../images/user-guide/profiles-attributes-events-segments.png)

## 合并策略

从主用户档案 **[!UICONTROL 菜单]** ，选择合 **[!UICONTROL 并策略选]** 项卡以视图属于您组织的合并策略列表。 每个列出的策略都显示其名称，无论它是否为默认合并策略，以及它所应用的模式。

有关合并策略的详细信息，请参 [阅合并策略用户指南](merge-policies.md)。

![](../images/user-guide/profiles-merge-policies.png)

## 合并模式 {#union-schema}

从主用户档案 **[!UICONTROL 菜单]** ，选择 **[!UICONTROL 合并]** 模式选项卡，以视图用户档案数据的合并模式。 合并模式是同一类下的所 [!DNL Experience Data Model] 有(XDM)字段的合并，该类的模式已被允许在中使用 [!DNL Real-time Customer Profile]。 通过从左侧的“[!UICONTROL Class]”列表中选择类，您可以在画布中视图其模式的结构。 例如，选择“[!DNL XDM Profile]”将显示类的合并 [!DNL XDM Individual Profile] 模式。

有关合并模式及其在Adobe Experience Platform的作用的详细信息，请参阅模式构图指南中有关合并模式 [的章节](../../xdm/schema/composition.md)。

![](../images/user-guide/profiles-union-schema.png)

## 后续步骤

通过阅读本指南，您现在了解如何使用UI视图 [!DNL Profile] 和管理 [!DNL Experience Platform] 数据。 有关如何使用实时用户档案API处理用户档案数据的信息，请参阅用户档案开发人 [员指南](../api/overview.md)。