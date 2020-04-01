---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 目录服务概述
topic: overview
translation-type: tm+mt
source-git-commit: eec5b07427aa9daa44d23f09cfaf1b38f8e811f3

---


# 目录服务概述

Catalog Service是Adobe Experience Platform中用于数据位置和世系的记录系统。 虽然收录到Experience Platform中的所有数据都以文件和目录的形式存储在Data Lake中，但Catalog会保留这些文件和目录的元数据和说明，以便进行查找和监视。

简而言之，Catalog充当元数据存储或“目录”，您可以在Experience Platform中找到有关数据的信息。 您可以使用“目录”回答以下问题：

* 我的数据位于何处？
* 这些数据处于哪个处理阶段？
* 哪些系统或进程对我的数据采取了行动？
* 已成功处理多少数据？
* 处理过程中发生了哪些错误？

Catalog提供了一个RESTful API，它允许您使用基本的CRUD操作以编程方式管理平台元数据。 See the [Catalog developer guide](api/getting-started.md) for more information.

## 目录和体验平台服务

目录服务跟踪的资源由多个Experience Platform服务使用。 为了充分利用Catalog的功能，建议您熟悉这些服务以及它们与Catalog的交互方式。

### 体验数据模型(XDM)系统

Experience Data Model(XDM)System是Platform组织客户体验数据的标准化框架。 Experience Platform利用XDM模式以一致、可重用的方式描述数据结构。

当数据被引入平台时，该数据的结构将映射到XDM模式并作为数据集的一部分存储在数据 **湖中**。 每个数据集的元数据由Catalog Service跟踪，它包括对数据集所符合的XDM模式的引用。

有关XDM系统的更多常规信息，请参阅 [XDM系统概述](../xdm/home.md)。

### 数据摄取

Experience Platform从多个来源收集数据，并将记录作为数据湖中的数据集保留。 Catalog可跟踪这些数据集的元数据，而不管其来源或摄取方法如何。

使用批处理摄取方法时，Catalog还会跟踪批处理文件的其 **他元数据** 。 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。 “目录”可跟踪这些批处理文件的元数据，以及它们在摄取后保留的数据集。 批处理元数据包括有关成功摄取的记录数的信息，以及任何失败的记录和关联的错误消息。

有关更多 [信息，请参阅数据获取概述](../ingestion/home.md) 。

## 目录对象

如上节所述，“目录”跟踪其他平台服务使用的几种资源和操作的元数据。 Catalog维护其自己的“对象”存储，这些对象封装了此元数据。 Catalog对象是平台数据的可查询表示形式，它允许您搜索、监视和标记数据，而无需访问数据本身。

下表概述了Catalog支持的不同对象类型：

| 对象 | API端点 | 定义 |
|---|---|---|
| 帐户 | `/accounts` | 创建源连接时，必须提供身份验证凭据。 帐户表示用于创建特定类型连接的身份验证凭据的集合。 每个连接都有一组唯一参数，这些参数由Catalog保留并在Azure密钥存储区中得到保护。 |
| 批处理 | `/batches` | 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。 Catalog中的批处理对象概述了批处理的摄取度量（如已处理的记录数或磁盘大小），并且可能还包括指向受批处理操作影响的数据集、视图和其他资源的链接。 |
| 连接 | `/connections` | 连接是源连接器的单个实例，对于您的组织唯一，并使用连接器类型的适当身份验证凭据进行配置。 |
| 连接器 | `/connectors` | 连接器定义源连接如何从其他Adobe应用程序(如Adobe Analytics和Adobe受众管理器)、第三方云存储源（如Azure Blob、Amazon S3、FTP服务器和SFTP服务器）和第三方CRM系统（如Microsoft Dynamics和Salesforce）收集数据。 |
| 数据集 | `/dataSets` | 数据集是用于收集数据（通常是表）的存储和管理构造，其中包含模式（列）和字段（行）。 |
| 数据集文件 | `/datasetFiles` | 数据集文件表示已在平台上保存的数据块。 作为文本文件的记录，您可以在这些位置找到文件的大小、文件包含的记录数以及对摄取文件的批次的引用。 |

## 后续步骤

本文档介绍了Catalog Service及其在更大范围的Experience Platform中的功能。 有关与 [该目录API的不同端点交互的步骤](api/getting-started.md) ，请参阅目录开发人员指南。 建议您还参阅有关过滤目录数据的指 [南](api/filter-data.md) ，以遵循限制API响应中返回数据的最佳实践。