---
keywords: Experience Platform；主页；热门主题；身份；XDM图形；身份服务；身份服务
solution: Experience Platform
title: Identity服务概述
description: Adobe Experience Platform Identity Service通过跨设备和系统桥接身份，允许您实时提供有影响力的个人数字体验，从而帮助您更好地了解客户及其行为。
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: ad9fb0bcc7bca55da432c72adc94d49e3c63ad6e
workflow-type: tm+mt
source-wordcount: '1839'
ht-degree: 10%

---

# [!DNL Identity Service] 概述

提供相关的数字体验要求完全了解您的客户。 当您的客户数据分散在不同的系统中，导致每个客户似乎拥有多个“身份”时，就会更加困难。

Adobe Experience Platform 身份服务通过跨设备和系统桥接身份，使您能够全面了解您的客户及其行为，助您实时提供有影响力的个人数字体验。

替换为 [!DNL Identity Service]，您可以：

- 确保您的客户通过每次互动获得一致、个性化的相关体验。
- 将来自不同来源的多个不同身份拼接在一起，并创建客户的全面视图。
- 利用身份图来映射不同的身份命名空间，从而为您提供客户如何跨不同渠道与您的品牌交互的可视表示形式。

## 快速入门

在深入了解 [!DNL Identity Service]，下面是关键术语的简短摘要：

| 搜索词 | 定义 |
| --- | --- |
| 标识 | 身份是指实体（通常是个人）的独特数据。登录ID、ECID或忠诚度ID等身份也称为“已知身份”。 |
| ECID | Experience CloudID (ECID)是跨Experience Platform和Adobe Experience Cloud应用程序使用的共享身份命名空间。 ECID为客户身份奠定了基础，用作设备的主ID以及身份图的基本节点。 请参阅 [ECID概述](./ecid.md) 以了解更多信息。 |
| 标识命名空间 | 标识命名空间用于区分标识的上下文或类型。例如，标识将“name<span>@email.com”识别为电子邮件地址，将“443522”识别为数字 CRM ID。身份命名空间用于查找单个身份并提供身份值的上下文。 这允许您确定 [!DNL Profile] 包含不同主ID，但共享相同值的片段 `email` 身份命名空间，实际上是同一个人。 请参阅 [身份命名空间概述](./namespaces.md) 以了解更多信息。 |
| 身份图 | 身份图是不同身份之间关系的映射，允许您可视化并更好地了解哪些客户身份是如何拼合在一起的，以及如何拼合的。 请参阅上的教程 [使用身份图查看器](./ui/identity-graph-viewer.md) 以了解更多信息。 |
| 个人身份信息(PII) | PII是可以直接识别客户的信息，如电子邮件地址或电话号码。 PII值通常用于匹配。 客户跨不同系统的多个身份。 |
| 未知或匿名身份 | 未知或匿名身份指示器可隔离设备，而无需识别使用该设备的实际人员。 未知和匿名身份包括访客的IP地址和Cookie ID等信息。 尽管未知和匿名身份可以提供行为数据，但在客户提供其PII之前，它们有限。 |

## 什么是 [!DNL Identity Service]？

每一天，客户都会与您的业务互动，并与您的品牌建立持续增长的关系。 典型客户可能活跃在您组织数据基础架构内的任意数量的系统中，例如电子商务、忠诚度和帮助台系统。 同一客户还可以在任意数量的设备上匿名参与。 [!DNL Identity Service] 允许您拼合客户的完整情况，汇总可能跨不同系统孤立的相关数据。

以消费者与品牌关系的日常例子为例：

- Mary在您的电子商务网站上有一个帐户，她过去曾在该帐户上完成过几笔订单。 她通常用自己的笔记本电脑购物，每次都登录这里。 但是，在访问期间，她使用平板电脑购买凉鞋，但没有下订单，也没有登录。
- 此时，Mary的活动显示为两个单独的用户档案：
   - 她的电子商务登录信息
   - 她的平板电脑设备，可能通过设备ID识别
- Mary稍后将恢复她的平板电脑会话，并在订阅您的新闻通讯时提供她的电子邮件地址。 在这样做时，流式摄取会添加新的身份作为她配置文件中的记录数据。 因此， [!DNL Identity Service] 现在将Mary的平板电脑设备活动与她的电子商务帐户历史记录关联起来。
- 下一次在她的平板电脑上单击时，您的目标内容可以反映玛丽的完整个人资料和历史记录，而不仅仅是未知购物者使用的平板电脑。

![Platform上的身份拼接](./images/identity-service-stitching.png)

基本上， [!DNL Identity Service] 使您可以拼合客户的完整信息，汇总可能分散在不同系统上的相关数据。 身份关系 [!DNL Identity Service] 定义和维护由Real-time Customer Profile用来全面了解客户及其与您品牌的互动。 欲了解更多信息，请参见 [Real-time Customer Profile概述](../profile/home.md).

### 用例

示例 [!DNL Identity Service] 实施包括：

- 电信公司可以依赖“电话号码”值，电话号码是指离线和在线数据集中的同一目标个人。
- 由于匿名访客比例较高，零售公司可能会在离线数据集中使用“电子邮件地址”，在在线数据集中使用ECID。
- 银行可能偏好离线数据集中的“帐号”，如分行交易。 它们可能依赖在线数据集中的“登录ID”，因为大多数访客在访问期间都将进行身份验证。
- 您的客户也可能具有唯一的专有ID，例如GUID或其他通用唯一标识符。

## 标识命名空间 {#identity-namespace}

