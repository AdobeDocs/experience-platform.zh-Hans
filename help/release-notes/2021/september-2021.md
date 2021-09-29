---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform的最新发行说明。
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: b616a0c0d49d980644f82bc3af5995b3b17b4c80
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 10%

---

# Adobe Experience Platform 发行说明

**发布日期：2021 年 9 月 29 日**

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Prep]](#data-prep)
- [源](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允许数据工程师在体验数据模型(XDM)之间映射、转换和验证数据。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 支持流数据流 | 现在，在为[!DNL Amazon Kinesis]、[!DNL Azure Event Hubs]和[!DNL Google PubSub]创建流数据流时，可以使用数据准备函数。 有关更多信息，请参阅有关[为云存储源创建流数据流的教程](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md) 。 |

要了解有关[!DNL Data Prep]的更多信息，请参阅[[!DNL Data Prep] 概述](../../data-prep/home.md)。

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

| 功能 | 描述 |
| --- | --- |
| [!DNL Data Landing Zone] | 现在，您可以使用[[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md)或[用户界面](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md)创建[!DNL Data Landing Zone]源连接。 [!DNL Data Landing Zone] 是由Platform [!DNL Azure Blob] 配置的一个存储界面，它允许您访问基于云的安全文件存储设施，以便在平台中和之外摄取和输出文件。有关更多信息，请参阅[[!DNL Data Landing Zone] 概述](../../sources/connectors/cloud-storage/data-landing-zone.md)。 |
| [!DNL Snowflake] | 现在，您可以使用[[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md)或[用户界面](../../sources/tutorials/ui/create/databases/snowflake.md)创建[!DNL Snowflake]源连接，以将数据从[!DNL Snowflake]数据库引入Platform。 有关更多信息，请参阅[[!DNL Snowflake] 概述](../../sources/connectors/databases/snowflake.md)。 |
| [!DNL SFTP] 源增强功能 | 创建[!DNL SFTP]源连接时，可以手动设置自定义端口号。 有关更多信息，请参阅[[!DNL SFTP] 概述](../../sources/connectors/cloud-storage/sftp.md)。 |

要了解有关源的更多信息，请参阅[源概述](../../sources/home.md)。
