---
title: 在Identity服务中删除
description: 本文档概述了可用于在Experience Platform中删除身份数据的各种机制，并明确了身份图可能受到何种影响。
source-git-commit: 17e39f6e9d6e62e22f867de91d571593ba945c71
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 在Identity服务中删除

Adobe Experience Platform Identity Service通过跨设备和系统为个人确定性地关联身份来生成身份图。 当在同一数据行中接收到两个或多个标记身份时，建立身份图链接。

实时客户资料利用身份图来创建客户属性和行为的全面、单一视图，使您能够实时地向人员而不是设备提供有影响的个人数字体验。

本文档概述了可用于在Experience Platform中删除身份数据的各种机制，并明确了身份图可能受到何种影响。

## 快速入门

以下文档引用了Experience Platform的以下功能：

* [Identity Service](home.md):通过跨设备和系统桥接身份，更好地了解各个客户及其行为。
   * [身份图](./ui/identity-graph-viewer.md):身份图是特定客户不同身份之间关系的映射，可直观地展示客户如何跨不同渠道与您的品牌进行交互。
   * [身份命名空间](namespaces.md):身份命名空间是Identity Service的组件，充当与身份相关的上下文的指示器。 例如，它们会区分“name”的值<span>@email.com”作为电子邮件地址，或“443522”作为数字CRM ID。
* [目录服务](../catalog/home.md):浏览数据湖中的数据谱系、元数据、文件描述、目录和数据集。
* [数据卫生](../hygiene/home.md):通过计划自动数据集过期时间或从一个数据集或所有数据集中删除单个记录，来管理您存储的消费者数据。
* [Adobe Experience Platform Privacy Service](../privacy-service/home.md):管理客户在Adobe Experience Cloud应用程序中访问、选择退出销售或删除其个人数据的请求。
* [实时客户资料](../profile/home.md):根据来自多个来源的汇总数据，实时提供统一的客户用户档案。

## 单个身份删除

单个身份删除请求允许您删除图表中的身份，从而删除与单个用户身份关联的链接，该用户身份与标识命名空间关联。 您可以使用 [数据卫生](../hygiene/home.md) 用于数据清理、删除匿名数据或收集数据的数据最小化。 对于客户请求删除数据以及遵守隐私法规(如《通用数据保护条例》(GDPR))等用例，您可以使用 [Privacy Service](../privacy-service/home.md).

以下各节概述了可用于Experience Platform中单个身份删除请求的机制。

### 删除单个身份Privacy Service

