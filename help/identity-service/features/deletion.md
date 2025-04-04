---
title: Identity Service中的删除
description: 本文档概述了可用于在Experience Platform中删除身份数据的各种机制，并阐明身份图形可能受到哪些影响。
exl-id: 0619d845-71c1-4699-82aa-c6436815d5b3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 1%

---

# Identity Service中的删除

Adobe Experience Platform Identity Service通过确定性地关联个人跨设备和系统的身份来生成身份图。 当在同一行数据内接收到两个或多个标记的身份时，建立身份图链接。

实时客户档案利用身份图创建客户属性和行为的全面且单一视图，让您能够实时向人员而非设备提供有影响力的个人数字体验。

本文档概述了可用于在Experience Platform中删除身份数据的各种机制，并阐明身份图形可能受到哪些影响。

## 快速入门

以下文档引用了Experience Platform的以下功能：

* [身份服务](../home.md)：通过跨设备和系统桥接身份，更好地了解个人客户及其行为。
   * [身份图](./identity-graph-viewer.md)：身份图是特定客户不同身份之间关系的映射，它为您提供了客户如何跨不同渠道与您的品牌互动的可视表示形式。
   * [身份命名空间](./namespaces.md)：身份命名空间是Identity Service的组件，充当与身份相关的上下文的指示器。 例如，它们将“name<span>@email.com”的值区分为电子邮件地址或“443522”区分为数字CRMID。
* [目录服务](../../catalog/home.md)：浏览数据湖中的数据谱系、元数据、文件描述、目录和数据集。
* [数据卫生](../../hygiene/home.md)：通过计划自动数据集过期时间，或者从一个数据集或所有数据集中删除单个记录来管理存储的消费者数据。
* [Adobe Experience Platform Privacy Service](../../privacy-service/home.md)：管理客户跨多个Adobe Experience Cloud应用程序访问、选择退出销售或删除其个人数据的请求。
* [实时客户个人资料](../../profile/home.md)：根据来自多个来源的汇总数据，实时提供统一的客户个人资料。

## 单个身份删除

通过单个身份删除请求可以删除图形中的身份，从而删除与与身份命名空间关联的单个用户身份关联的链接。 您可以将[Privacy Service](../../privacy-service/home.md)提供的机制用于用例，例如客户请求删除数据以及遵守《通用数据保护条例》(GDPR)等隐私法规。

以下各节概述了可以在Experience Platform中用于单个身份删除请求的机制。

### 在Privacy Service中删除单个身份

