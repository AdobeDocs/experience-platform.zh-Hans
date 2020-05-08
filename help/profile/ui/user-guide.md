---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 实时客户用户档案用户指南
topic: guide
translation-type: tm+mt
source-git-commit: 667aadde831a1d010f8cbbbb20bd92f914558bd1
workflow-type: tm+mt
source-wordcount: '882'
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

## 用户档案概述

在Experience Platform [UI中](http://platform.adobe.com)，单击左 **侧导航中的** 用户档案 _，以打开用户档案工作区中_ 的“概述 _”选_ 项卡。 此选项卡显示多个构件，它们提供有关用户档案存储的高级信息，包括可寻址受众总数、上周内摄取的用户档案记录数，以及有关同一时间段内成功记录和失败记录的统计信息。

![](../images/user-guide/profile-overview.png)

## 视图用户档案范例

单击 **“浏览** ”以视图可用用户档案的示例列表。 此示例包括您的总用户档案数中最多50 [个用户档案](#profile-count)。 样本通过自动作业进行刷新，该作业在摄取新用户档案数据时拾取新数据。 每个列出的用户档案都显示其ID、名、姓和个人电子邮件。 单击列出的用户档案的ID将在用户档案查看器中显示其详 [细信息](#profile-viewer)。

![](../images/user-guide/profile-samples.png)

您可以通过单击列选择器图标来自定义在列表中显示的属性。 此列表显示包含可添加或删除的常用用户档案属性的下拉列表。

![](../images/user-guide/column-selector.png)

### 用户档案计数 {#profile-count}

用户档案数显示组织在组织的默认合并策略将用户档案片段合并到一起以为每个客户组成单个用户档案后，组织在Experience Platform中拥有的用户档案总数。 换言之，您的组织可能有多个与跨不同渠道与您的品牌进行交互的单个客户相关的用户档案片段，但这些片段将合并在一起（根据默认合并策略），并将返回“1”个用户档案计数，因为它们都与同一个人相关。

用户档案计数还包括具有属性（记录数据）的用户档案以及仅包含时间序列(事件)数据的用户档案，如Adobe Analytics用户档案。 用户档案计数会定期刷新，以提供平台内最新的用户档案总数。

当向用户档案存储中引入用户档案会使计数增加或减少5%以上时，将触发一个作业以更新计数。 对于流数据工作流，每小时检查一次以确定是否达到5%的增加或减少阈值。 如果已激活，则会自动触发作业以更新用户档案计数。 对于批量摄取，在成功将批量摄入用户档案存储的15分钟内，如果达到5%增加或减少阈值，则运行作业以更新用户档案计数。

![](../images/user-guide/profile-count.png)

### 用户档案搜索

如果您知道特定用户档案的链接标识（如其电子邮件地址），则可以单击“查找用户档案” **查找该用户档案**。 这是访问特定用户档案的最可靠方法，而不管它是否出现在示例列表中。

![](../images/user-guide/find-a-profile.png)

在显示的对话框中，从下拉命名空间卡（本例中的“电子邮件”）中选择适当的ID列表，并在下面输入ID值，然后单击“确 **定”**。 如果找到，则目标用户档案的详细信息将显示在用户档案查看器中，如下一节所述。

![](../images/user-guide/find-a-profile-details.png)

### 用户档案查看器 {#profile-viewer}

选择或搜索特定用户档案后，用户档案查 _看器_ 的“详细信息”屏幕将打开。 本页显示有关选定用户档案的信息，如用户档案的基本属性、链接身份和可用的联系渠道。 显示的用户档案信息已从多个用户档案片段合并到一起，以形成单个客户的单个视图。

![](../images/user-guide/profile-viewer-detail.png)

用户档案查看器还提供选项卡，允许您视图与此用户档案关联的事件和段成员关系（如果有）。

![](../images/user-guide/profile-viewer-events-seg.png)

## 合并策略

单击 **合并策略** ，以视图属于您组织的一列表合并策略。 每个列出的策略都显示其名称，无论它是否为默认合并策略，以及它所应用的模式。

![](../images/user-guide/profile-merge-policies.png)

有关在UI中使用合并策略的详细信息，请参阅合 [并策略用户指南](merge-policies.md)。

## 合并模式

单 **击合并** 模式,视图用户档案数据存储的合并模式。 合并模式是同一类下所有体验数据模型(XDM)字段的合并，该类模式已被允许用于实时客户用户档案。 单击左侧列表中的类，在画布中视图其合并模式的结构。

![](../images/user-guide/profile-union-schema.png)

有关合并模式及其在实时用户档案 [中的角色](../../xdm/schema/composition.md) ，请参阅模式构图指南中有关合并模式的部分。

## 后续步骤

阅读本指南，您现在了解如何使用Experience Platform UI视图和管理用户档案数据。 有关如何利用实时客户用户档案数据生成受众细分的信息，请参 [阅细分文档](../../segmentation/home.md)。