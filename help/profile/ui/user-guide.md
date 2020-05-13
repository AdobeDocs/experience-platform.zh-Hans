---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 实时客户用户档案用户指南
topic: guide
translation-type: tm+mt
source-git-commit: 5718a3930f1e12e62a7bbe60f249c7f6f3434fa7
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 0%

---


# 实时客户用户档案用户指南

实时客户用户档案可以为您的每位客户创建整体视图，将来自多个渠道（包括在线、离线、CRM和第三方数据）的数据相结合。

此文档可作为在Adobe Experience Platform用户界面中与实时客户用户档案交互的指南。

## 入门指南

本用户指南需要了解与管理实时客户用户档案相关的各种Experience Platform服务。 在阅读本用户指南之前，请查阅以下服务的文档：

* [实时客户用户档案](../home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。
* [身份服务](../../identity-service/home.md): 通过将来自不同数据源的身份融入平台，实现实时客户用户档案。
* [体验数据模型(XDM)](../../xdm/home.md): 平台组织客户体验数据的标准化框架。

## 概述

在Experience Platform [UI中](http://platform.adobe.com)，单击左 **侧导** 航 _中的用户档案_ ，以打开“概述”选项卡。 此选项卡提供文档和视频链接，帮助您理解并开始使用用户档案。

![](../images/user-guide/profiles-overview.png)

## 用户档案浏览

单击“ **浏览** ”选项卡，按标识浏览用户档案。 此选项卡还包含您的总 [用户档案数](#profile-count)。

![](../images/user-guide/profiles-browse.png)

### 用户档案计数 {#profile-count}

用户档案数显示组织在组织的默认合并策略将用户档案片段合并到一起以为每个客户组成单个用户档案后，组织在Experience Platform中拥有的用户档案总数。 换言之，您的组织可能有多个与跨不同渠道与您的品牌进行交互的单个客户相关的用户档案片段，但这些片段将合并在一起（根据默认合并策略），并将返回“1”个用户档案计数，因为它们都与同一个人相关。

用户档案计数还包括具有属性（记录数据）的用户档案以及仅包含时间序列(事件)数据的用户档案，如Adobe Analytics用户档案。 用户档案计数会定期刷新，以提供平台内最新的用户档案总数。

当向用户档案存储中引入用户档案会使计数增加或减少5%以上时，将触发一个作业以更新计数。 对于流数据工作流，每小时检查一次以确定是否达到5%的增加或减少阈值。 如果已激活，则会自动触发作业以更新用户档案计数。 对于批量摄取，在成功将批量摄入用户档案存储的15分钟内，如果达到5%增加或减少阈值，则运行作业以更新用户档案计数。

### 身份命名空间

“标 **识命名空间** ”选择器打开一个对话框，您可以从中选择要搜索的标识命名空间，还可以通过选择筛选器图标并选择要添加或删除的属性来自定义搜索中显示的属性。

![](../images/user-guide/profiles-search-filter.png)

从“选 *择身份命名空间* ”对话框中，选择要搜索的命名空间，或使用对话框中的“ **搜索** ”栏开始键入命名空间的名称。 您可以选择命名空间来视图其他详细信息，找到要搜索的命名空间后，可以选择单选按钮并按 **选择** 继续。

![](../images/user-guide/profiles-select-identity-namespace.png)

### 标识值

选择身份 **命名空间**&#x200B;后，您返回“浏 *览* ”选项卡，在该选项卡中可以输 **入身份值**。 此值特定于单个客户用户档案，且必须为提供的命名空间的有效条目。 例如，选择“身 **份命名空间** ”“电子邮件”将 **需要有效电子邮** 件地址形式的“身份”值。

![](../images/user-guide/profiles-show-profile.png)

输入值后，选择“显 **示用户档案** ”，并返回与值匹配的单个用户档案。 选择 **用户档案ID** ,视图用户档案详细信息。

![](../images/user-guide/profiles-display-profile.png)

### 用户档案详细信息

选择用户档案 **ID后**，将打 _开“详细信_ 息”选项卡。 此页显示有关所选用户档案的信息，包括基本属性、链接身份和可用的联系渠道。 显示的用户档案信息已从多个用户档案片段合并到一起，以形成单个客户的单个视图。

![](../images/user-guide/profiles-profile-detail.png)

您可以视图与用户档案相关的附加信息，包括用户档案是其成员的属性、事件和区段。

![](../images/user-guide/profiles-attributes-events-segments.png)

## 合并策略

单击 **合并策略** ，以视图属于您组织的一列表合并策略。 每个列出的策略都显示其名称，无论它是否为默认合并策略，以及它所应用的模式。

有关在UI中使用合并策略的详细信息，请参阅合 [并策略用户指南](merge-policies.md)。

![](../images/user-guide/profiles-merge-policies.png)

## 合并模式

单 **击合并** 模式以视图用户档案商店的合并模式。 合并模式是同一类下所有体验数据模型(XDM)字段的合并，该类模式已被允许用于实时客户用户档案。 单击左侧列表中的类，在画布中视图其合并模式的结构。

例如，选择“XDM用户档案”将显示XDM单个用户档案类的合并模式。

有关合并模式及其在实时用户档案 [中的角色](../../xdm/schema/composition.md) ，请参阅模式构图指南中有关合并模式的部分。

![](../images/user-guide/profiles-union-schema.png)

## 后续步骤

阅读本指南，您现在了解如何使用Experience Platform UI视图和管理用户档案数据。 有关如何利用实时客户用户档案数据生成受众细分的信息，请参 [阅细分文档](../../segmentation/home.md)。