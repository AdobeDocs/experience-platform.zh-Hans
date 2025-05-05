---
title: Adobe Experience Platform 发行说明（2021 年 1 月）
description: Adobe Experience Platform 的 2021 年 1 月发行说明。
doc-type: release notes
last-update: January 27, 2021
author: ens60013
exl-id: 6fb92e35-922c-47ba-8cf4-44edd92acfa1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 27%

---

# Adobe Experience Platform 发行说明

**发行日期： 2021年1月27日**

Adobe Experience Platform 中现有功能的更新：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep]允许数据工程师映射、转换和验证与Experience Data Model (XDM)之间的数据。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 正则表达式函数 | [!DNL Data Prep]映射器现在支持基于正则表达式匹配和提取部分输入字段。 |

有关详细信息，请参阅[[!DNL Data Prep] 概述](../../data-prep/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预先构建的与目标平台的集成，可实现从 Adobe Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件宣传、定向广告和许多其他用例。

**新目标**

| 目标 | 描述 |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob]是Microsoft的云对象存储解决方案。 |

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 高级标识匹配 | 通过添加对其他身份匹配（如外部ID、电话号码和移动设备ID）的支持，增强了[!DNL Facebook Custom Audiences]和[!DNL Google Customer Match]中的受众匹配率功能。 有关更多详细信息，请参阅以下文档： <ul><li>[Facebook目标](../../destinations/catalog/social/facebook.md)</li><li>[Google客户匹配目标](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[将受众数据激活到流式区段导出目标](../../destinations/ui/activate-segment-streaming-destinations.md)</li></ul> |

要了解更多信息，请访问[目标概述](../../destinations/home.md)。

## 实时客户轮廓 {#profile}

Adobe Experience Platform 使您能够为客户提供协调、一致且相关的体验，无论他们何时何地与您的品牌互动均是如此。利用实时客户轮廓，您可以看到每个客户的整体视图，其中结合来自多个渠道的数据，包括在线、离线、CRM 和第三方数据。[!DNL Profile]允许您将客户数据整合到一个统一视图中，并提供每个客户交互的带时间戳的可操作帐户。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 从配置文件存储中删除数据集 | 当您从Experience Platform数据湖中删除数据集时，它也会自动从配置文件存储中删除。 您不再需要使用配置文件系统作业API端点发出删除请求，以显式从配置文件存储中删除数据集。 有关详细信息，请参阅[配置文件系统作业API终结点指南](../../profile/api/profile-system-jobs.md)。 |
| 给定区段的预计ID命名空间计数 | 对于预计的用户档案计数，预览API现在报告：<ul><li>给定命名空间中区段内的预计配置文件总数。</li><li>给定命名空间的配置文件合并架构中估计的总配置文件数。</li></ul>有关详细信息，请参阅[配置文件预览API端点指南](../../profile/api/preview-sample-status.md)。 |

有关实时客户个人资料的更多信息，包括用于使用[!DNL Profile]数据的教程和最佳实践，请从阅读[实时客户个人资料概述](../../profile/home.md)开始。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Experience Platform服务来构建、标记和增强这些数据。 您可以从各种源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| Adobe Audience Manager源连接器增强功能 | 您现在可以从Audience Manager中筛选和选择单个第一方区段以摄取到Experience Platform中，并筛选掉第一方特征。 有关详细信息，请参阅有关[创建Audience Manager源连接器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)的教程。 |
| [!DNL Google BigQuery]源连接器增强功能 | 您现在可以使用[!DNL BigQuery]源连接器在一次流运行中摄取大于10GB的文件。 有关详细信息，请参阅[[!DNL BigQuery] 源连接器概述](../../sources/connectors/databases/bigquery.md)。 |
| 支持云存储的复杂数据类型 | 使用云存储源连接器时，您现在可以摄取复杂的数据类型，例如JSON文件中的数组。 有关详细信息，请参阅有关在UI[&#128279;](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)中创建云存储数据流[或使用 [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md)创建的教程。 |
| 支持[!DNL Microsoft Dynamics]源的基于服务主体密钥的身份验证 | 您现在可以使用服务主体密钥对您的[!DNL Dynamics]帐户进行身份验证，作为基于密码的身份验证的替代方法。 有关详细信息，请参阅[[!DNL Dynamics] 源连接器概述](../../sources/connectors/crm/ms-dynamics.md)。 |
| 云存储源中对自定义分隔符的UI支持 | 您现在可以设置自定义列分隔符，如逗号(`,`)、制表符(`\t`)或管道字符(`|`)，以在UI中收集分隔的文件。 有关详细信息，请参阅有关[使用云存储源连接器](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)创建数据流的教程 |

要了解有关源的更多信息，请参阅[源概述](../../sources/home.md)。
