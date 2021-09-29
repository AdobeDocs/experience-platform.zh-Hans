---
keywords: Experience Platform；主页；热门主题；身份；XDM图形；身份服务；Identity服务
solution: Experience Platform
title: Identity Service概述
topic-legacy: overview
description: Adobe Experience Platform Identity Service通过跨设备和系统桥接身份，使您能够实时提供有影响的个人数字体验，从而帮助您更好地了解客户及其行为。
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: 5373b8fcd84cee749a85bdb755a23eb7292cf352
workflow-type: tm+mt
source-wordcount: '1792'
ht-degree: 0%

---

# [!DNL Identity Service] 概述

提供相关的数字体验需要全面了解您的客户。 当客户数据在不同的系统中分散，导致每个客户似乎都具有多个“身份”时，这会使操作愈发困难。

Adobe Experience Platform Identity Service通过跨设备和系统桥接身份，使您能够实时提供有影响的个人数字体验，从而全面了解客户及其行为。

使用[!DNL Identity Service]，您可以：

- 确保客户通过每次互动获得一致、个性化且相关的体验。
- 将来自不同来源的多个不同身份拼合在一起，并全面了解您的客户。
- 利用身份图映射不同的身份命名空间，以直观的方式展示客户如何跨不同渠道与您的品牌进行交互。

## 快速入门

在深入研究[!DNL Identity Service]的详细信息之前，以下是关键术语的简要摘要：

| 搜索词 | 定义 |
| --- | --- |
| 身份 | 身份是实体（通常是个人）特有的数据。 身份（如登录ID、ECID或忠诚度ID）也称为“已知身份”。 |
| ECID | Experience CloudID(ECID)是跨Experience Platform和Adobe Experience Cloud应用程序使用的共享身份命名空间。 ECID为客户身份提供了基础，可用作设备的主ID，用作身份图的基节点。 有关更多信息，请参阅[ECID概述](./ecid.md) 。 |
| 身份命名空间 | 身份命名空间用于区分身份的上下文或类型。 例如，标识将“name<span>@email.com”区分为电子邮件地址或“443522”区分为数字CRM ID。 身份命名空间用于查找个人身份并提供身份值的上下文。 这允许您确定两个[!DNL Profile]片段（包含不同的主ID，但共享`email`标识命名空间的相同值）实际上是同一个片段。 有关更多信息，请参阅[标识命名空间概述](./namespaces.md)。 |
| 身份图 | 身份图是不同身份之间关系的映射，使您能够可视化并更好地了解哪些客户身份被拼合在一起，以及如何拼合。 有关更多信息，请参阅关于[使用身份图查看器](./ui/identity-graph-viewer.md)的教程。 |
| 个人身份信息(PII) | PII是可以直接识别客户的信息，如电子邮件地址或电话号码。 PII值通常用于匹配。 客户在不同系统中的多个身份。 |
| 未知或匿名身份 | 未知或匿名身份是指在不识别使用设备的实际人员的情况下隔离设备的指示器。 未知和匿名身份包括访客的IP地址和Cookie ID等信息。 尽管未知和匿名身份可以提供行为数据，但在客户提供其PII之前，这些身份数据会受到限制。 |

## 什么是 [!DNL Identity Service]？

客户每天都与您的业务互动，并与您的品牌建立持续不断的关系。 典型客户可能在贵组织数据基础架构中的任意数量的系统中处于活动状态，例如您的电子商务、忠诚度和服务台系统。 同一客户也可以在任意数量的设备上匿名接触。 [!DNL Identity Service] 允许您整合客户的完整图片，聚合相关数据，否则这些数据可能会分散到不同的系统中。

以消费者与您的品牌关系的日常示例为例：

- Mary在您的电子商务网站上有一个帐户，她过去在该帐户中完成了一些订单。 她通常使用自己的个人笔记本电脑进行购物，每次都会登录。 但是，在她的一次访问中，她使用平板电脑购买凉鞋，但没有下订单，也没有登录。
- 此时，Mary的活动将显示为两个单独的用户档案：
   - 她的电子商务登录
   - 她的平板电脑设备，可能由设备ID识别
- Mary稍后恢复平板电脑会话，并在订阅您的新闻稿时提供其电子邮件地址。 在执行此操作后，流摄取会添加新身份作为其配置文件中的记录数据。 因此，[!DNL Identity Service]现在会将Mary的平板电脑设备活动与其电子商务帐户历史记录相关联。
- 在下次点击她的平板电脑时，您的目标内容可能会反映Mary的完整资料和历史，而不是只反映未知购物者使用的平板电脑。

![Platform上的身份拼合](./images/identity-service-stitching.png)

基本上，[!DNL Identity Service]允许您将客户的完整图片拼合在一起，聚合可能分散在不同系统中的相关数据。 [!DNL Identity Service]定义和维护的身份关系通过实时客户资料进行利用，以构建客户及其与您品牌的交互的完整图片。 有关更多信息，请参阅[实时客户资料概述](../profile/home.md)。