>[!CONTEXTUALHELP]
>id="platform_identity_namespace"
>title="身份命名空间"
>abstract="标识命名空间用于区分标识的上下文或类型。例如，标识将“name<span>@email.com”识别为电子邮件地址，将“443522”识别为数字 CRM ID。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_identity_value"
>title="标识值"
>abstract="标识值是代表唯一个人、组织或资产的标识符。该值表示的标识的上下文或类型由相应的标识命名空间定义。当跨配置文件片段匹配记录数据时，命名空间和标识值必须匹配。"
>text="Learn more in documentation"

如果您问某人“您的ID是什么？” 如果没有进一步的情况，他们很难提供有用的答案。 按照相同的逻辑，表示标识值（无论是系统生成的ID还是电子邮件地址）的字符串值只有在提供用于提供字符串值上下文的限定符（身份命名空间）时才会完整。

您的客户可能通过线上和线下渠道的组合与您的品牌互动，这带来了如何将这些分散的互动整合为单个客户身份的难题。

要了解跨多个设备和渠道的客户，首先要在每个渠道中识别他们。 Platform通过使用身份命名空间来实现这一点。 身份命名空间是电子邮件或电话等标识符，用于为客户身份提供其他上下文。 身份命名空间用于查找或链接单个身份，并为身份值提供上下文。 请参阅 [身份命名空间概述](./namespaces.md) 以了解更多信息。

## 身份图

身份图是不同身份命名空间之间关系的映射，允许您可视化并更好地了解哪些客户身份以及如何拼合在一起。 请参阅上的教程 [使用身份图查看器](./ui/identity-graph-viewer.md) 以了解更多信息。

以下视频旨在支持您了解身份和身份图。

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## 将身份数据提供给 [!DNL Identity Service]

本节介绍在使用提供给Adobe Experience Platform的数据之前，如何处理这些数据。 [!DNL Identity Service] 为每个客户构建身份图。

### 决定标识字段

根据您的企业数据收集策略，标记为身份的数据字段将确定您的身份映射中包含哪些数据。 要实现Adobe Experience Platform的最大优势和最全面的客户身份，您应该上传在线和离线数据。

- 在线数据是描述在线状态和行为的数据，如用户名和电子邮件地址。

- 离线数据是指与在线状态不直接相关的数据，例如CRM系统的ID。 此类数据使您的身份更加稳健，并支持不同系统中的数据聚合。

### 创建其他身份命名空间

虽然Experience Platform提供了各种标准命名空间，但您可能需要创建其他命名空间来对您的身份正确分类。 有关更多信息，请参阅以下部分： [查看和创建组织的命名空间](./namespaces.md) 在身份命名空间概述中。

>[!NOTE]
>
>标识命名空间是标识的限定符。 因此，创建命名空间后，便无法删除该命名空间。

### 将身份数据包含在中 [!DNL Experience Data Model] (XDM)

作为标准化的框架， [!DNL Platform] 组织客户数据， [!DNL Experience Data Model] (XDM)允许跨Experience Platform和与之交互的其他服务共享和理解数据 [!DNL Platform]. 欲知更多信息，请参见 [XDM系统概述](../xdm/home.md).

记录架构和时序架构均提供了包含身份数据的方法。 在摄取数据时，如果发现来自不同命名空间的数据片段共享共同的身份数据，则身份图将在这些片段之间创建新的关系。

### 将XDM字段标记为标识

任何类型的字段 `string` 在实施记录或时间序列的架构中，XDM类可标记为标识字段。 因此，摄取到该字段中的所有数据都将被视为身份数据。

>[!NOTE]
>
>数组字段和映射类型字段不受支持，并且无法标记为标识字段。

如果标识字段共享公共PII数据，则还允许关联标识。
例如，通过将电话号码字段标记为标识字段， [!DNL Identity Service] 自动绘制与其他使用相同电话号码的个人的关系图。

>[!NOTE]
>
>在标记字段时，会提供生成的身份命名空间。

### 配置数据集 [!DNL Identity Service]

在流式摄取过程中， [!DNL Identity Service]自动从记录和时间序列数据中提取身份数据。 但是，在摄取数据之前，必须启用 [!DNL Identity Service]. 请参阅上的教程  [使用API为Real-time Customer Profile和Identity服务配置数据集](../profile/tutorials/dataset-configuration.md) 以了解更多信息。

### 将数据摄取到 [!DNL Identity Service]

[!DNL Identity Service] 使用通过以下任一方式发送到Experience Platform的XDM兼容数据 [批量摄取](../ingestion/batch-ingestion/overview.md) 或 [流式摄取](../ingestion/streaming-ingestion/overview.md).

以下视频旨在支持您了解Identity Service。 此视频介绍如何将数据字段标记为身份，以及在引入身份数据后，如何验证该数据是否已写入Adobe Experience Platform Identity Service专用图。

>[!WARNING]
>
>此 [!DNL Platform] 以下视频中显示的UI已过期。 请参阅文档以了解最新的UI屏幕截图和功能。

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## 数据管理

Adobe Experience Platform在构建时考虑到了隐私问题，并且包含一个数据治理框架以保护您的客户PII数据。 默认情况下，“电子邮件”或“电话”命名空间下的身份数据会被加密，但为了确保敏感数据在保留之前会被加密，可以在数据被摄取或到达时对其应用数据使用标签 [!DNL Platform]. 欲知更多信息，请阅读 [数据管理概述](../data-governance/home.md).

## 后续步骤

现在您已了解 [!DNL Identity Service] 以及它在Experience Platform中的角色，您可以开始学习如何使用您的身份图 [[!DNL Identity Service API]](./api/getting-started.md).
