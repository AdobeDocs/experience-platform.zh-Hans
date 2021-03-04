---
keywords: Experience Platform；主页；热门主题；身份；身份；XDM图；身份服务；身份服务
solution: Experience Platform
title: Identity Service概述
topic: 概述
description: Adobe Experience Platform Identity Service通过跨设备和系统连接身份，帮您实时提供有影响力的个性化数字体验，从而帮助您更好地视图客户及其行为。
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '1733'
ht-degree: 0%

---


# [!DNL Identity Service]概述

提供相关的数字体验需要全面了解客户。 当客户数据在不同系统之间碎片化，导致每个客户似乎具有多个“身份”时，这就变得更加困难。 Adobe Experience Platform [!DNL Identity Service]通过跨设备和系统连接身份，帮助您获得对客户及其行为的更好视图，从而使您能够实时提供有影响力的个性化数字体验。

## 了解 [!DNL Identity Service]

每天，客户都与您的业务互动，并与您的品牌建立不断增长的关系。 典型客户可能在组织数据基础架构中的任意数量的系统中处于活动状态，例如您的电子商务、忠诚度和服务台系统。 同一客户也可能在任意数量的设备上匿名参与。 [!DNL Identity Service] 使您能够整合客户的完整图景，并聚集相关数据，否则这些数据可能会分散在不同的系统中。

以消费者与您品牌关系的日常示例为例：

Mary在您的电子商务网站上有一个帐户，她过去在那里完成了一些订单。 她通常使用自己的个人笔记本电脑购物，每次都在那里登录。 然而，在一次探访中，她用平板电脑购买凉鞋，但没有下订单，也没有登录。

此时，玛丽的活动显示为两个单独的用户档案:她的eCommerce登录名和平板电脑设备（可能由设备ID识别）。

玛丽稍后会继续其平板电脑会话，并在订阅您的新闻稿时提供电子邮件地址。 这样做后，流摄取会在她的用户档案中添加新的身份作为记录数据。 因此，[!DNL Identity Service]现在将Mary的平板电脑设备活动与她的电子商务帐户历史记录相关联。

在她的平板电脑上点击下一下，您的目标内容可以反映玛丽的完整用户档案和历史，而不仅仅是一个未知顾客使用的平板电脑。

[!DNL Identity Service]定义和维护的身份关系由[!DNL Real-time Customer Profile]利用，以全面了解客户及其与您品牌的互动。 有关详细信息，请参阅[实时客户用户档案概述](../profile/home.md)。

### 身份

身份是实体（通常是个人）特有的数据。 诸如登录ID、ECID或忠诚度ID之类的标识称为已知标识。

PII（如电子邮件地址和电话号码）可直接标识客户。 因此，PII用于跨系统匹配客户的多个身份。

未知或匿名身份将某个设备单独列出，而不识别使用该设备的实际人。 此类别包括诸如访客的IP地址和Cookie ID等信息。 虽然可以使用未知身份从设备收集行为数据，但在客户在旅程中提供PII之前，跨设备或介质关联这些身份是有限的。

