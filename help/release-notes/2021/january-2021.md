---
title: Adobe Experience Platform 发行说明
description: Experience Platform发行说明2021年1月27日
doc-type: release notes
last-update: January 27, 2021
author: ens60013
translation-type: tm+mt
source-git-commit: 2e3a6acbfaa7f733a9843068c00f31f0b7f535b6
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 7%

---


# Adobe Experience Platform 发行说明

**发行日期：2021 年 1 月 27 日**

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允许数据工程师在体验数据模型(XDM)之间映射、转换和验证数据。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 常规表达式函数 | [!DNL Data Prep] 映射器现在支持基于常规表达式匹配和提取部分输入字段。 |

有关详细信息，请参阅[[!DNL Data Prep] 概述](../../data-prep/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预建的与目标平台的集成，允许从Adobe Experience Platform无缝激活数据。您可以使用目标来激活已知和未知的跨渠道营销活动、电子邮件活动、定向广告和许多其他用例数据。

**新目标**

| 目标 | 描述 |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] 是微软的云对象存储解决方案。 |

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 高级ID匹配 | 通过增加对外部ID、电话号码和移动设备ID等其他身份匹配的支持，增强了[!DNL Facebook Custom Audiences]和[!DNL Google Customer Match]中的受众匹配率功能。 有关更多详细信息，请参阅以下文档： <ul><li>[Facebook目标](../../destinations/catalog/social/facebook.md)</li><li>[Google客户匹配目标](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[将用户档案和区段激活到目标](../../destinations/ui/activate-destinations.md)</li></ul> |

要了解更多信息，请访问[目标概述](../../destinations/home.md)。

## [!DNL Sources] {#sources}

Adobe Experience Platform可以从外部来源收集数据，同时允许您使用平台服务来构建、标记和增强这些数据。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)收集数据。

Experience Platform提供RESTful API和交互式UI，使您能轻松为各种数据提供者设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置获取运行的时间，以及管理数据获取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| Adobe Audience Manager源连接器增强 | 您现在可以过滤和选择从Audience Manager到引入平台的各个第一方区段，并过滤掉第一方特征。 有关详细信息，请参阅关于[创建Audience Manager源连接器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)的教程。 |
| [!DNL Google BigQuery] 源连接器增强功能 | 您现在可以使用[!DNL BigQuery]源连接器在一个流运行中摄取大于10GB的文件。 有关详细信息，请参阅[[!DNL BigQuery] 源连接器概述](../../sources/connectors/databases/bigquery.md)。 |
| 支持云存储的复杂数据类型 | 现在，在使用云存储源连接器时，您可以收集复杂数据类型，如JSON文件中的数组。 有关详细信息，请参阅有关在UI](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)或[中使用 [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md)创建云存储数据流[的教程。 |
| 支持[!DNL Microsoft Dynamics]源的基于服务主体密钥的身份验证 | 您现在可以使用服务主体密钥作为基于密码的身份验证的替代方法，对您的[!DNL Dynamics]帐户进行身份验证。 有关详细信息，请参阅[[!DNL Dynamics] 源连接器概述](../../sources/connectors/crm/ms-dynamics.md)。 |
| 对云存储源中自定义分隔符的UI支持 | 您现在可以设置自定义列分隔符，如逗号(`,`)、制表符(`\t`)或管道(`|`)，以在UI中收集分隔的文件。 有关详细信息，请参阅[使用云存储源连接器](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md)创建数据流的教程 |

要进一步了解源，请参阅[源概述](../../sources/home.md)。
