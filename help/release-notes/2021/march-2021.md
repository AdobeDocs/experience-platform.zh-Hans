---
title: Adobe Experience Platform 发行说明
description: Experience Platform 2021年3月31日发行说明。
doc-type: release notes
last-update: March 31, 2021
author: ens72741
translation-type: tm+mt
source-git-commit: 58382528cc787e8d2005c8c322904266880ad0b9
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 6%

---


# Adobe Experience Platform 发行说明

**发布日期：2021 年 3 月 31 日**

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Sandboxes]](#sandboxes)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允许数据工程师在体验数据模型(XDM)之间映射、转换和验证数据。

| 功能 | 描述 |
| ------- | ----------- |
| `add_to_array` 函数 | 更新了功能，支持将数组用作参数。 |
| `to_array` 函数 | 更新了功能，支持将对象用作参数。 |

有关详细信息，请参阅[[!DNL Data Prep] 概述](../../data-prep/home.md)。

## [!DNL Sandboxes] {#sandboxes}

Adobe Experience Platform旨在在全球范围内丰富数字体验应用程序。 公司经常并行运行多个数字体验应用程序，需要满足这些应用程序的开发、测试和部署的需要，同时确保操作合规性。

为了满足这一需求，Experience Platform提供了沙箱，可将单个平台实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

| 功能 | 描述 |
| ------- | ----------- |
| （测试版）多个制作沙箱 | 您现在可以在IMS组织中创建和管理多个制作沙箱，并将特定制作沙箱专门用于不同的业务线、品牌、项目或地区。 有关详细信息，请参阅有关在UI](../../sandboxes/ui/user-guide.md)或[中使用API](../../sandboxes/api/create-sandbox.md)创建生产沙箱[的教程。 |

有关沙箱的详细信息，请参阅[沙箱概述](../../sandboxes/home.md)。

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
