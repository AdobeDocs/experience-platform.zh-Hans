---
title: Adobe Experience Platform 发行说明（2021 年 9 月）
description: Adobe Experience Platform 2021 年 9 月发行说明。
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 29%

---

# Adobe Experience Platform 发行说明

**发行日期： 2021年9月29日**

Adobe Experience Platform 中现有功能的更新：

- [数据引入](#ingestion)
- [[!DNL Data Prep]](#data-prep)
- [源](#sources)

## 数据引入 {#ingestion}

Adobe Experience Platform Data Ingestion表示Experience Platform从各种来源摄取数据的多种方法，以及该数据如何在Data Lake中保留以供下游Experience Platform服务使用。

**新增功能**

| 功能 | 描述 |
|------- | -----------|
| 使用批量摄取更新插入或修补配置文件记录 | Real-Time Customer Profile现在允许通过批量摄取更新单个配置文件记录数据中的配置文件属性。 有关详细信息，请参阅[批量摄取开发人员指南](../../ingestion/batch-ingestion/api-overview.md)。 |

要了解有关将数据摄取到Experience Platform的更多信息，请访问[数据摄取文档](../../ingestion/home.md)。

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep]允许数据工程师映射、转换和验证与Experience Data Model (XDM)之间的数据。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 支持流数据流 | 现在，在为[!DNL Amazon Kinesis]、[!DNL Azure Event Hubs]和[!DNL Google PubSub]创建流数据流时，您可以使用数据准备功能。 有关详细信息，请参阅有关[为云存储源](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)创建流数据流的教程。 |

要了解有关[!DNL Data Prep]的更多信息，请参阅[[!DNL Data Prep] 概述](../../data-prep/home.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Experience Platform服务来构建、标记和增强这些数据。 您可以从各种来源获取数据，例如 Adobe 应用程序、基于云的存储、第三方软件和 CRM 系统。

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

| 功能 | 描述 |
| --- | --- |
| [!DNL Data Landing Zone] | 您现在可以使用[[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md)或[用户界面](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md)创建[!DNL Data Landing Zone]源连接。 [!DNL Data Landing Zone]是由Experience Platform设置的[!DNL Azure Blob]存储接口，允许您访问安全的基于云的文件存储设施，以将文件导入Experience Platform。 有关详细信息，请参阅[[!DNL Data Landing Zone] 概述](../../sources/connectors/cloud-storage/data-landing-zone.md)。 |
| [!DNL Snowflake] | 您现在可以使用[[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md)或[用户界面](../../sources/tutorials/ui/create/databases/snowflake.md)创建[!DNL Snowflake]源连接，将数据从[!DNL Snowflake]数据库引入Experience Platform。 有关详细信息，请参阅[[!DNL Snowflake] 概述](../../sources/connectors/databases/snowflake.md)。 |
| [!DNL SFTP]源增强功能 | 您可以在创建[!DNL SFTP]源连接时手动设置自定义端口号。 有关详细信息，请参阅[[!DNL SFTP] 概述](../../sources/connectors/cloud-storage/sftp.md)。 |

要了解有关源的更多信息，请参阅[源概述](../../sources/home.md)。
