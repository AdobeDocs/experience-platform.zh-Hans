---
title: Adobe Experience Platform发行说明2021年3月
description: 2021年3月版Adobe Experience Platform发行说明。
doc-type: release notes
last-update: March 31, 2021
author: ens72741
exl-id: 027cd7b1-1651-4939-bc97-968a41824117
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 6%

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
| `add_to_array` 函数 | 更新了支持将数组作为参数的功能。 |
| `to_array` 函数 | 更新了支持将对象作为参数的功能。 |

有关详细信息，请参阅 [[!DNL Data Prep] 概述](../../data-prep/home.md).

## 分段服务 {#segmentation}

Adobe Experience Platform Segmentation Service提供了用户界面和RESTful API，允许您从 [!DNL Real-time Customer Profile] 数据。 这些区段在上集中配置和维护 [!DNL Platform]，以便任何Adobe应用程序都可轻松访问。

[!DNL Segmentation Service] 通过描述区分客户群中可销售人群的标准来定义特定的用户档案子集。 区段可以基于记录数据（如人口统计信息）或表示客户与您的品牌交互的时间序列事件。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| （测试版）边缘分段 | 边缘区段可实时评估区段，以便支持同一页面和下一页个性化用例。 有关边缘分割的更多信息，请参阅 [分段UI概述](../../segmentation/ui/overview.md). |
| （测试版）增量分段 | 将批量分段中评估的现有区段定义的新鲜度增加到多达一小时。 |

有关 [!DNL Segmentation Service]，请参阅 [分段概述](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

| 功能 | 描述 |
| ------- | ----------- |
| 测试版源迁移至GA | 以下来源已从测试版提升为正式发布： <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| 支持压缩文件摄取的API | 您现在可以使用云存储源预览和摄取压缩的JSON或分隔文件。 有关更多信息，请参阅 [使用API收集云存储数据](../../sources/tutorials/api/collect/cloud-storage.md). |
| UI支持递归文件上传 | 现在，在使用云存储源时，您可以递归摄取整个文件夹。 摄取整个文件夹时，必须确保其内容共享相同的架构。 有关更多信息，请参阅 [在UI中为云存储连接器配置数据流](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

要进一步了解源，请参阅 [源概述](../../sources/home.md).
