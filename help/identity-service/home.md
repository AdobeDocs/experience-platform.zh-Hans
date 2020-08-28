---
keywords: Experience Platform;home;popular topics;identity;Identity;XDM graphs;identity service;Identity service
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: overview
description: Adobe Experience Platform身份服务通过跨设备和系统连接身份帮助您更好地视图客户及其行为，使您能够实时提供有影响力的个性化数字体验。
translation-type: tm+mt
source-git-commit: 6e4a3ebe84c82790f58f8ec54e6f72c2aca0b7da
workflow-type: tm+mt
source-wordcount: '1711'
ht-degree: 0%

---


# [!DNL Identity Service]概述

提供相关的数字体验需要全面了解客户。 当客户数据在不同的系统中分散，导致每个客户似乎具有多个“身份”时，这就变得更加困难。 Adobe Experience Platform [!DNL Identity Service] 通过跨设备和系统连接身份，帮助您更好地视图客户及其行为，从而实时提供有影响力的个性化数字体验。

## 了解 [!DNL Identity Service]

客户每天都与您的业务互动，与您的品牌建立不断增长的关系。 典型客户可能活跃在组织数据基础架构中任意数量的系统中，如电子商务、忠诚度和服务台系统。 同一客户也可能在任意数量的设备上匿名进行互动。 [!DNL Identity Service] 允许您将客户的完整图片拼凑在一起，从而聚合相关数据，否则这些数据可能会分散在不同的系统中。

以消费者与您品牌关系的日常示例为例：

Mary在您的电子商务网站上有一个帐户，她过去在那里完成了几个订单。 她通常使用个人笔记本电脑购物，每次都登录。 然而，在一次探访中，她用平板电脑购买凉鞋，但没有下订单，也不登录。

此时，玛丽的活动显示为两个单独的用户档案:她的eCommerce登录名和平板电脑设备（可能由设备ID识别）。

玛丽稍后会恢复其平板电脑会话，并在订阅您的新闻稿时提供电子邮件地址。 这样做后，流摄取会在她的用户档案中添加新的身份作为记录数据。 因此，现在 [!DNL Identity Service] Mary的平板电脑设备活动与她的电子商务帐户历史相关。

在她的平板电脑上点击下一下，您的目标内容可以反映玛丽的完整用户档案和历史，而不仅仅是一个未知顾客使用的平板电脑。

定义和维护 [!DNL Identity Service] 的身份关系通过 [!DNL Real-time Customer Profile] 构建客户及其与品牌互动的完整视图而得到利用。 有关详细信息，请参 [阅实时客户用户档案概述](../profile/home.md)。

### 身份

身份是实体（通常是个人）特有的数据。 登录ID、ECID或忠诚度ID等标识称为已知 **标识**。

PII（如电子邮件地址和电话号码）用于直接识别客户。 因此，PII用于跨系统匹配客户的多个身份。

**未知或匿名身份** ，在不识别使用设备的实际人员的情况下，将设备单独列出。 此类别包括访客的IP地址和cookie ID等信息。 虽然可以使用未知身份从设备收集行为数据，但在客户在旅程中提供PII之前，跨设备或介质关联这些身份是有限的。