### 用例

[!DNL Identity Service]实施的示例包括：

- 电信公司可能依赖“电话号码”值，其中电话号码是指线下和线上数据集中的同一关注个人。
- 由于匿名访客的高百分比，零售公司可能会在离线数据集中使用“电子邮件地址”，并在在线数据集中使用ECID。
- 银行可能倾向于在离线数据集中使用“帐号”，例如分行交易。 它们可能依赖于在线数据集中的“登录ID”，因为大多数访客在访问期间都将进行身份验证。
- 您的客户还可能具有唯一的专有ID，如GUID或其他通用唯一标识符。

## 身份命名空间

如果你问某人“你的ID是什么？” 如果没有进一步的背景，他们将很难提供有用的答案。 按照相同的逻辑，表示标识值的字符串值（无论是系统生成的ID还是电子邮件地址）只有在提供给字符串值上下文的限定符时才能完成：身份命名空间。


您的客户可能会通过线上和线下渠道的组合与您的品牌进行交互，这就给如何将这些分散的交互协调到单个客户身份带来了挑战。

通过识别每个渠道中的客户，开始跨多个设备和渠道了解客户。 Platform使用身份命名空间来实现此目的。 标识命名空间是用于为客户标识提供其他上下文的标识符，例如电子邮件或电话。 身份命名空间用于查找或链接个人身份，并提供身份值的上下文。 有关更多信息，请参阅[标识命名空间概述](./namespaces.md)。

## 身份图

身份图是不同身份命名空间之间关系的映射，允许您可视化并更好地了解哪些客户身份拼合在一起，以及如何拼合。 有关更多信息，请参阅关于[使用身份图查看器](./ui/identity-graph-viewer.md)的教程。

以下视频旨在支持您对身份和身份图形的了解。 它涵盖身份收集、身份图和API的三项功能。 文中还描述了确定性和概率性算法如何用于构建专用身份图，并讨论了它们与第三方图和Adobe Experience Platform身份服务协作图的作用。

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## 向[!DNL Identity Service]提供身份数据

本节介绍在[!DNL Identity Service]为每位客户构建身份图之前，如何处理提供给Adobe Experience Platform的数据。

### 确定身份字段

根据您的企业数据收集策略，您标记为身份的数据字段将决定哪些数据包含在您的身份映射中。 为了最大限度地利用Adobe Experience Platform以及尽可能全面的客户身份，您应当上传在线和离线数据。

- 在线数据是描述在线状态和行为（如用户名和电子邮件地址）的数据。

- 离线数据是指与在线存在无直接关系的数据，例如来自CRM系统的ID。 此类数据可让您的身份更加强健，并支持跨不同系统的数据凝聚力。

### 创建其他身份命名空间

虽然Experience Platform提供了多种标准命名空间，但您可能需要创建其他命名空间以对您的身份正确分类。 有关更多信息，请参阅身份命名空间概述中关于[查看和创建组织](./namespaces.md)的命名空间的部分。

>[!NOTE]
>
>身份命名空间是身份的限定符。 因此，在创建命名空间后，将无法删除该命名空间。

### 在[!DNL Experience Data Model](XDM)中包含身份数据

作为[!DNL Platform]组织客户数据的标准化框架，[!DNL Experience Data Model](XDM)允许在与[!DNL Platform]交互的Experience Platform和其他服务之间共享和理解数据。 有关详细信息，请参阅[XDM系统概述](../xdm/home.md)。

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

[!DNL Identity Service] 通过批量摄取或流式摄取，使用发 [送到](../ingestion/batch-ingestion/overview.md) Experience Platform的 [符合XDM的数据](../ingestion/streaming-ingestion/overview.md)。

以下视频旨在支持您对Identity Service的了解。 此视频向您展示了如何为数据字段设置标签以作为标识，引入标识数据，然后验证该数据是否已发送到Adobe Experience Platform Identity Service专用图。

>[!WARNING]
>
>以下视频中显示的[!DNL Platform] UI已过期。 有关最新的UI屏幕截图和功能，请参阅相关文档。

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## 数据管理

Adobe Experience Platform构建时考虑了隐私，并包含一个数据管理框架来保护客户PII数据。 默认情况下，“email”或“phone”命名空间下的身份数据会加密，但为确保在保留敏感数据之前对其进行加密，在摄取数据时或在数据到达[!DNL Platform]后，可以对数据应用数据使用标签。 有关更多信息，请阅读[数据管理概述](../data-governance/home.md)。

## 后续步骤

现在，您已了解[!DNL Identity Service]的关键概念及其在Experience Platform中的角色，接下来便可以开始了解如何使用[[!DNL Identity Service API]](./api/getting-started.md)使用身份图。
