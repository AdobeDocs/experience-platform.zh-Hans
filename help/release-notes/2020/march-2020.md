---
title: Adobe Experience Platform发行说明2020年3月
description: Adobe Experience Platform 2020年3月版发行说明。
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: 发行说明;
exl-id: 407c2bac-4c8a-4939-b3dd-788250f15650
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发布日期：2020 年 3 月 11 日**

Adobe Experience Platform 现有功能的更新包括：

* [数据治理](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## 数据治理 {#governance}

[!DNL Experience Platform] 允许公司将来自多个企业系统的数据汇集在一起，以便更好地让营销人员识别、了解和吸引客户。 [!DNL Experience Platform] 包括一个端到端的数据治理基础架构，以确保数据在 [!DNL Platform] 在系统之间共享时。

Adobe Experience Platform数据管理是用于管理客户数据并确保遵守适用于数据使用的法规、限制和策略的一系列策略和技术。 它在以下方面发挥着关键作用 [!DNL Experience Platform] 在不同的级别，包括编目、数据谱系、数据使用标签、数据访问策略和对营销活动数据的访问控制。

**新增功能**

>[!NOTE]
>
>以下某些新功能目前处于测试阶段，并非对所有用户都可用。 Beta版功能可能会发生更改。

| 功能 | 描述 |
| ------- | ----------- |
| 自动强制实施的数据使用策略 [!DNL Real-Time Customer Data Platform] | 现在，在将数据激活到目标的工作流中强制执行数据使用策略。 在进行影响现有激活的更改（例如更改数据集标签、合并策略、区段定义等）时，也会嵌入并强制执行数据管理。 |
| 用于强制实施的数据谱系 | 在Real-Time CDP中违反数据使用策略时，UI会显示一个包含数据谱系信息的通知，以帮助用户了解违反策略的原因以及他们可以采取哪些措施来解决违规。 |


**已知问题**

* None

有关“数据管理”的更多信息，请参阅 [数据治理概述](../../data-governance/home.md).

## 数据引入 {#ingestion}

Adobe Experience Platform提供了一组丰富的功能，可用于摄取任何类型和延迟的数据。 Adobe Experience Platform [!DNL Data Ingestion] 为摄取数据提供了多个替代方案，包括批处理API、流API、本机Adobe连接器、数据集成合作伙伴或Adobe Experience Platform UI。

**新增功能**

| 功能 | 描述 |
|------- | -----------|
| 部分批次摄取 | 部分批量摄取是指在一定阈值内摄取包含错误的数据的能力。 借助此功能，用户可以成功地将其所有正确数据摄取到Adobe Experience Platform中，同时对其所有不正确的数据进行单独批处理。 详细信息将添加到不成功的批次，以解释它们未通过验证的原因。 有关部分批量摄取的更多信息，请参阅 [部分批量摄取文档](../../ingestion/batch-ingestion/partial.md). |

**已知问题**

* None

要了解有关将数据摄取到Platform的更多信息，请访问 [数据引入文档](../../ingestion/home.md).


## 目标 {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md)，目标是预先构建的与目标平台的集成，可无缝地向这些合作伙伴激活数据。

**新目标**

提供了一些新目标，您可以在其中激活Adobe Experience Platform数据。 有关详细信息，请参阅下文：

| 目标 | 描述 |
|--- | ---|
| 云存储目标 | Real-Time CDP现在可以将区段作为数据文件交付到 [!DNL Amazon S3] 或SFTP云存储位置。 这使您能够通过CSV或制表符分隔文件将受众及其配置文件属性发送到内部系统。 |
| 广告目标 | 此 [!DNL Google] 对于三个不同的目标卡，目标卡现在拆分为三个目标卡 [!DNL Google] Real-Time CDP中当前支持的平台： [!DNL Google Ads]， [!DNL Google Ad Manager]， [!DNL Google] 显示和视频360。 |

要了解更多信息，请访问 [目标概述](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

提供相关的数字体验需要全面了解您的客户。 当您的客户数据分散在不同的系统上，导致每个客户似乎都有多个“身份”时，就会使这一点变得更加困难。

Adobe Experience Platform [!DNL Identity Service] 通过跨设备和系统桥接身份，允许您实时提供有影响力的个人数字体验，帮助您更好地了解客户及其行为。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 增强专用图 | 专用图形功能已得到增强，可减少图形生成延迟，从每周批处理流程缩短为每日更新的图形，从而允许 [!DNL Identity Service] 客户访问更多最新的标识图和链接。 |

**已知问题**

* None

有关详情，请参阅 [!DNL Identity Service]，请参见 [Identity服务概述](../../identity-service/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用来构建、标记和增强这些数据 [!DNL Platform] 服务。 您可以从各种来源(如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统)中摄取数据。

[!DNL Experience Platform] 提供了一个RESTful API和一个交互式UI，可让您轻松为各种数据提供程序设置源连接。 这些源连接允许您进行身份验证并连接到外部存储系统和CRM服务，设置引入运行的时间，以及管理数据引入吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| Adobe Audience Manager连接器的已弃用信号 | 将不再发送来自Audience Manger的信号级数据。 请注意，特征和区段的区段成员资格仍会包括在内。 由于此更改，将不再生成集客数据集。 |
| 重命名的数据集 | Audience Manger连接器生成的数据集将具有更新的名称和描述。 |
| 启用 [!DNL Profile] 在Audience Manger中切换 | [!DNL Profile] 可以启用或禁用切换以将数据集提升到 [!DNL Real-Time Customer Profile]. 默认情况下将启用切换功能。 |
| 云存储系统的UI支持 | 新的源连接器 [!DNL Azure Data Lake Storage Gen2] 在UI中。 |
| CRM系统的UI支持 | 新的源连接器 [!DNL HubSpot]， [!DNL Salesforce Service Cloud]、和 [!DNL ServiceNow] 在UI中。 |
| 数据库系统的UI支持 | 新的源连接器 [!DNL AWS Redshift]， [!DNL Google BigQuery]， [!DNL MariaDB]， [!DNL Microsoft SQL Server]、和 [!DNL MySQL] 在UI中。 |

**已知问题**

* None

要了解有关源的更多信息，请参阅 [源概述](../../sources/home.md).