如下图所示，已知和匿名身份都是身份图的重要组 [成部分](#identity-graphs)，这些组成部分将在本文档稍后讨论。

![平台上的身份拼接](./images/identity-service-stitching.png)

实施 [!DNL Identity Service] 示例包括：

- 电信公司可能依赖“电话号码”值，其中电话号码指线下和线上数据集中的同一个人兴趣。
- 零售公司可能在脱机数据集中使用“电子邮件地址”，在联机数据集中使用ECID，因为匿名访客的百分比很高。
- 银行可能更喜欢离线数据集中的“帐号”，如分行交易。 他们可能依赖在线数据集中的“登录ID”，因为大多数访客在访问时都将通过身份验证。
- 您的客户也可能具有唯一的专有ID，如GUID或其他全局唯一标识符。

### 身份数据

如果你问一个人“你的身份证是什么？” 如果没有更多的背景，他们将很难提供有用的答案。 根据同一逻辑，表示标识值的字符串值（无论是系统生成的ID还是电子邮件地址）只有在与提供字符串值上下文的限定符一起提供时才完成：身份命名空间。

## 身份命名空间和身份图

您的客户可以通过线上和线下渠道的组合与您的品牌进行互动，从而面临如何将这些分散的互动整合为单一客户身份的难题。

[!DNL Experience Platform] 通过两个概念解决此难题： [身份命名空间](#identity-namespaces) 和 [身份图](#identity-graphs)。

以下视频旨在支持您对身份和身份图的理解。 以下视频介绍Identity Collection、Identity Graphs和API的三种功能。 同时介绍了确定性和概率算法如何构造私有身份图，讨论了私有身份图、Adobe Experience Platform身份服务合作图和第三方图的作用。

>[!IMPORTANT]
>
> 概率专用图仍在开发中，并计划在以后发布。

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

### 身份命名空间

当您的客户跨多个渠道与您的品牌进行交互时，如果您无法跨渠道观察和跟踪其活动，就很难理解并为其提供服务。

通过在每个渠道识别客户，跨多种设备和开始了解客户。 Adobe Experience Platform通过使用身份命名空间来实现这一点。
标识命名空间是用于提供数据来源的上下文的标识符，如设备ID或电子邮件ID。 标识命名空间用于查找或链接个人标识，并提供标识值的上下文以防止数据冲突。 例如，ID“123456”可能是指电子商务系统中的一个人，而指服务台系统中的另一个人。 有关详细信息，请参阅 [身份命名空间概述](./namespaces.md)。

### 标识图

标识图是不同标识命名空间之间关系的映射，可直观地展示不同渠道中客户如何与您的品牌互动。

所有客户身份图都可以近乎实时地 [!DNL Identity Service] 进行集体管理和更新，以响应客户活动。

[!DNL Identity Service] 管理仅由您的组织可见的、基于您的数据（称为私有图）构建的标识图。 [!DNL Identity Service] 当所摄取的数据记录包含多个身份时增加您的私人图表，并在找到的身份之间添加关系。

作为提供和标记身份数据时要考虑的潜在因素类型的示例，使用电话号码（如“工作电话”）可能会产生比您在身份图中期望的更多关系。 您可能会发现，许多员工在工作时都使用相同的数字，而“家”和“移动”更能确保关系尽可能精确。

## 向提供身份数据 [!DNL Identity Service]

本节介绍在为每位客户建立身份图之前，如 [!DNL Identity Service] 何处理提供给Adobe Experience Platform的数据。

### 确定身份字段

根据您的企业数据收集策略，您标为身份的数据字段将决定哪些数据将包含在您的身份映射中。 为获得Adobe Experience Platform的最大益处和尽可能最全面的客户身份，您应上传线上和线下数据。

- 在线数据是描述在线状态和行为的数据，如用户名和电子邮件地址。

- 离线数据是指与在线状态不直接相关的数据，如CRM系统的ID。 此类数据使您的身份更加可靠，并支持不同系统之间的数据凝聚力。

### 创建其他身份命名空间

优惠 [!DNL Experience Platform] 各种标准命名空间时，您可能需要创建其他命名空间来正确地对您的身份进行分类。 有关详细信息，请参阅标识 [命名空间概述中有关查看和创](./namespaces.md) 建组织命名空间的部分。

>[!NOTE]
>
>身份命名空间是身份的限定符。 因此，一旦创建了命名空间，就无法删除它。

### 在(XDM)中包 [!DNL Experience Data Model] 含标识数据

作为组织客户数据的 [!DNL Platform] 标准化框架， [!DNL Experience Data Model] (XDM)允许在与之交互的其他服务之间共享和 [!DNL Experience Platform] 理解数据 [!DNL Platform]。 有关详细信息，请参 [阅XDM系统概述](../xdm/home.md)。

记录和时间序列模式都提供了包含身份数据的方法。 在摄取数据时，如果发现来自不同命名空间的数据片段共享公共身份数据，则标识图将在它们之间创建新关系。

### 将XDM字段标记为标识

实现记录 `string` 或时间序列XDM类的模式中任何类型的字段都可以标记为标识字段。 因此，所有引入该字段的数据都将被视为身份数据。

如果标识字段共享通用PII数据，则还允许标识链接。
例如，通过将电话号码字段标记为标识字段， [!DNL Identity Service] 自动绘制与使用相同电话号码的其他个人的关系图。

>[!NOTE]
>
>在标记字段时提供所得身份的命名空间。

### 为 [!DNL Identity Service]

在流摄取过程中，自 [!DNL Identity Service ]动从记录和时间序列数据中提取身份数据。 但是，在摄取数据之前，必须为启用它 [!DNL Identity Service]。 有关详细信 [息，请参阅使用API为实时客户用户档案和身份服务配置数据集](../profile/tutorials/dataset-configuration.md) 教程。

### 将数据收录到 [!DNL Identity Service]

[!DNL Identity Service] 通过批量摄取或流摄 [!DNL Experience Platform] 取，消 [耗发送到](../ingestion/batch-ingestion/overview.md) 的符合 [XDM的数据](../ingestion/streaming-ingestion/overview.md)。

以下视频旨在支持您对Identity Service的理解。 此视频向您展示如何将数据字段标记为身份，摄取身份数据，然后验证数据是否已写入Adobe Experience Platform身份服务专用图。

>[!WARNING]
>
>以 [!DNL Platform] 下视频中显示的UI已过期。 有关最新的UI屏幕截图和功能，请参阅文档。

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## 数据管理

Adobe Experience Platform是以隐私为重而构建的，并包含一个数据治理框架以保护您的客户PII数据。 “电子邮件”或“电话”命名空间下的身份数据默认是加密的，但为了确保在敏感数据被保留之前对其进行加密，数据使用标签可以在数据被摄取或到达时应用到数据 [!DNL Platform]。 有关详细信息，请阅读“数 [据管理”概述](../data-governance/home.md)。

## 后续步骤

现在，您已经了解了其中 [!DNL Identity Service] 的主要概念及 [!DNL Experience Platform]其角色，可以开始学习如何使用[!DNL Identity Service API] [使用您的身份图](./api/getting-started.md)。