如下图所示，已知和匿名身份都是[标识图](#identity-graphs)的重要组件，本文档稍后将讨论。

![平台上的身份拼接](./images/identity-service-stitching.png)

[!DNL Identity Service]实现的示例包括：

- 电信公司可能依赖“电话号码”值，即电话号码是指线下和线上数据集中的同一个人。
- 零售公司可能在脱机数据集中使用“电子邮件地址”，在联机数据集中使用ECID，因为匿名访客占很大比例。
- 银行可能更喜欢离线数据集中的“帐号”，如分行交易。 他们可能依赖在线数据集中的“登录ID”，因为大多数访客在访问时都会通过身份验证。
- 您的客户还可能具有唯一的专有ID，如GUID或其他全局唯一标识符。

### 身份数据

如果你问一个人“你的身份证是什么？” 如果没有进一步的背景，他们很难提供一个有用的答案。 根据同一逻辑，表示标识值的字符串值（无论是系统生成的ID还是电子邮件地址）只有在提供给字符串值上下文的限定符时才完成：身份命名空间。

## 身份命名空间和身份图

您的客户可以通过线上和线下渠道的组合与您的品牌进行互动，从而面临如何将这些分散的互动协调到单个客户身份的难题。

[!DNL Experience Platform] 通过两个概念解决此难题： [身份](#identity-namespaces) 名称和 [身份图](#identity-graphs)。

以下视频旨在支持您对身份和身份图的理解。 以下视频介绍了Identity Collection、Identity Graphs和API的三个功能。 文中还描述了如何使用确定性和概率算法来构造私有标识图，并讨论了私有标识图、Adobe Experience Platform身份服务合作图和第三方图的作用。

>[!IMPORTANT]
>
> 概率专用图仍在开发中，并将在以后发布。

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

### 身份命名空间

当您的客户跨多个渠道与您的品牌互动时，如果您无法跨渠道观察和跟踪其活动，则很难理解和服务客户。

通过在每个渠道中识别客户，跨多种设备和渠道开始了解客户。 Adobe Experience Platform通过使用身份命名空间来实现这一点。
标识命名空间是用于提供数据来源的上下文的标识符，如设备ID或电子邮件ID。 标识命名空间用于查找或链接个人标识，并提供标识值的上下文以防止数据冲突。 例如，ID“123456”可能是指电子商务系统中的一个人，而是指服务台系统中的另一个人。 有关详细信息，请参阅[标识命名空间概述](./namespaces.md)。

### 标识图

身份图是不同身份命名空间之间关系的映射，可直观地展示不同渠道中客户如何与品牌互动。

所有客户标识图由[!DNL Identity Service]以近乎实时的方式集体管理和更新，以响应客户活动。

[!DNL Identity Service] 管理仅由您的组织可见的、基于您的数据（称为专用图）构建的标识图。[!DNL Identity Service] 当收录的数据记录包含多个标识时，添加您的私人图表，并在找到的标识之间添加关系。

例如，在提供和标记身份数据时，要考虑的潜在因素类型，使用电话号码（如“工作电话”）可能会产生比您在身份图中期望的更多关系。 你可能会发现，许多员工在工作中都提及同样的数字，而“家”和“移动”更能确保尽可能精确的关系。

有关详细信息，请参阅有关[访问标识图查看器](./ui/identity-graph-viewer.md)的教程

## 向[!DNL Identity Service]提供身份数据

本节介绍在[!DNL Identity Service]使用前如何处理提供给Adobe Experience Platform的数据，以便为每位客户构建一个标识图。

### 确定身份字段

根据您的企业数据收集策略，您标记为身份的数据字段将决定在您的身份映射中包含哪些数据。 为最大限度地利用Adobe Experience Platform和尽可能最全面的客户身份，您应上传线上和线下数据。

- 在线数据是描述在线状态和行为（如用户名和电子邮件地址）的数据。

- 离线数据是指与在线状态不直接相关的数据，如CRM系统的ID。 此类数据使您的身份更加可靠，并支持不同系统之间的数据凝聚力。

### 创建其他身份命名空间

当[!DNL Experience Platform]优惠各种标准命名空间时，您可能需要创建其他命名空间以正确地对您的身份分类。 有关详细信息，请参阅标识命名空间概述中有关[查看和创建组织的命名空间的部分。](./namespaces.md)

>[!NOTE]
>
>身份命名空间是身份的限定符。 因此，一旦创建了命名空间，便无法删除它。

### 在[!DNL Experience Data Model](XDM)中包含标识数据

作为[!DNL Platform]组织客户数据的标准化框架，[!DNL Experience Data Model](XDM)允许跨[!DNL Experience Platform]和与[!DNL Platform]交互的其他服务共享和理解数据。 有关详细信息，请参阅[XDM系统概述](../xdm/home.md)。

记录和时间序列模式都提供了包含身份数据的方法。 在摄取数据时，如果发现来自不同命名空间的数据片段共享公共标识数据，则标识图将在它们之间创建新关系。

### 将XDM字段标记为标识

在实现记录或时间序列XDM类的模式中类型`string`的任何字段都可以标记为标识字段。 因此，所有引入该字段的数据都将被视为身份数据。

如果身份字段共享通用PII数据，则还允许关联身份。
例如，通过将电话号码字段标记为标识字段，[!DNL Identity Service]会自动绘制与使用相同电话号码的其他个人的关系。

>[!NOTE]
>
>在标记字段时提供所得身份的命名空间。

### 为[!DNL Identity Service]配置数据集

在流摄取过程中，[!DNL Identity Service ]自动从记录和时间序列数据中提取身份数据。 但是，在摄取数据之前，必须为[!DNL Identity Service]启用它。 有关详细信息，请参阅有关使用API](../profile/tutorials/dataset-configuration.md)为实时客户用户档案和身份服务配置数据集的教程。[

### 将数据收录到[!DNL Identity Service]

[!DNL Identity Service] 通过批量摄取或流摄 [!DNL Experience Platform] 取向发 [送](../ingestion/batch-ingestion/overview.md) 符合XDM [的数据](../ingestion/streaming-ingestion/overview.md)。

以下视频旨在支持您对Identity Service的了解。 此视频向您展示如何将数据字段标记为身份，摄取身份数据，然后验证数据是否已将其写入Adobe Experience Platform Identity Service专用图。

>[!WARNING]
>
>以下视频中显示的[!DNL Platform] UI已过期。 有关最新的UI屏幕截图和功能，请参阅文档。

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## 数据治理

Adobe Experience Platform构建时考虑到隐私，并包含一个数据治理框架以保护客户PII数据。 默认情况下，“email”或“phone”命名空间下的身份数据会加密，但为了确保在保留敏感数据之前加密，可以在数据被摄取时或数据到达[!DNL Platform]时对数据应用数据使用标签。 有关详细信息，请阅读[数据治理概述](../data-governance/home.md)。

## 后续步骤

现在，您已经了解了[!DNL Identity Service]的关键概念及其在[!DNL Experience Platform]中的角色，可以开始学习如何使用[[!DNL Identity Service API]](./api/getting-started.md)的身份图。
