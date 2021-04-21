---
keywords: Experience Platform；主页；热门主题；目录服务；目录服务；目录服务；数据位置；数据管理;数据管理；世系；目录；启用数据集
solution: Experience Platform
title: 目录服务概述
topic-legacy: overview
description: Catalog Service是Adobe Experience Platform中数据位置和谱系的记录系统。 虽然摄取到Experience Platform中的所有数据都作为文件和目录存储在数据湖中，但目录保留这些文件和目录的元数据和说明，以用于查找和监视。
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 5%

---

# [!DNL Catalog Service] 概述

[!DNL Catalog Service] 是Adobe Experience Platform中数据位置和谱系的记录系统。虽然收录到[!DNL Experience Platform]中的所有数据都作为文件和目录存储在[!DNL Data Lake]中，但[!DNL Catalog]保留这些文件和目录的元数据和说明，以用于查找和监视。

简而言之，[!DNL Catalog]充当元数据存储或“目录”，您可以在[!DNL Experience Platform]中找到有关数据的信息。 可以使用[!DNL Catalog]回答以下问题：

* 我的数据位于何处？
* 处理这些数据的阶段是什么？
* 哪些系统或进程对我的数据采取了行动？
* 已成功处理多少数据？
* 处理过程中发生了哪些错误？

[!DNL Catalog] 提供一个RESTful API，它允许您使用基本CRUD [!DNL Platform] 操作以编程方式管理元数据。有关详细信息，请参阅[目录开发人员指南](api/getting-started.md)。

## [!DNL Catalog] 和服 [!DNL Experience Platform] 务

[!DNL Catalog Service]跟踪的资源由多个[!DNL Experience Platform]服务使用。 为了充分利用[!DNL Catalog's]功能，建议您熟悉这些服务以及它们与[!DNL Catalog]的交互方式。

### [!DNL Experience Data Model] (XDM)系统

[!DNL Experience Data Model] (XDM)系统是组织客户体验数据 [!DNL Platform] 的标准化框架。[!DNL Experience Platform] 利用XDM模式以一致、可重用的方式描述数据结构。

当数据被摄取到[!DNL Platform]中时，该数据的结构将映射到XDM模式并作为数据集的一部分存储在[!DNL Data Lake]中。 每个数据集的元数据由[!DNL Catalog Service]跟踪，其中包括对数据集所符合的XDM模式的引用。

有关XDM系统的更多一般信息，请参阅[XDM系统概述](../xdm/home.md)。

### [!DNL Data Ingestion]

[!DNL Experience Platform] 从多个源中摄取数据，并将记录作为数据集保留在 [!DNL Data Lake]中。[!DNL Catalog] 跟踪这些数据集的元数据，而不管其来源或摄取方法。

使用批处理摄取方法时，[!DNL Catalog]还会跟踪批处理文件的其他元数据。 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。[!DNL Catalog] 跟踪这些批处理文件的元数据，以及它们在摄取后保留的数据集。批处理元数据包括有关成功摄取的记录数的信息，以及任何失败记录和关联的错误消息。

有关详细信息，请参阅[数据摄取概述](../ingestion/home.md)。

## [!DNL Catalog] 对象

如上节所述，[!DNL Catalog]跟踪其他[!DNL Platform]服务使用的几种资源和操作的元数据。 [!DNL Catalog] 维护其自己的“对象”存储，这些对象封装了此元数据。[!DNL Catalog] 对象是数据的可 [!DNL Platform] 查询表示形式，它允许您搜索、监视和标记数据，而无需访问数据本身。

下表概述了[!DNL Catalog]支持的不同对象类型：

| 对象 | API端点 | 定义 |
|---|---|---|
| 帐户 | `/accounts` | 创建源连接时，必须提供身份验证凭据。 帐户表示用于创建特定类型连接的身份验证凭据的集合。 每个连接都有一组唯一参数，这些参数由[!DNL Catalog]保留，并在[!DNL Azure Key Vault]中加以保护。 |
| 批 | `/batches` | 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。[!DNL Catalog]中的批处理对象概述了批处理的摄取量度（如已处理的记录数或磁盘上的大小），还可能包括指向受批处理操作影响的数据集、视图和其他资源的链接。 |
| Connection | `/connections` | 连接是源连接器的单个实例，对于您的组织是唯一的，并且使用连接器类型的适当身份验证凭据进行配置。 |
| 连接器 | `/connectors` | 连接器定义源连接如何从其他Adobe应用程序(如Adobe Analytics和Adobe Audience Manager)、第三方云存储源（如[!DNL Azure Blob]、[!DNL Amazon S3]、FTP服务器和SFTP服务器）以及第三方CRM系统（如[!DNL Microsoft Dynamics]和[!DNL Salesforce]）收集数据。 |
| 数据集 | `/dataSets` | 存储集是用于收集模式（通常是表）的和管理构造，其中包含数据（列）和字段（行）。 有关详细信息，请参阅[数据集概述](./datasets/overview.md)。 |
| 数据集文件 | `/datasetFiles` | 数据集文件表示已保存在[!DNL Platform]上的数据块。 作为文本文件的记录，您可以在这些位置找到文件的大小、包含的记录数以及对摄取文件的批次的引用。 |

## 后续步骤

本文档介绍了[!DNL Catalog Service]及其在[!DNL Experience Platform]更大范围内的工作方式。 有关与该[!DNL Catalog] API的不同端点交互的步骤，请参阅[[!DNL Catalog] 开发人员指南](api/getting-started.md)。 还建议您参阅[筛选目录数据](api/filter-data.md)指南，以遵循限制API响应中返回数据的最佳实践。
