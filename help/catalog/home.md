---
keywords: Experience Platform；主页；热门主题；目录服务；目录；目录服务；数据位置；数据位置；数据管理；数据管理；谱系；谱系；目录；启用数据集
solution: Experience Platform
title: 目录服务概述
description: 目录服务是Adobe Experience Platform中数据位置和谱系的记录系统。 虽然摄取到Experience Platform中的所有数据都将作为文件和目录存储在Data Lake中，但Catalog会保存这些文件和目录的metadata和描述，以供查找和监控。
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
source-git-commit: 0ebe9eadb1bce6252b43a50af009ce1b0f6e5d6e
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 6%

---

# [!DNL Catalog Service] 概述

[!DNL Catalog Service] 是Adobe Experience Platform中数据位置和族系的记录系统。 虽然所有数据都已摄取 [!DNL Experience Platform] 存储在 [!DNL Data Lake] 作为文件和目录， [!DNL Catalog] 保存这些文件和目录的元数据和描述，以供查找和监控。

简言之， [!DNL Catalog] 充当元数据存储或“目录”，您可以在其中查找有关您的数据的信息 [!DNL Experience Platform]. 您可以使用 [!DNL Catalog] 回答以下问题：

* 我的数据位于何处？
* 此数据处于哪个处理阶段？
* 哪些系统或流程对我的数据执行了操作？
* 已成功处理多少数据？
* 处理过程中发生了哪些错误？

[!DNL Catalog] 提供一个RESTful API，允许您以编程方式管理 [!DNL Platform] 使用基本CRUD操作的元数据。 请参阅 [目录开发人员指南](api/getting-started.md) 了解更多信息。

## [!DNL Catalog] 和 [!DNL Experience Platform] 服务

满足以下条件的资源 [!DNL Catalog Service] 多个曲目使用 [!DNL Experience Platform] 服务。 为了充分利用 [!DNL Catalog's] 建议您熟悉这些服务以及它们如何与交互 [!DNL Catalog].

### [!DNL Experience Data Model] (XDM)系统

[!DNL Experience Data Model] (XDM)系统是一种标准化的框架，通过它 [!DNL Platform] 组织客户体验数据。 [!DNL Experience Platform] 利用XDM架构以一致且可重用的方式描述数据结构。

当数据被摄取到 [!DNL Platform]，则该数据的结构会映射到XDM架构并存储在 [!DNL Data Lake] 作为数据集的一部分。 每个数据集的元数据由进行跟踪 [!DNL Catalog Service]，包括对数据集符合的XDM架构的引用。

有关XDM系统的更多常规信息，请参阅 [XDM系统概述](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] 从多个源摄取数据，并将记录作为数据集保留在 [!DNL Data Lake]. [!DNL Catalog] 跟踪这些数据集的元数据，无论其源或摄取方法如何。

使用批量摄取方法时， [!DNL Catalog] 还跟踪批处理文件的其他元数据。 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。[!DNL Catalog] 跟踪这些批处理文件的元数据，以及摄取后它们保留的数据集。 批量元数据包括有关成功摄取的记录数的信息，以及任何失败记录和关联的错误消息。

请参阅 [数据摄取概述](../ingestion/home.md) 了解更多信息。

## [!DNL Catalog] 对象

如上一节所述， [!DNL Catalog] 跟踪由其他资源使用的多种资源和操作的元数据 [!DNL Platform] 服务。 [!DNL Catalog] 维护其自己封装此元数据的“对象”存储。 [!DNL Catalog] 对象是可查询的表示形式 [!DNL Platform] 让您可以搜索、监控和标记数据，而无需访问数据本身。

下表概述了支持的各种对象类型 [!DNL Catalog]：

| 对象 | API端点 | 定义 |
|---|---|---|
| 批次 | `/batches` | 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。中的批次对象 [!DNL Catalog] 概述了批处理的摄取量度（例如处理的记录数或磁盘大小），并且可能还包括指向数据集、视图和受批处理操作影响的其他资源的链接。 |
| 数据集 | `/dataSets` | 数据集是用于收集数据的存储和管理结构（通常是表），其中包含架构（列）和字段（行）。 请参阅 [数据集概述](./datasets/overview.md) 了解更多信息。 |
| 数据集文件 | `/datasetFiles` | 数据集文件表示已保存的数据块 [!DNL Platform]. 作为文本文件的记录，您可以在此处找到文件的大小、包含的记录数以及对摄取文件的批次的引用。 |

## 后续步骤

本文档介绍了 [!DNL Catalog Service] 以及它在更大范围内如何运行 [!DNL Experience Platform]. 请参阅 [[!DNL Catalog] 开发人员指南](api/getting-started.md) 以了解与该报表的不同端点进行交互的步骤 [!DNL Catalog] API。 建议您同时参阅以下内容的相关指南： [筛选目录数据](api/filter-data.md) 以遵循限制API响应中返回的数据的最佳实践。
