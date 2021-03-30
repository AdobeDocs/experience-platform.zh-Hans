---
title: Adobe Experience Platform 发行说明
description: Experience Platform 2021年3月31日发行说明。
doc-type: release notes
last-update: March 31, 2021
author: ens72741
translation-type: tm+mt
source-git-commit: 8d4270d9168a570fcf92ba60d70dbc8e9af98136
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 9%

---


# Adobe Experience Platform 发行说明

**发行日期：2021 年 3 月 31 日**

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Sources]](#sources)

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源收集数据，同时允许您使用平台服务构建、标记和增强该数据。 您可以从各种来源收集数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松为各种数据提供者设置源连接。 这些源连接允许您对外部存储系统和CRM服务进行身份验证并连接，设置获取运行的时间，以及管理数据获取吞吐量。

2021年3月版的Experience Platform中包含以下源更新：

| 功能 | 描述 |
| ------- | ----------- |
| 测试版源迁移至GA | 以下源已从测试版提升为GA: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| 对压缩文件摄取的API支持 | 您现在可以使用云预览源存储和摄取压缩的JSON或分隔文件。 有关详细信息，请参阅教程，其中介绍使用API](../../sources/tutorials/api/collect/cloud-storage.md)收集云存储数据。[ |
| 递归文件上传的UI支持 | 现在，使用云存储源时，您可以递归收录整个文件夹。 在摄取整个文件夹时，必须确保其内容共享相同的模式。 有关详细信息，请参阅教程，其中介绍在UI](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)中为云存储连接器配置数据流。[ |

要了解有关源的详细信息，请参阅[源概述](../../sources/home.md)。
