---
keywords: Experience Platform；主页；热门主题；身份；XDM图形；身份服务；Identity服务
solution: Experience Platform
title: Identity Service概述
topic-legacy: overview
description: Adobe Experience Platform Identity Service通过跨设备和系统桥接身份，使您能够实时提供有影响的个人数字体验，从而帮助您更好地了解客户及其行为。
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: 288f24351788ed4b8a0c68cffe5eb5c91ed01691
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 0%

---

# [!DNL Identity Service] 概述

提供相关的数字体验需要全面了解您的客户。 当客户数据在不同的系统中分散，导致每个客户似乎都具有多个“身份”时，这会使操作愈发困难。 Adobe Experience Platform [!DNL Identity Service]通过跨设备和系统桥接身份，使您能够实时提供有影响的个人数字体验，从而帮助您更好地了解客户及其行为。

## 了解 [!DNL Identity Service]

客户每天都与您的业务互动，并与您的品牌建立持续不断的关系。 典型客户可能在贵组织数据基础架构中的任意数量的系统中处于活动状态，例如您的电子商务、忠诚度和服务台系统。 同一客户也可以在任意数量的设备上匿名接触。 [!DNL Identity Service] 允许您整合客户的完整图片，聚合相关数据，否则这些数据可能会分散到不同的系统中。

以消费者与您的品牌关系的日常示例为例：

Mary在您的电子商务网站上有一个帐户，她过去在该网站上完成了一些订单。 她通常使用自己的个人笔记本电脑进行购物，每次都会登录。 但是，在她的一次访问中，她使用平板电脑购买凉鞋，但没有下订单，也没有登录。

此时，Mary的活动将显示为两个单独的用户档案：她的电子商务登录和平板电脑设备（可能由设备ID识别）。

Mary稍后恢复平板电脑会话，并在订阅您的新闻稿时提供其电子邮件地址。 在执行此操作后，流摄取会添加新身份作为其配置文件中的记录数据。 因此，[!DNL Identity Service]现在会将Mary的平板电脑设备活动与其电子商务帐户历史记录相关联。

在下次点击她的平板电脑时，您的目标内容可能会反映Mary的完整资料和历史，而不是只反映未知购物者使用的平板电脑。

[!DNL Identity Service]定义和维护的身份关系由[!DNL Real-time Customer Profile]利用来构建客户及其与您品牌的交互的完整图片。 有关更多信息，请参阅[实时客户资料概述](../profile/home.md)。

### 标识

身份是实体（通常是个人）特有的数据。 登录ID、ECID或忠诚度ID等身份称为已知身份。

PII（如电子邮件地址和电话号码）用于直接识别客户。 因此，PII用于跨系统匹配客户的多个身份。

未知或匿名身份会在设备上单独显示一个设备，而不会识别使用该设备的实际人员。 此类别包括访客的IP地址和Cookie ID等信息。 虽然可以使用未知身份从设备收集行为数据，但在客户在其历程中提供PII之前，将这些身份跨设备或介质关联是有限的。