Privacy Service会根据隐私法规(例如，《通用数据保护条例》(GDPR)和《加州消费者隐私法案》(CCPA))的规定，处理客户访问、选择退出销售或删除其个人数据的请求。 借助Privacy Service，您可以使用API或UI提交作业请求。 当Experience Platform收到来自Privacy Service的删除请求时，Experience Platform会向Privacy Service发送确认，确认已收到该请求并且已将受影响的数据标记为删除。 个人身份的删除基于提供的命名空间和/或ID值。 此外，还会删除与给定组织关联的所有沙盒。 有关详细信息，请参阅Identity Service](../privacy.md)中的[隐私请求处理指南。

下表提供了Privacy Service中单个身份删除的划分信息：

| 单一身份删除 | Privacy Service |
| --- | --- |
| 已接受的用例 | 仅数据隐私请求(GDPR、CCPA)。 |
| 估计延迟 | 几天到几周 |
| 受影响的服务 | Privacy Service中的单个身份删除允许您选择是从Identity Service、Real-Time Customer Profile还是数据湖中删除数据。 |
| 删除模式 | 从Identity Service中删除身份。 |

{style="table-layout:auto"}

## 数据集删除

以下各节概述了可用于删除Experience Platform中的数据集和相关标识链接的机制。

### 在目录服务中删除数据集

您可以使用目录服务提交数据集删除请求。 有关如何使用目录服务删除数据集的更多信息，请阅读有关使用目录服务API [删除对象的指南](../../catalog/api/delete-object.md)。 或者，您可以使用Experience Platform UI提交数据集删除请求。 有关详细信息，请阅读[数据集用户指南](../../catalog/datasets/user-guide.md#delete-a-dataset)。

### 数据保健中的数据集过期时间

Adobe Experience Platform UI中的[[!UICONTROL 数据卫生]工作区](../../hygiene/ui/overview.md)允许您安排数据集的过期时间。 当数据集达到其到期日期时，数据湖、Identity Service和Real-time Customer Profile会开始单独的进程，以从各自的服务中删除数据集的内容。 有关详细信息，请参阅[使用[!UICONTROL 数据保健]工作区](../../hygiene/ui/dataset-expiration.md)管理数据集过期时间的指南。

下表细列了目录服务中的数据集删除与数据卫生之间的差异：

| 数据集删除 | 目录服务 | 数据卫生 |
| --- | --- | --- |
| 已接受的用例 | 在Experience Platform中删除完整数据集及其关联的身份信息。 | 管理Experience Platform中存储的数据。 |
| 估计延迟 | Days | Days |
| 受影响的服务 | 通过目录服务删除数据集将从Identity Service、实时客户个人资料和数据湖中删除数据。 | 通过数据卫生删除数据集会从Identity Service、实时客户个人资料和数据湖中删除数据。 |
| 删除模式 | 从由特定数据集建立的Identity Service中删除链接身份。 | 根据到期计划，从由特定数据集建立的Identity Service中删除链接身份。 |

{style="table-layout:auto"}

## 删除后身份图的不同状态

所有标识图删除都会导致删除请求指定的两个或多个标识之间的链接。 对于数据集删除请求，将删除指定数据集建立的所有标识链接，并且可能会也可能不会从图形中删除标识。 对于单一身份删除请求，会删除指定身份的身份链接，因此会从所有身份图中删除身份值本身。 没有与另一个身份进行单个关联的身份不会存储在Identity Service中。

下面概述了删除可能对身份图状态产生的影响。

| 身份图状态 | 描述 |
| --- | --- |
| 部分更新 | 成功处理删除请求后，如果图形内至少有两个身份保持链接，则会对图形进行部分更新。 删除后，其余的标识链接可以保持相互连接，也可以根据被删除的标识将其拆分为两个或多个单独的图形。 |
| 完全删除 | 图表必须具有至少两个链接身份才能存在。 因此，如果删除请求导致删除图表中的所有现有链接，则该图表将被完全删除。 |
| 无更改 | 如果特定删除请求包含未与图形的任何成员关联的身份或数据集，则图形不受影响。 此外，即使删除请求确实删除了数据集或身份数据集组合之间的链接，图形也不会更新，因为该链接是由未删除的其他链接建立的。 这意味着，如果链接存在于两个不同的数据集中，则不会更新图形，因为只删除其中一个数据集。 |

{style="table-layout:auto"}

## 后续步骤

本文档介绍了可用于删除Experience Platform上的身份和数据集的各种机制。 本文档还概述了身份和数据集删除如何影响身份图。 有关身份标识服务的更多信息，请参阅[身份标识服务概述](../home.md)。

<!--

You can use [Data hygiene](../hygiene/home.md) for data cleansing, removing anonymous data, or data minimization for the data that you have collected.

### Single identity deletion in the [!UICONTROL Data Hygiene] workspace

The [[!UICONTROL Data Hygiene] workspace](../hygiene/ui/overview.md) in the Experience Platform UI allows you to delete consumer records that are participating in Identity Service and Real-Time Customer Profile. For a comprehensive guide on using the [!UICONTROL Data Hygiene] workspace, see the tutorial on [deleting consumer records](../hygiene/ui/record-delete.md).

The table below provides a breakdown of differences between single identity deletion in Privacy Service and Data hygiene:

| Single identity deletion | Privacy Service | Data hygiene |
| --- | --- | --- |
| Accepted use cases | Data privacy requests (GDPR, CCPA) only. | Management of data stored in Experience Platform. |
| Estimated latency | Days to weeks | Days |
| Services impacted | Single identity deletion in Privacy Service allows you to select whether data will be deleted from Identity Service, Real-Time Customer Profile, or data lake. | Single identity deletion in Data hygiene deletes the selected data across Identity Service, Real-Time Customer Profile, and data lake. |
| Deletion patterns | Delete an identity from Identity Service. | Delete an identity from Identity Service. |

-->
