---
keywords: Experience Platform；主页；热门主题；目录服务；目录服务；数据位置；数据位置；数据管理；谱系；谱系；目录；启用数据集
solution: Experience Platform
title: 目录服务概述
description: 目录服务是Adobe Experience Platform中数据位置和谱系的记录系统。 虽然摄取到Experience Platform的所有数据都作为文件和目录存储在数据湖中，但Catalog会保存这些文件和目录的元数据和说明，以便进行查找和监控。
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 5%

---

# [!DNL Catalog Service] 概述

[!DNL Catalog Service] 是Adobe Experience Platform中数据位置和谱系的记录系统。 而所有被摄取到 [!DNL Experience Platform] 存储在 [!DNL Data Lake] 作为文件和目录， [!DNL Catalog] 包含这些文件和目录的元数据和说明，以便进行查找和监控。

简言之， [!DNL Catalog] 充当元数据存储或“目录”，您可以在其中找到有关数据的信息 [!DNL Experience Platform]. 您可以使用 [!DNL Catalog] 回答以下问题：

* 我的数据位于何处？
* 此数据在处理的哪个阶段？
* 哪些系统或进程对我的数据采取了行动？
* 已成功处理多少数据？
* 处理过程中发生了哪些错误？

[!DNL Catalog] 提供允许您以编程方式管理的RESTful API [!DNL Platform] 元数据。 请参阅 [目录开发人员指南](api/getting-started.md) 以了解更多信息。

## [!DNL Catalog] 和 [!DNL Experience Platform] 服务

资源 [!DNL Catalog Service] 跟踪由多个 [!DNL Experience Platform] 服务。 为了充分利用 [!DNL Catalog's] 功能，建议您熟悉这些服务以及它们与 [!DNL Catalog].

### [!DNL Experience Data Model] (XDM)系统

[!DNL Experience Data Model] (XDM)系统是标准化框架， [!DNL Platform] 组织客户体验数据。 [!DNL Experience Platform] 利用XDM模式以可重用的一致方式描述数据结构。

数据被摄取到 [!DNL Platform]，则该数据的结构会映射到XDM架构并存储在 [!DNL Data Lake] 作为数据集的一部分。 每个数据集的元数据由 [!DNL Catalog Service]，其中包含对数据集符合的XDM架构的引用。

有关XDM系统的更多常规信息，请参阅 [XDM系统概述](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] 从多个源中摄取数据，并将记录作为数据集保留在 [!DNL Data Lake]. [!DNL Catalog] 跟踪这些数据集的元数据，而不考虑其源或摄取方法。

使用批量摄取方法时， [!DNL Catalog] 还跟踪批处理文件的其他元数据。 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。[!DNL Catalog] 跟踪这些批处理文件的元数据，以及在摄取后保留的数据集。 批量元数据包括有关成功摄取的记录数以及任何失败记录和关联错误消息的信息。

请参阅 [数据摄取概述](../ingestion/home.md) 以了解更多信息。

## [!DNL Catalog] 对象

如上节所述， [!DNL Catalog] 跟踪其他资源和操作使用的几种类型的元数据 [!DNL Platform] 服务。 [!DNL Catalog] 维护其自己的“对象”存储库，该存储库将封装此元数据。 [!DNL Catalog] 对象是可查询的表示 [!DNL Platform] 数据，您无需访问数据本身即可搜索、监控和标记数据。

下表概述了支持的不同对象类型 [!DNL Catalog]:

| 对象 | API端点 | 定义 |
|---|---|---|
| 帐户 | `/accounts` | 创建源连接时，必须提供身份验证凭据。 帐户表示用于创建特定类型连接的身份验证凭据的集合。 每个连接都有一组由保留的唯一参数 [!DNL Catalog] 在 [!DNL Azure Key Vault]. |
| 批次 | `/batches` | 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。中的批处理对象 [!DNL Catalog] 概述了批处理的摄取量度（如已处理的记录数或磁盘大小），并且可能还包含指向受批处理操作影响的数据集、视图和其他资源的链接。 |
| Connection | `/connections` | 连接是源连接器的单个实例，对您的组织是唯一的，使用连接器类型的相应身份验证凭据进行配置。 |
| 连接器 | `/connectors` | 连接器定义源连接如何从其他Adobe应用程序(如Adobe Analytics和Adobe Audience Manager)、第三方云存储源(如 [!DNL Azure Blob], [!DNL Amazon S3]、FTP服务器和SFTP服务器)以及第三方CRM系统(例如 [!DNL Microsoft Dynamics] 和 [!DNL Salesforce])。 |
| 数据集 | `/dataSets` | 数据集是用于收集数据（通常是表）的存储和管理结构，其中包含架构（列）和字段（行）。 请参阅 [数据集概述](./datasets/overview.md) 以了解更多信息。 |
| 数据集文件 | `/datasetFiles` | 数据集文件表示已保存的数据块 [!DNL Platform]. 作为文字文件的记录，您可以在这些文件中找到文件的大小、包含的记录数以及对摄取文件的批处理的引用。 |

## 后续步骤

本文档介绍了 [!DNL Catalog Service] 以及它在 [!DNL Experience Platform]. 请参阅 [[!DNL Catalog] 开发人员指南](api/getting-started.md) 以了解与的不同端点进行交互的步骤 [!DNL Catalog] API。 建议您参阅 [筛选目录数据](api/filter-data.md) 以遵循限制API响应中返回的数据的最佳实践。