如下图所示，已知和匿名身份都是[标识图](#identity-graphs)的重要组件，本文档后面将讨论这些组件。

![Platform上的身份拼合](./images/identity-service-stitching.png)

[!DNL Identity Service]实施的示例包括：

- 电信公司可能依赖“电话号码”值，其中电话号码是指线下和线上数据集中的同一关注个人。
- 由于匿名访客的高百分比，零售公司可能会在离线数据集中使用“电子邮件地址”，并在在线数据集中使用ECID。
- 银行可能倾向于在离线数据集中使用“帐号”，例如分行交易。 它们可能依赖于在线数据集中的“登录ID”，因为大多数访客在访问期间都将进行身份验证。
- 您的客户还可能具有唯一的专有ID，如GUID或其他通用唯一标识符。

### 身份数据

如果你问某人“你的ID是什么？” 如果没有进一步的背景，他们将很难提供有用的答案。 按照相同的逻辑，表示标识值的字符串值（无论是系统生成的ID还是电子邮件地址）只有在提供给字符串值上下文的限定符时才能完成：身份命名空间。

## 身份命名空间和身份图

您的客户可能会通过线上和线下渠道的组合与您的品牌进行交互，这就给如何将这些分散的交互协调到单个客户身份带来了挑战。

[!DNL Experience Platform] 通过两个概念解决此难题： [身份](#identity-namespaces) 名称和 [身份图](#identity-graphs)。

以下视频旨在支持您对身份和身份图形的了解。 以下视频介绍了身份收集、身份图和API的三项功能。 文中还介绍了确定性和概率性算法如何用于构建专用身份图，并讨论了专用身份图、Adobe Experience Platform身份服务协作图和第三方图的作用。

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

### 身份命名空间

当您的客户跨多个渠道（包括Web、移动应用程序、呼叫中心或店面）与您的品牌进行交互时，如果您无法跨渠道观察和跟踪客户的活动，则很难了解并为其提供服务。

通过识别每个渠道中的客户，开始跨多个设备和渠道了解客户。 Adobe Experience Platform使用身份命名空间来实现此目的。
标识命名空间是用于提供数据源自的上下文的标识符，例如设备ID或电子邮件ID。 身份命名空间用于查找或链接个人身份，并提供身份值的上下文以防止数据冲突。 例如，ID“123456”可能是指您的电子商务系统中的一个人员，而指您的帮助台系统中的其他人员。 有关更多信息，请参阅[标识命名空间概述](./namespaces.md)。

### 身份图

身份图是不同身份命名空间之间关系的映射，可直观地表示客户如何跨不同渠道与您的品牌进行交互。

所有客户身份图表都由[!DNL Identity Service]以近乎实时的方式集体管理和更新，以响应客户活动。

[!DNL Identity Service] 管理仅由您的组织查看并基于您的数据构建的标识图（称为专用图）。[!DNL Identity Service] 当已摄取的数据记录包含多个身份时，通过在找到的身份之间添加关系来增强您的专用图。

作为提供和标记身份数据时需要考虑的潜在因素类型的示例，使用电话号码（如“工作电话”）可能会产生比您在身份图中预期的更多关系。 您可能会发现，许多员工在工作中引用的号码是相同的，“家”和“移动”更好地有助于保持尽可能精确的关系。

有关更多信息，请参阅有关[访问标识图查看器](./ui/identity-graph-viewer.md)的教程

## 向[!DNL Identity Service]提供身份数据

本节介绍在[!DNL Identity Service]为每位客户构建身份图之前，如何处理提供给Adobe Experience Platform的数据。

### 确定身份字段

根据您的企业数据收集策略，您标记为身份的数据字段将决定哪些数据包含在您的身份映射中。 为了最大限度地利用Adobe Experience Platform以及尽可能全面的客户身份，您应当上传在线和离线数据。

- 在线数据是描述在线状态和行为（如用户名和电子邮件地址）的数据。

- 离线数据是指与在线存在无直接关系的数据，例如来自CRM系统的ID。 此类数据可让您的身份更加强健，并支持跨不同系统的数据凝聚力。

### 创建其他身份命名空间

虽然[!DNL Experience Platform]提供多种标准命名空间，但您可能需要创建其他命名空间以对您的身份正确分类。 有关更多信息，请参阅身份命名空间概述中关于[查看和创建组织](./namespaces.md)的命名空间的部分。

>[!NOTE]
>
>身份命名空间是身份的限定符。 因此，在创建命名空间后，将无法删除该命名空间。

### 在[!DNL Experience Data Model](XDM)中包含身份数据

作为[!DNL Platform]组织客户数据的标准化框架，[!DNL Experience Data Model](XDM)允许在与[!DNL Platform]交互的[!DNL Experience Platform]和其他服务之间共享和理解数据。 有关详细信息，请参阅[XDM系统概述](../xdm/home.md)。

记录架构和时序架构都提供了包含身份数据的方法。 在摄取数据时，如果发现来自不同命名空间的数据片段共享通用身份数据，则该身份图将在它们之间创建新关系。

### 将XDM字段标记为标识

架构中实现记录或时间序列XDM类的任何类型为`string`的字段都可以标记为标识字段。 因此，摄取到该字段的所有数据都将被视为身份数据。

>[!NOTE]
>
>数组和映射类型字段不受支持，无法标记和标记为标识字段。

如果标识字段共享通用PII数据，则还允许关联标识。
例如，[!DNL Identity Service]通过将电话号码字段标记为身份字段，自动绘制与使用相同电话号码的其他个人的关系的图表。

>[!NOTE]
>
>在标记字段时，将提供所生成标识的命名空间。

### 为[!DNL Identity Service]配置数据集

在流式摄取过程中，[!DNL Identity Service ]会自动从记录数据和时间序列数据中提取身份数据。 但是，在摄取数据之前，必须为[!DNL Identity Service]启用该功能。 有关更多信息，请参阅有关[使用API为实时客户配置文件和Identity服务配置数据集的教程](../profile/tutorials/dataset-configuration.md) 。

### 将数据摄取到[!DNL Identity Service]

[!DNL Identity Service] 使用通过批量摄取或流 [!DNL Experience Platform] 式摄取 [发送](../ingestion/batch-ingestion/overview.md) 到的符 [合XDM的数据](../ingestion/streaming-ingestion/overview.md)。

以下视频旨在支持您对Identity Service的了解。 此视频向您展示了如何为数据字段设置标签以作为标识，引入标识数据，然后验证该数据是否已发送到Adobe Experience Platform Identity Service专用图。

>[!WARNING]
>
>以下视频中显示的[!DNL Platform] UI已过期。 有关最新的UI屏幕截图和功能，请参阅相关文档。

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## 数据管理

Adobe Experience Platform构建时考虑了隐私，并包含一个数据管理框架来保护客户PII数据。 默认情况下，“email”或“phone”命名空间下的身份数据会加密，但为确保在保留敏感数据之前对其进行加密，在摄取数据时或在数据到达[!DNL Platform]后，可以对数据应用数据使用标签。 有关更多信息，请阅读[数据管理概述](../data-governance/home.md)。

## 后续步骤

现在，您已经了解了[!DNL Identity Service]的关键概念及其在[!DNL Experience Platform]中的角色，接下来可以开始了解如何使用[[!DNL Identity Service API]](./api/getting-started.md)来使用身份图。
