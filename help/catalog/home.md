---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 目录服务概述
topic: overview
translation-type: tm+mt
source-git-commit: 1fce86193bc1660d0f16408ed1b9217368549f6c
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 5%

---


# 目录服务概述

目录服务是Adobe Experience Platform中数据位置和世系的记录系统。 虽然引入到Experience Platform的所有数据都以文件和目录形式存储在数据湖中，但目录保留这些文件和目录的元数据和说明，以便进行查找和监控。

简单地说，Catalog充当元数据存储或“目录”，您可以在Experience Platform中找到有关数据的信息。 您可以使用目录回答以下问题：

* 我的数据位于何处？
* 这些数据处于哪个处理阶段？
* 哪些系统或进程对我的数据采取了行动？
* 成功处理了多少数据？
* 处理过程中发生了哪些错误？

Catalog提供一个RESTful API，它允许您使用基本的CRUD操作以编程方式管理平台元数据。 See the [Catalog developer guide](api/getting-started.md) for more information.

## 目录和体验平台服务

目录服务跟踪的资源由多个Experience Platform服务使用。 为了充分利用目录的功能，建议您熟悉这些服务以及它们与目录的交互方式。

### 体验数据模型(XDM)系统

体验数据模型(XDM)系统是平台组织客户体验数据的标准化框架。 Experience Platform利用XDM模式以一致、可重用的方式描述数据结构。

当数据被引入平台时，该数据的结构将映射到XDM模式并作为数据集的一部分存储在数据 **湖中**。 每个数据集的元数据由目录服务跟踪，该服务包括对数据集所符合的XDM模式的引用。

有关XDM系统的更多一般信息，请参阅 [XDM系统概述](../xdm/home.md)。

### 数据获取

Experience Platform从多个来源收集数据，并将记录作为数据湖中的数据集保留。 Catalog跟踪这些数据集的元数据，而不管其来源或摄取方法如何。

使用批处理摄取方法时，Catalog还会跟踪批处理文件的其 **他元** 数据。 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。目录跟踪这些批处理文件的元数据以及它们在摄取后保留的数据集。 批处理元数据包括有关成功摄取的记录数的信息，以及任何失败记录和关联的错误消息。

有关更多 [信息，请参见](../ingestion/home.md) “数据获取概述”。

## 目录对象

如上节所述，目录跟踪其他平台服务使用的几种资源和操作的元数据。 目录保留其自己的“对象”存储，这些对象封装此元数据。 目录对象是平台数据的可查询表示形式，它允许您搜索、监视和标记数据，而无需访问数据本身。

下表概述了Catalog支持的不同对象类型：

| 对象 | API端点 | 定义 |
|---|---|---|
| 帐户 | `/accounts` | 创建源连接时，必须提供身份验证凭据。 帐户表示用于创建特定类型连接的身份验证凭据的集合。 每个连接都有一组唯一参数，这些参数由Catalog保留并在Azure密钥保管库中保护。 |
| 批 | `/batches` | 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。目录中的批处理对象概述了批处理的摄取量度（如已处理的记录数或磁盘大小），还可能包括指向受批处理操作影响的数据集、视图和其他资源的链接。 |
| 连接 | `/connections` | 连接是源连接器的单个实例，对于您的组织是唯一的，并且使用相应的连接器类型身份验证凭据进行配置。 |
| 连接器 | `/connectors` | 连接器定义源连接如何从其他Adobe应用程序(如Adobe Analytics和Adobe受众管理器)、第三方云存储源（如Azure Blob、Amazon S3、FTP服务器和SFTP服务器）以及第三方CRM系统（如Microsoft Dynamics和Salesforce）收集数据。 |
| 数据集 | `/dataSets` | 数据集是用于存储（通常是表）集合的模式和管理构造，其中包含（列）和字段（行）。 有关更多 [信息，请参](./datasets/overview.md) 阅数据集概述。 |
| 数据集文件 | `/datasetFiles` | 数据集文件表示已保存在平台上的数据块。 作为文本文件的记录，您可以在这些位置找到文件的大小、文件包含的记录数以及对摄取文件的批次的引用。 |

## 后续步骤

本文档介绍了目录服务及其在更大范围的Experience Platform中的功能。 有关与 [该目录API的](api/getting-started.md) 不同端点进行交互的步骤，请参阅目录开发人员指南。 建议您还参考有关过滤目录数 [据的指南](api/filter-data.md) ，以遵循限制API响应中返回数据的最佳实践。