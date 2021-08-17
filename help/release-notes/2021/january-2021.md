---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2021年1月27日
doc-type: release notes
last-update: January 27, 2021
author: ens60013
exl-id: 6fb92e35-922c-47ba-8cf4-44edd92acfa1
source-git-commit: 02c22453470d55236d4235c479742997e8407ef3
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发行日期：2021 年 1 月 27 日**

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允许数据工程师在体验数据模型(XDM)之间映射、转换和验证数据。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 正则表达式函数 | [!DNL Data Prep] 映射器现在支持基于正则表达式匹配和提取部分输入字段。 |

有关详细信息，请参阅[[!DNL Data Prep] 概述](../../data-prep/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是与目标平台的预建集成，可无缝激活来自Adobe Experience Platform的数据。您可以使用目标来激活跨渠道营销活动、电子邮件促销活动、定向广告和许多其他用例的已知和未知数据。

**新目标**

| 目标 | 描述 |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] 是Microsoft的云对象存储解决方案。 |

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 高级ID匹配 | 通过添加对其他身份匹配（如外部ID、电话号码和移动设备ID）的支持，增强了[!DNL Facebook Custom Audiences]和[!DNL Google Customer Match]中的受众匹配率功能。 有关更多详细信息，请参阅以下文档： <ul><li>[Facebook目标](../../destinations/catalog/social/facebook.md)</li><li>[Google客户匹配目标](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[将受众数据激活到流区段导出目标](../../destinations/ui/activate-segment-streaming-destinations.md)</li></ul> |

要了解更多信息，请访问[目标概述](../../destinations/home.md)。

## Real-time Customer Profile {#profile}

Adobe Experience Platform使您能够为客户在何处或何时与您的品牌进行交互，从而提供协调、一致的相关体验。 通过实时客户资料，您可以查看每个客户的整体视图，该视图将来自多个渠道的数据（包括在线、离线、CRM和第三方数据）进行整合。 [!DNL Profile] 允许您将客户数据整合到统一视图中，为每次客户交互提供一个可操作且带有时间戳的帐户。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 从配置文件存储中删除数据集 | 从Experience Platform数据湖中删除数据集时，该数据集也会自动从用户档案存储中删除。 您不再需要使用配置文件系统作业API端点发出删除请求，以便明确地从配置文件存储中删除数据集。 有关更多信息，请参阅[配置文件系统作业API端点指南](../../profile/api/profile-system-jobs.md)。 |
| 给定区段的估计ID命名空间计数 | 对于预计的配置文件计数，预览API现在会报告：<ul><li>给定命名空间的区段中预计用户档案的总数。</li><li>给定命名空间的配置文件合并架构中预计配置文件的总数。</li></ul>要了解更多信息，请参阅[配置文件预览API端点指南](../../profile/api/preview-sample-status.md)。 |

有关实时客户资料的更多信息，包括有关使用[!DNL Profile]数据的教程和最佳实践，请首先阅读[实时客户资料概述](../../profile/home.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| Adobe Audience Manager源连接器增强功能 | 您现在可以从Audience Manager中筛选和选择单个第一方区段，以将其摄取到Platform中，以及过滤掉第一方特征。 有关更多信息，请参阅有关[创建Audience Manager源连接器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)的教程。 |
| [!DNL Google BigQuery] 源连接器增强功能 | 现在，您可以使用[!DNL BigQuery]源连接器在一个流运行中摄取大于10GB的文件。 有关更多信息，请参阅[[!DNL BigQuery] 源连接器概述](../../sources/connectors/databases/bigquery.md) 。 |
| 支持云存储的复杂数据类型 | 现在，在使用云存储源连接器时，您可以摄取复杂的数据类型，例如JSON文件中的数组。 有关更多信息，请参阅有关在UI](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)或[中使用 [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md)创建云存储数据流[的教程。 |
| 支持[!DNL Microsoft Dynamics]源基于服务主体密钥的身份验证 | 现在，您可以使用服务主体密钥作为基于密码的身份验证的替代方法，对[!DNL Dynamics]帐户进行身份验证。 有关更多信息，请参阅[[!DNL Dynamics] 源连接器概述](../../sources/connectors/crm/ms-dynamics.md) 。 |
| 云存储源中自定义分隔符的UI支持 | 现在，您可以设置自定义列分隔符(如逗号(`,`)、制表符(`\t`)或管道字符(`|`))，以在UI中收集分隔文件。 有关更多信息，请参阅有关[使用云存储源连接器创建数据流的教程](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) |

要了解有关源的更多信息，请参阅[源概述](../../sources/home.md)。