Privacy Service处理客户访问、选择退出销售或删除其个人数据的请求，这些请求符合隐私法规(如《通用数据保护条例》(GDPR)和《加州消费者隐私法案》(CCPA)等规定。 通过Privacy Service，您可以使用API或UI提交作业请求。 当Experience Platform收到来自Privacy Service的删除请求时，Platform会向Privacy Service发送确认，确认该请求已被接收，且受影响的数据已被标记为删除。 单个身份的删除基于提供的命名空间和/或ID值。 此外，与给定组织关联的所有沙箱都会被删除。 有关更多信息，请阅读 [Identity Service中的隐私请求处理](privacy.md).

### 在 [!UICONTROL 数据卫生] 工作区

的 [[!UICONTROL 数据卫生] 工作区](../hygiene/ui/overview.md) 在Platform UI中，您可以删除参与Identity服务和实时客户资料的客户记录。 有关使用 [!UICONTROL 数据卫生] 工作区中，请参阅 [删除消费者记录](../hygiene/ui/record-delete.md).

下表列出了Privacy Service和数据卫生中单个身份删除之间的差异：

| 单个身份删除 | Privacy Service | 数据卫生 |
| --- | --- | --- |
| 已接受的用例 | 仅限数据隐私请求(GDPR、CCPA)。 | 管理存储在Experience Platform中的数据。 |
| 估计滞后 | 从天到周 | Days |
| 受服务影响 | Privacy Service中的单个身份删除允许您选择数据是从Identity Service、实时客户资料还是数据湖中删除。 | 数据卫生中的单个身份删除会在“身份服务”、“实时客户资料”和“数据湖”中删除选定的数据。 |
| 删除模式 | 从Identity Service中删除身份。 | 从Identity Service中删除身份。 |

{style=&quot;table-layout:auto&quot;}

## 数据集删除

以下各节概述了可用于删除Experience Platform中数据集和相关身份链接的机制。

### 目录服务中的数据集删除

您可以使用目录服务提交数据集删除请求。 有关如何使用Catalog Service删除数据集的更多信息，请阅读 [使用目录服务API删除对象](../catalog/api/delete-object.md). 或者，您也可以使用Platform UI提交数据集删除请求。 有关更多信息，请阅读 [datasets用户指南](../catalog/datasets/user-guide.md#delete-a-dataset).

### 数据卫生中的数据集过期

的 [[!UICONTROL 数据卫生] 工作区](../hygiene/ui/overview.md) 在Adobe Experience Platform UI中，您可以计划数据集的过期日期。 当数据集到期日期时，数据湖、Identity Service和实时客户配置文件会开始各自的流程，以从各自的服务中删除数据集的内容。 有关更多信息，请阅读 [使用管理数据集过期 [!UICONTROL 数据卫生] 工作区](../hygiene/ui/dataset-expiration.md).

下表列出了“目录服务”中删除数据集与数据卫生之间的差异：

| 数据集删除 | 目录服务 | 数据卫生 |
| --- | --- | --- |
| 已接受的用例 | 删除Platform中的完整数据集及其关联的身份信息。 | 管理存储在Experience Platform中的数据。 |
| 估计滞后 | Days | Days |
| 受服务影响 | 通过“目录服务”删除数据集会从“身份服务”、“实时客户配置文件”和“数据湖”中删除数据。 | 通过数据卫生删除数据集会从Identity Service、“实时客户资料”和“数据湖”中删除数据。 |
| 删除模式 | 从由特定数据集建立的Identity服务中删除链接的身份。 | 根据过期计划，从由特定数据集建立的Identity Service中删除链接的身份。 |

{style=&quot;table-layout:auto&quot;}

## 删除后身份图的不同状态

删除所有标识图会导致删除两个或更多标识之间的链接，如删除请求所指定。 对于数据集删除请求，由指定数据集建立的所有身份链接都将被删除，并且可能或不会从图表中删除身份。 对于单个身份删除请求，将删除指定身份的身份链接，从而从所有身份图中删除身份值本身。 没有与其他身份的单个链接的身份不会存储在Identity Service中。

下面概述删除可能对身份图状态产生的潜在影响。

| 身份图状态 | 描述 |
| --- | --- |
| 部分更新 | 成功处理删除请求后，图表中至少有两个标识保持关联时，会进行局部更新。 删除后，剩余的身份链接可能会彼此保持连接，或者可以根据删除的身份拆分为两个或多个单独的图表。 |
| 完全移除 | 图表必须至少具有两个链接的标识才能存在。 因此，如果删除请求导致删除图表中的所有现有链接，则图表将被完全删除。 |
| 无更改 | 如果某个特定删除请求包含的标识或数据集与该图表的任何成员都不关联，则该图表将不会受到影响。 此外，即使删除请求确实删除了数据集或身份数据集组合之间的链接，也不会更新图表，因为该链接是由其他未删除的链接建立的。 这意味着如果链接存在于两个不同的数据集中，则不会更新图表，因为只会删除其中一个数据集。 |

{style=&quot;table-layout:auto&quot;}

## 后续步骤

本文档介绍了可用于删除Experience Platform上的身份和数据集的各种机制。 本文档还概述了身份和数据集删除如何影响身份图。 有关Identity Service的更多信息，请阅读 [Identity Service概述](home.md).