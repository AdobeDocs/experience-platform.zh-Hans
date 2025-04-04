---
title: Adobe Experience Platform 发行说明（2021 年 3 月）
description: Adobe Experience Platform 的 2021 年 3 月发行说明。
doc-type: release notes
last-update: March 31, 2021
author: ens72741
exl-id: 027cd7b1-1651-4939-bc97-968a41824117
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 37%

---

# Adobe Experience Platform 发行说明

**发行日期： 2021年3月31日**

Adobe Experience Platform 中现有功能的更新：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep]允许数据工程师映射、转换和验证与Experience Data Model (XDM)之间的数据。

| 功能 | 描述 |
| ------- | ----------- |
| `add_to_array`函数 | 更新了支持将数组作为参数的功能。 |
| `to_array`函数 | 更新了支持将对象作为参数的功能。 |

有关详细信息，请参阅[[!DNL Data Prep] 概述](../../data-prep/home.md)。

## Segmentation Service {#segmentation}

Adobe Experience Platform Segmentation Service提供了一个用户界面和RESTful API，允许您根据[!DNL Real-Time Customer Profile]数据构建区段并生成受众。 这些区段是在[!DNL Experience Platform]上集中配置和维护的，因此任何Adobe应用程序都可以轻松访问它们。

[!DNL Segmentation Service] 通过描述在您的客户群中区分适销人群的标准，来定义特定的轮廓子集。区段可以基于记录数据（例如人口统计信息）或代表客户与您的品牌互动的时间序列事件。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| (Beta) Edge分段 | Edge分段会实时评估区段，以允许对同一页面和下一页面进行个性化使用案例。 有关边缘分段的更多信息，请参阅[分段UI概述](../../segmentation/ui/overview.md)。 |
| (Beta)增量分段 | 将在批量分段中评估的现有区段定义的时效性提高到一小时。 |

有关 [!DNL Segmentation Service] 的详细信息，请查看[分段概述](../../segmentation/home.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Experience Platform服务来构建、标记和增强这些数据。 您可以从各种来源获取数据，例如 Adobe 应用程序、基于云的存储、第三方软件和 CRM 系统。

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

| 功能 | 描述 |
| ------- | ----------- |
| Beta源迁移到GA | 以下源已从Beta版升级到GA版： <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| API支持压缩文件摄取 | 您现在可以使用云存储源预览和摄取压缩的JSON或分隔文件。 有关详细信息，请参阅关于使用API [收集云存储数据的教程](../../sources/tutorials/api/collect/cloud-storage.md)。 |
| 递归文件上传的UI支持 | 使用云存储源时，您现在可以递归摄取整个文件夹。 摄取整个文件夹时，必须确保其内容共享相同的架构。 有关详细信息，请参阅有关[在UI](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)中为云存储连接器配置数据流的教程。 |

要了解有关源的更多信息，请参阅[源概述](../../sources/home.md)。
