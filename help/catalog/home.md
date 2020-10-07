---
keywords: Experience Platform;home;popular topics;catalog service;catalog;Catalog service;data location;Data Location;Data management;data management;Lineage;lineage;Catalog;enable dataset
solution: Experience Platform
title: 目录服务概述
topic: overview
description: 目录服务是Adobe Experience Platform内数据位置和谱系的记录系统。 当所有被引入Experience Platform的数据作为文件和目录存储在数据湖中时，目录会保存这些文件和目录的元数据和描述，以便进行查找和监视。
translation-type: tm+mt
source-git-commit: 34cfcaac276bf2645a0365a0dfa71c4ead6e2ecb
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 5%

---


# [!DNL Catalog Service]概述

[!DNL Catalog Service] 是Adobe Experience Platform境内数据定位和谱系记录系统。 当所有被引入的数据 [!DNL Experience Platform] 作为文件和目 [!DNL Data Lake] 录存储在中时， [!DNL Catalog] 保留这些文件和目录的元数据和说明以供查找和监视。

只需简单 [!DNL Catalog] 地放入，即可充当元数据存储或“目录”，在此可以在中查找有关数据的信息 [!DNL Experience Platform]。 您可以使 [!DNL Catalog] 用来回答以下问题：

* 我的数据位于何处？
* 这些数据处于哪个处理阶段？
* 哪些系统或进程对我的数据采取了行动？
* 成功处理了多少数据？
* 处理过程中发生了哪些错误？

[!DNL Catalog] 提供一个RESTful API，它允许您使用基本的CRUD [!DNL Platform] 操作以编程方式管理元数据。 See the [Catalog developer guide](api/getting-started.md) for more information.

## [!DNL Catalog] 和服 [!DNL Experience Platform] 务

跟踪的资 [!DNL Catalog Service] 源被多个服务 [!DNL Experience Platform] 使用。 为了充分利用这些 [!DNL Catalog's] 功能，建议您熟悉这些服务及其交互方式 [!DNL Catalog]。

### [!DNL Experience Data Model] (XDM)系统

[!DNL Experience Data Model] (XDM)系统是组织客户体验数据的 [!DNL Platform] 标准化框架。 [!DNL Experience Platform] 利用XDM模式以一致、可重用的方式描述数据结构。

当数据被摄取 [!DNL Platform]到其中时，该模式的结构将映射到XDM并作为数据集的一 [!DNL Data Lake] 部分存储在该数据中。 每个数据集的元数据 [!DNL Catalog Service]都由跟踪，包括对数据集所符合的XDM模式的引用。

有关XDM系统的更多一般信息，请参阅 [XDM系统概述](../xdm/home.md)。

### [!DNL Data Ingestion]

[!DNL Experience Platform] 从多个源中摄取数据，并将记录作为数据集保留在 [!DNL Data Lake]中。 [!DNL Catalog] 跟踪这些数据集的元数据，无论其来源或摄取方法如何。

使用批处理摄取方法时，还 [!DNL Catalog] 会跟踪批处理文件的其他元数据。 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。[!DNL Catalog] 跟踪这些批处理文件的元数据，以及它们在摄取后保留的数据集。 批处理元数据包括有关成功摄取的记录数的信息，以及任何失败记录和关联的错误消息。

有关更多 [信息，请参见](../ingestion/home.md) “数据获取概述”。

## [!DNL Catalog] 对象

如上一节所述，将跟踪 [!DNL Catalog] 其他服务所使用的几种资源和操作的元数 [!DNL Platform] 据。 [!DNL Catalog] 维护其自己的“对象”存储，其中包含此元数据。 [!DNL Catalog] 对象是数据的可 [!DNL Platform] 查询表示形式，它允许您搜索、监视和标记数据，而无需访问数据本身。

下表概述了支持的不同对象类型 [!DNL Catalog]:

| 对象 | API端点 | 定义 |
|---|---|---|
| 帐户 | `/accounts` | 创建源连接时，必须提供身份验证凭据。 帐户表示用于创建特定类型连接的身份验证凭据的集合。 每个连接都有一组唯一参数，这些参数由 [!DNL Catalog] 并保护在中 [!DNL Azure Key Vault]。 |
| 批 | `/batches` | 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。中的批处理对 [!DNL Catalog] 象概述了批处理的摄取量度（如已处理的记录数或磁盘大小），还可能包括指向受批处理操作影响的数据集、视图和其他资源的链接。 |
| 连接 | `/connections` | 连接是源连接器的单个实例，对于您的组织是唯一的，并且使用相应的连接器类型身份验证凭据进行配置。 |
| 连接器 | `/connectors` | 连接器定义源连接如何从其他Adobe应用程序(如Adobe Analytics和Adobe Audience Manager)、第三方云存储源(如 [!DNL Azure Blob]、 [!DNL Amazon S3]FTP服务器和SFTP服务器)以及第三方CRM系统(如 [!DNL Microsoft Dynamics] 和 [!DNL Salesforce])收集数据。 |
| 数据集 | `/dataSets` | 数据集是用于存储（通常是表）集合的模式和管理构造，其中包含（列）和字段（行）。 有关更多 [信息，请参](./datasets/overview.md) 阅数据集概述。 |
| 数据集文件 | `/datasetFiles` | 数据集文件表示已保存的数据块 [!DNL Platform]。 作为文本文件的记录，您可以在这些位置找到文件的大小、文件包含的记录数以及对摄取文件的批次的引用。 |

## 后续步骤

本文档介绍了它 [!DNL Catalog Service] 在更大范围内的功能及其运行方式 [!DNL Experience Platform]。 有关与 [[!DNL Catalog] 该API的](api/getting-started.md) 不同端点进行交互的步骤，请参阅开发 [!DNL Catalog] 人员指南。 建议您还参考有关过滤目录数 [据的指南](api/filter-data.md) ，以遵循限制API响应中返回数据的最佳实践。