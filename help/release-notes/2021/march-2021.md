---
title: Adobe Experience Platform发行说明2021年3月
description: Adobe Experience Platform 2021年3月版发行说明。
doc-type: release notes
last-update: March 31, 2021
author: ens72741
exl-id: 027cd7b1-1651-4939-bc97-968a41824117
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
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

[!DNL Data Prep] 允许数据工程师映射、转换和验证数据到/传出体验数据模型(XDM)。

| 功能 | 描述 |
| ------- | ----------- |
| `add_to_array` 函数 | 更新了支持将阵列作为参数的功能。 |
| `to_array` 函数 | 更新了支持对象作为参数的功能。 |

欲知更多信息，请参见 [[!DNL Data Prep] 概述](../../data-prep/home.md).

## 分段服务 {#segmentation}

Adobe Experience Platform Segmentation Service提供了一个用户界面和RESTful API，允许您从构建区段和生成受众。 [!DNL Real-Time Customer Profile] 数据。 这些区段集中配置并维护于 [!DNL Platform]，便于任何Adobe应用程序访问。

[!DNL Segmentation Service] 通过描述用于区分客户群内可销售人员组的标准，来定义用户档案的特定子集。 区段可以基于记录数据（例如人口统计信息）或表示客户与您的品牌互动的时间系列事件。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| (Beta)边缘分段 | Edge分段会实时评估区段，从而允许使用同一页面和下一页面个性化用例。 有关边缘分段的更多信息，请参阅 [分段UI概述](../../segmentation/ui/overview.md). |
| (Beta)增量分段 | 将在批量分段中评估的现有区段定义的时效性提高到一小时。 |

有关的详细信息 [!DNL Segmentation Service]，请参阅 [分段概述](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强这些数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)中摄取数据。

Experience Platform提供RESTful API和交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您进行身份验证并连接到外部存储系统和CRM服务，设置引入运行的时间，以及管理数据引入吞吐量。

| 功能 | 描述 |
| ------- | ----------- |
| Beta版源迁移至GA | 以下源已从Beta版升级到GA版： <ul><li>[[!DNL MySQL]](../../sources/connectors/databases/mysql.md)</li><li>[[!DNL PostGres]](../../sources/connectors/databases/postgres.md)</li><li>[[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md)</li><li>[[!DNL SFTP]](../../sources/connectors/cloud-storage/sftp.md)</li><li>[[!DNL Shopify]](../../sources/connectors/ecommerce/shopify.md)</li></ul> |
| 对压缩文件提取的API支持 | 您现在可以使用云存储源预览和摄取压缩的JSON或分隔文件。 有关更多信息，请参阅以下教程： [使用API收集云存储数据](../../sources/tutorials/api/collect/cloud-storage.md). |
| 递归文件上传的UI支持 | 您现在可以在使用云存储源时递归摄取整个文件夹。 摄取整个文件夹时，必须确保其内容共享相同的架构。 有关更多信息，请参阅以下教程： [在UI中为云存储连接器配置数据流](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

要了解有关源的更多信息，请参阅 [源概述](../../sources/home.md).
