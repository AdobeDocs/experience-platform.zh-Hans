---
title: Adobe Experience Platform发行说明2021年1月
description: Adobe Experience Platform 2021年1月版发行说明。
doc-type: release notes
last-update: January 27, 2021
author: ens60013
exl-id: 6fb92e35-922c-47ba-8cf4-44edd92acfa1
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 5%

---

# Adobe Experience Platform 发行说明

**发行日期：2021 年 1 月 27 日**

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允许数据工程师映射、转换和验证数据到/传出体验数据模型(XDM)。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 正则表达式函数 | [!DNL Data Prep] 映射器现在支持基于正则表达式匹配和提取部分输入字段。 |

欲知更多信息，请参见 [[!DNL Data Prep] 概述](../../data-prep/home.md).

## 目标 {#destinations}

[!DNL Destinations] 是与目标平台预建的集成，允许从Adobe Experience Platform无缝激活数据。 您可以使用目标为跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例激活已知和未知数据。

**新目标**

| 目标 | 描述 |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] 是Microsoft的云对象存储解决方案。 |

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 高级标识匹配 | 中的受众匹配率功能增强 [!DNL Facebook Custom Audiences] 和 [!DNL Google Customer Match]，方法是添加对其他身份匹配的支持，例如外部ID、电话号码和移动设备ID。 有关更多详细信息，请参阅以下文档： <ul><li>[facebook目标](../../destinations/catalog/social/facebook.md)</li><li>[Google客户匹配目标](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[将受众数据激活到流式区段导出目标](../../destinations/ui/activate-segment-streaming-destinations.md)</li></ul> |

要了解更多信息，请访问 [目标概述](../../destinations/home.md).

## 实时客户资料 {#profile}

通过Adobe Experience Platform，无论客户在何处或何时与您的品牌互动，您都可以为其推动协调、一致且相关的体验。 利用实时客户档案，您可以查看合并了来自多个渠道（包括在线、离线、CRM和第三方数据）的数据的每个单个客户的整体视图。 [!DNL Profile] 允许您将客户数据整合到一个统一的视图中，并提供每个客户交互的带时间戳的可操作帐户。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 从配置文件存储中删除数据集 | 当您从Experience Platform数据湖中删除数据集时，它也会自动从配置文件存储中删除。 您不再需要使用配置文件系统作业API端点发出删除请求，以显式从配置文件存储中删除数据集。 欲了解更多信息，请参见 [配置文件系统作业API端点指南](../../profile/api/profile-system-jobs.md). |
| 给定区段的预计ID命名空间计数 | 对于预计的配置文件计数，预览API现在会报告：<ul><li>给定命名空间的区段中的估计配置文件总数。</li><li>给定命名空间的配置文件合并架构中估计的配置文件总数。</li></ul>要了解更多信息，请参阅 [配置文件预览API端点指南](../../profile/api/preview-sample-status.md). |

有关Real-Time Customer Profile的更多信息，包括有关使用的教程和最佳实践 [!DNL Profile] 数据，请首先阅读 [Real-time Customer Profile概述](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强这些数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)中摄取数据。

Experience Platform提供RESTful API和交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您进行身份验证并连接到外部存储系统和CRM服务，设置引入运行的时间，以及管理数据引入吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| Adobe Audience Manager源连接器增强功能 | 您现在可以从Audience Manager中筛选和选择单个第一方区段以摄取到Platform中，并筛选掉第一方特征。 请参阅上的教程 [创建Audience Manager源连接器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) 了解更多信息。 |
| [!DNL Google BigQuery] 源连接器增强功能 | 现在，您可以使用在一次流中摄取大于10 GB的文件 [!DNL BigQuery] 源连接器。 请参阅 [[!DNL BigQuery] 源连接器概述](../../sources/connectors/databases/bigquery.md) 了解更多信息。 |
| 支持云存储的复杂数据类型 | 现在，在使用云存储源连接器时，您可以摄取复杂的数据类型，例如JSON文件中的阵列。 请参阅有关创建云存储数据流的教程 [在UI中](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) 或 [使用 [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md) 了解更多信息。 |
| 支持以下项的基于服务主体密钥的身份验证 [!DNL Microsoft Dynamics] 源 | 您现在可以验证您的 [!DNL Dynamics] 使用服务主体密钥作为基于密码的身份验证的替代方案的帐户。 请参阅 [[!DNL Dynamics] 源连接器概述](../../sources/connectors/crm/ms-dynamics.md) 了解更多信息。 |
| 云存储源中的自定义分隔符支持UI | 您现在可以设置自定义列分隔符，如逗号(`,`)，制表符(`\t`)或管道字符(`|`)，以在UI中收集分隔文件。 请参阅上的教程 [使用云存储源连接器创建数据流](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) 了解更多信息 |

要了解有关源的更多信息，请参阅 [源概述](../../sources/home.md).
