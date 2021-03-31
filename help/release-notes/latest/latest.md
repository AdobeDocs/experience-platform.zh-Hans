---
title: Adobe Experience Platform 发行说明
description: Experience Platform 2021年3月31日发行说明。
doc-type: release notes
last-update: March 31, 2021
author: ens70167
translation-type: tm+mt
source-git-commit: 9b4395d423bbc62c8a1a9427ea91248a0f693794
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 7%

---


# Adobe Experience Platform 发行说明

**发布日期：2021 年 3 月 31 日**

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允许数据工程师在体验数据模型(XDM)之间映射、转换和验证数据。

| 功能 | 描述 |
| ------- | ----------- |
| `add_to_array` 函数 | 更新了功能，支持将数组用作参数。 |
| `to_array` 函数 | 更新了功能，支持将对象用作参数。 |

有关详细信息，请参阅[[!DNL Data Prep] 概述](../../data-prep/home.md)。

## Segmentation Service {#segmentation}

Adobe Experience Platform Segmentation Service提供用户界面和RESTful API，使您能够根据[!DNL Real-time Customer Profile]数据构建区段和生成受众。 这些区段在[!DNL Platform]上集中配置和维护，使任何Adobe应用程序都可轻松访问它们。

[!DNL Segmentation Service] 通过描述区分客户群中可销售人群的标准，定义特定的用户档案子集。细分可以基于记录数据（如人口统计信息）或表示客户与您品牌互动的时间序列事件。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| （测试版）边缘分割 | 边缘细分可实时评估细分，允许使用相同的页面和下一页个性化用例。 有关边缘分段的详细信息，请参阅[分段UI概述](../../segmentation/ui/overview.md)。 |
| （测试版）增量细分 | 将批细分中评估的现有区段定义的新鲜度提高到最多一小时。 |

有关[!DNL Segmentation Service]的详细信息，请参阅[分段概述](../../segmentation/home.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源收集数据，同时允许您使用平台服务构建、标记和增强该数据。 您可以从各种来源收集数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松为各种数据提供者设置源连接。 这些源连接允许您对外部存储系统和CRM服务进行身份验证并连接，设置获取运行的时间，以及管理数据获取吞吐量。

| 功能 | 描述 |
| ------- | ----------- |
| 测试版源迁移至GA | 以下源已从测试版提升为GA: <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| 对压缩文件摄取的API支持 | 您现在可以使用云预览源存储和摄取压缩的JSON或分隔文件。 有关详细信息，请参阅教程，其中介绍使用API](../../sources/tutorials/api/collect/cloud-storage.md)收集云存储数据。[ |
| 递归文件上传的UI支持 | 现在，使用云存储源时，您可以递归收录整个文件夹。 在摄取整个文件夹时，必须确保其内容共享相同的模式。 有关详细信息，请参阅教程，其中介绍在UI](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)中为云存储连接器配置数据流。[ |

要了解有关源的详细信息，请参阅[源概述](../../sources/home.md)。
