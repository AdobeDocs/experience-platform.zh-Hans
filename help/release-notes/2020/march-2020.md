---
title: Adobe Experience Platform发行说明2020年3月
description: 2020年3月版Adobe Experience Platform发行说明。
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

[!DNL Experience Platform] 允许公司将多个企业系统中的数据整合在一起，以便营销人员能够更好地识别、了解和吸引客户。 [!DNL Experience Platform] 包括端到端数据管理基础架构，以确保在 [!DNL Platform] 和在系统之间共享时。

Adobe Experience Platform数据管理是用于管理客户数据并确保符合适用于数据使用的法规、限制和策略的一系列策略和技术。 它在 [!DNL Experience Platform] 在不同级别，包括编目、数据谱系、数据使用标签、数据访问策略以及对营销操作数据的访问控制。

**新增功能**

>[!NOTE]
>
>以下一些新功能目前处于测试阶段，并且并非所有用户都能使用。 测试版功能可能会发生更改。

| 功能 | 描述 |
| ------- | ----------- |
| 自动执行 [!DNL Real-Time Customer Data Platform] | 现在，在将数据激活到目标的工作流中强制实施数据使用策略。 在进行影响现有激活的更改（例如更改数据集标签、合并策略、区段定义等）时，也会嵌入并强制执行“数据管理”。 |
| 用于执行的数据谱系 | 在Real-Time CDP中违反数据使用策略时，UI会显示一则通知，其中包含数据谱系信息，以帮助用户了解违反策略的原因以及他们可以执行哪些操作来解决违规。 |


**已知问题**

* None

有关“数据管理”的更多信息，请参阅 [数据管理概述](../../data-governance/home.md).

## 数据引入 {#ingestion}

Adobe Experience Platform提供丰富的功能集，用于摄取任何类型的数据和延迟。 Adobe Experience Platform [!DNL Data Ingestion] 提供了多个用于摄取数据的替代方法，包括批量API、流API、本机Adobe连接器、数据集成合作伙伴或Adobe Experience Platform UI。

**新增功能**

| 功能 | 描述 |
|------- | -----------|
| 部分批量摄取 | 部分批量摄取是指摄取包含错误的数据（最高可达特定阈值）的功能。 利用此功能，用户可以成功将其所有正确数据摄取到Adobe Experience Platform中，同时将其所有错误数据单独批量。 详细信息会添加到不成功的批次中，以解释它们为何未通过验证。 有关部分批量摄取的更多信息，请参阅 [部分批量摄取文档](../../ingestion/batch-ingestion/partial.md). |

**已知问题**

* None

要了解有关将数据摄取到平台的更多信息，请访问 [数据摄取文档](../../ingestion/home.md).


## 目标 {#destinations}

在 [Real-time Customer Data Platform](../../rtcdp/overview.md)，目标是与目标平台的预建集成，可无缝地向这些合作伙伴激活数据。

**新目标**

您可以在新目标中激活Adobe Experience Platform数据。 有关详细信息，请参阅下文：

| 目标 | 描述 |
|--- | ---|
| 云存储目标 | Real-Time CDP现在可以将区段作为数据文件提交到 [!DNL Amazon S3] 或SFTP云存储位置。 这允许您通过CSV或制表符分隔的文件，将受众及其配置文件属性发送到内部系统。 |
| 广告目标 | 的 [!DNL Google] 目标卡现在分为三个目标卡，对于这三个不同的目标卡 [!DNL Google] Real-Time CDP中当前支持的平台： [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google] 显示和视频360。 |

要了解更多信息，请访问 [目标概述](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

提供相关的数字体验需要全面了解您的客户。 当客户数据在不同的系统中分散，导致每个客户似乎都具有多个“身份”时，这会使操作愈发困难。

Adobe Experience Platform [!DNL Identity Service] 通过跨设备和系统桥接身份，使您能够实时提供有影响的个人数字体验，从而帮助您更好地了解客户及其行为。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 增强的专用图 | 专用图功能已得到增强，可减少图形生成延迟，从每周批处理流程缩短为每日刷新的图形，从而允许 [!DNL Identity Service] 客户可访问更多最新身份图和关联。 |

**已知问题**

* None

有关 [!DNL Identity Service]，请参阅 [Identity Service概述](../../identity-service/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用 [!DNL Platform] 服务。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

[!DNL Experience Platform] 提供了RESTful API和交互式UI，让您能够轻松为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| Adobe Audience Manager连接器的已弃用信号 | 将不再发送来自Audience Manger的信号级数据。 请注意，特征和区段的区段成员资格仍将包含在内。 由于进行此更改，将不再生成集客数据集。 |
| 重命名的数据集 | 由Audience Manger连接器生成的数据集将具有更新的名称和描述。 |
| 启用 [!DNL Profile] 在Audience Manger中切换 | [!DNL Profile] 可以启用或禁用切换，以将数据集提升到 [!DNL Real-Time Customer Profile]. 默认情况下，将启用切换。 |
| 云存储系统的UI支持 | 新的源连接器 [!DNL Azure Data Lake Storage Gen2] 中。 |
| CRM系统的UI支持 | 新的源连接器 [!DNL HubSpot], [!DNL Salesforce Service Cloud]和 [!DNL ServiceNow] 中。 |
| 对数据库系统的用户界面支持 | 新的源连接器 [!DNL AWS Redshift], [!DNL Google BigQuery], [!DNL MariaDB], [!DNL Microsoft SQL Server]和 [!DNL MySQL] 中。 |

**已知问题**

* None

要进一步了解源，请参阅 [源概述](../../sources/home.md).
