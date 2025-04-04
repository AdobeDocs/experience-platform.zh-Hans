---
keywords: Experience Platform；主页；热门主题；目录服务；目录；目录服务；数据位置；数据管理；数据管理；谱系；谱系；目录；启用数据集
solution: Experience Platform
title: 目录服务概述
description: 目录服务是 Adobe Experience Platform 中记录数据位置和沿袭的系统。虽然所有摄取到 Experience Platform 中的数据均作为文件和目录存储在数据湖中，但目录中容纳这些文件和目录的元数据和描述以供查找和监控。
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 8%

---

# [!DNL Catalog Service] 概述

[!DNL Catalog Service]是Adobe Experience Platform中数据位置和族系的记录系统。 虽然所有被摄取到[!DNL Experience Platform]的数据都作为文件和目录存储在[!DNL Data Lake]中，但[!DNL Catalog]保留这些文件和目录的元数据和描述，以便进行查找和监视。

简而言之，[!DNL Catalog]充当元数据存储或“目录”，您可以在其中查找[!DNL Experience Platform]中有关您的数据的信息。 您可以使用[!DNL Catalog]回答以下问题：

* 我的数据位于何处？
* 此数据处于哪个处理阶段？
* 哪些系统或流程对我的数据执行了操作？
* 已成功处理多少数据？
* 处理过程中发生了哪些错误？

[!DNL Catalog]提供了一个RESTful API，允许您使用基本CRUD操作以编程方式管理[!DNL Experience Platform]元数据。 有关详细信息，请参阅[目录开发人员指南](api/getting-started.md)。

## [!DNL Catalog]和[!DNL Experience Platform]服务

[!DNL Catalog Service]跟踪的资源由多个[!DNL Experience Platform]服务使用。 为了充分利用[!DNL Catalog's]功能，建议您熟悉这些服务以及它们如何与[!DNL Catalog]交互。

### [!DNL Experience Data Model] (XDM)系统

[!DNL Experience Data Model] (XDM)系统是[!DNL Experience Platform]用于组织客户体验数据的标准化框架。 [!DNL Experience Platform]利用XDM架构以一致且可重用的方式描述数据结构。

将数据摄取到[!DNL Experience Platform]中时，该数据的结构将映射到XDM架构并作为数据集的一部分存储在[!DNL Data Lake]中。 [!DNL Catalog Service]跟踪每个数据集的元数据，包括对该数据集所遵循的XDM架构的引用。

有关XDM系统的更多常规信息，请参阅[XDM系统概述](../xdm/home.md)。

### [!DNL Data Ingestion]

[!DNL Experience Platform]从多个源摄取数据，并将记录作为[!DNL Data Lake]中的数据集保留。 [!DNL Catalog]跟踪这些数据集的元数据，无论其源或摄取方法如何。

使用批处理摄取方法时，[!DNL Catalog]还会跟踪批处理文件的其他元数据。 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。 [!DNL Catalog]跟踪这些批处理文件的元数据，以及摄取后它们保留的数据集。 批次元数据包括有关成功摄取的记录数的信息，以及任何失败记录和关联的错误消息。

有关详细信息，请参阅[数据引入概述](../ingestion/home.md)。

## [!DNL Catalog]对象

如上一节所述，[!DNL Catalog]跟踪其他[!DNL Experience Platform]服务使用的多种资源和操作的元数据。 [!DNL Catalog]保留其自己封装此元数据的“对象”存储。 [!DNL Catalog]对象是[!DNL Experience Platform]数据的可查询表示形式，允许您搜索、监视和标记数据而无需访问数据本身。

下表概述了[!DNL Catalog]支持的不同对象类型：

| 对象 | API端点 | 定义 |
|---|---|---|
| 批次 | `/batches` | 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。 [!DNL Catalog]中的批次对象概述了批次的摄取量度（例如处理的记录数或磁盘大小），并且可能还包括到受批次操作影响的数据集、视图和其他资源的链接。 |
| 数据集 | `/dataSets` | 数据集是用于收集数据的存储和管理结构（通常是表），其中包含架构（列）和字段（行）。 有关详细信息，请参阅[数据集概述](./datasets/overview.md)。 |
| 数据集文件 | `/datasetFiles` | 数据集文件表示已在[!DNL Experience Platform]上保存的数据块。 作为文本文件的记录，您可以从中找到文件的大小、包含的记录数以及对摄取文件的批次的引用。 |

## 后续步骤

本文档介绍了[!DNL Catalog Service]以及它如何在[!DNL Experience Platform]的较大范围内工作。 有关与该[!DNL Catalog] API的不同端点进行交互的步骤，请参阅[[!DNL Catalog] 开发人员指南](api/getting-started.md)。 建议您同时参阅关于[筛选目录数据](api/filter-data.md)的指南，以便遵循限制API响应中返回的数据的最佳实践。
